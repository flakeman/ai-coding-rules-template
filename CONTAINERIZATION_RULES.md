# Kubernetes и Контейнеризация - Правила и Принципы для Web-разработки

## 1. Архитектурные Принципы

### 1.1 Микросервисная архитектура
- Один контейнер = одна функция/сервис
- Сервисы должны быть независимыми и масштабируемыми
- Слабая связанность, высокая когезия
- Правило 12-Factor App для всех контейнеров

### 1.2 Cloud-Native Design
- Приложение должно быть stateless (при возможности)
- Хранение состояния только в external storage (DB, Redis, S3)
- Готовность к graceful shutdown
- Метрики и логи должны быть centralized

### 1.3 Portable & Reproducible
- Контейнер работает одинаково везде (dev/staging/prod)
- Явная версионизация образов (vX.Y.Z, не latest)
- Все зависимости в Dockerfile, ничего на хосте
- Конфигурация через environment переменные или ConfigMaps

## 2. Docker Image Rules

### 2.1 Слои образа
- Минимизировать количество слоёв
- Часто меняющийся код = последний слой
- Кэшируемые операции (установка зависимостей) выше

### 2.2 Оптимизация размера
- Использовать slim/alpine образы как базу
- Multi-stage builds для уменьшения финального размера
- Удалять кэши пакетных менеджеров
- Максимальный размер - 500MB (ideally < 200MB)

### 2.3 Security
- Работать от non-root user
- Использовать read-only filesystem где возможно
- Scan образы на уязвимости
- Минимизировать количество утилит (no bash, только sh если нужно)

### 2.4 Image Tagging
```
registry.example.com/service-name:v1.2.3
registry.example.com/service-name:v1.2.3-sha-abc1234
registry.example.com/service-name:latest (only for dev)
```

## 3. Kubernetes Deployment Rules

### 3.1 Основные объекты
- **Pod** = минимальная единица развертывания
- **Deployment** для stateless сервисов (default)
- **StatefulSet** только если нужно состояние (БД, очередь)
- **DaemonSet** для сервисов на каждом ноде (логирование, мониторинг)
- **CronJob** для периодических задач

### 3.2 Resource Management
```yaml
resources:
  requests:
    memory: "64Mi"      # минимум для гарантии
    cpu: "100m"         # миллиядра (1000m = 1 CPU)
  limits:
    memory: "256Mi"     # максимум
    cpu: "500m"
```
- Всегда указывать requests и limits
- Requests базируются на реальных данных, не угадывать
- Limits должны быть примерно в 2 раза выше requests

### 3.3 Replicas & Scaling
```yaml
replicas: 3  # minimum для production
```
- Минимум 2 реплики для HA (ideally 3+)
- HorizontalPodAutoscaler (HPA) для автоскейлинга
- PodDisruptionBudget (PDB) для safe maintenance

### 3.4 Liveness & Readiness Probes
```yaml
livenessProbe:         # перезагрузить если dead
  httpGet:
    path: /health
    port: 8080
  initialDelaySeconds: 30
  periodSeconds: 10

readinessProbe:        # готов ли к трафику
  httpGet:
    path: /ready
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 5
```

### 3.5 Service Discovery
- Используй internal DNS: service-name.namespace.svc.cluster.local
- Сервис = стабильный IP + LoadBalancer
- Для external traffic используй Ingress (не NodePort в prod)

## 4. ConfigMap & Secrets Management

### 4.1 ConfigMap для конфигурации
```yaml
# Не для secrets!
# Для: URLs, timeout значения, feature flags
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  DB_HOST: "postgres.default.svc.cluster.local"
  LOG_LEVEL: "info"
```

### 4.2 Secrets для sensitive data
```yaml
# Для: passwords, tokens, API keys
apiVersion: v1
kind: Secret
metadata:
  name: app-secrets
type: Opaque
data:
  DB_PASSWORD: base64encoded
  API_KEY: base64encoded
```
- Шифровать secrets at rest
- Использовать external secret management (HashiCorp Vault, SOPS)
- Никогда не коммитить secrets в git

## 5. Networking Rules

### 5.1 Network Policies
- По умолчанию deny всё, потом allow явно
- Pod-to-Pod communication через labels
- Ingress только на необходимые порты

### 5.2 Service Types
- **ClusterIP** (default) для internal communication
- **LoadBalancer** для external (облако)
- **NodePort** только для dev/testing

### 5.3 Ingress
- Используй Ingress Controller (nginx-ingress, Istio)
- TLS termination на Ingress
- Path-based routing для микросервисов

## 6. Storage Rules

### 6.1 Ephemeral Storage (по умолчанию)
- Данные в контейнере = временные
- Не надеяться на persistence без явного PVC

### 6.2 PersistentVolumes
```yaml
volumeMounts:
  - name: data
    mountPath: /data
volumes:
  - name: data
    persistentVolumeClaim:
      claimName: app-pvc
```
- Использовать PVC для stateful компонентов
- Правильный StorageClass для разных типов (fast SSD, backup, etc)

### 6.3 Data Backup
- Автоматический backup for databases
- Проверять восстановление периодически
- Retention policy (30 дней, 7 неделей, etc)

## 7. Logging & Monitoring

### 7.1 Логирование
- Писать логи в STDOUT/STDERR (не файлы)
- Structured logging (JSON формат)
- Логи = единый канал для всех сервисов
- Инструменты: ELK, Loki, Splunk

### 7.2 Метрики
```
# Expose на /metrics (Prometheus format)
# Для каждого сервиса
```
- Обязательно: request rate, latency, error rate
- Alerts на основе метрик
- Dashboard для каждого сервиса

### 7.3 Tracing
- Correlation ID для связи запросов
- Distributed tracing (Jaeger, Zipkin)
- Для tracking request flow в микросервисах

## 8. Deployment Patterns

### 8.1 Rolling Update (default)
```yaml
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxSurge: 1
    maxUnavailable: 0
```
- Плавная замена подов
- Zero downtime

### 8.2 Blue-Green Deployment
- Две одинаковые окружения
- Switch traffic между ними
- Instant rollback if needed

### 8.3 Canary Deployment
- Новая версия на 5-10% трафика
- Постепенное увеличение процента
- Откат if метрики плохие

### 8.4 Feature Flags
- Включать/выключать фичи без redeploy
- ConfigMap для toggle management

## 9. Security Best Practices

### 9.1 RBAC (Role-Based Access Control)
- Service accounts для каждого приложения
- Minimal permissions для каждого SA
- Не использовать default service account

### 9.2 Pod Security
- SecurityContext: runAsNonRoot, readOnlyRootFilesystem
- Network policies для restrict communication
- No privileged containers

### 9.3 Image Security
- Scan в CI/CD pipeline
- Sign images (cosign, etc)
- Private registry для internal images

### 9.4 Secrets Rotation
- Регулярно ротировать API ключи
- Graceful handling старых секретов
- Audit log для access к secrets

## 10. Development Workflow

### 10.1 Local Development
```bash
# k3s или Docker Desktop with K8s
# Minikube для testing
# skaffold для local dev loop
```

### 10.2 Testing
- Unit tests в контейнере
- Integration tests с docker-compose или k3s
- Load testing перед deployment

### 10.3 CI/CD Pipeline
```
Code Push → Build Image → Test → Push Registry → Deploy Dev →
→ Deploy Staging → Manual Approval → Deploy Prod
```

### 10.4 GitOps
- Все конфиги в git
- ArgoCD/Flux для auto-sync
- Source of truth = git repo

## 11. Observability Checklist
- [ ] Health checks (liveness + readiness)
- [ ] Logs в stdout + структурированное логирование
- [ ] Prometheus metrics exposed
- [ ] Alerts настроены (SLA/SLO)
- [ ] Dashboards в Grafana
- [ ] Tracing для critical paths
- [ ] Error tracking (Sentry, etc)

## 12. Performance Optimization

### 12.1 Image cache optimization
- Layer order: rarely-changed → frequently-changed
- Parallel builds

### 12.2 Pod startup optimization
- Fast health checks (readinessProbe delay)
- Pre-warming containers
- Connection pooling

### 12.3 Resource utilization
- Right-sizing requests/limits
- HPA on custom metrics
- Bin packing optimization

## 13. Disaster Recovery

### 13.1 Backup Strategy
- PVC snapshots regular
- Helm charts в git
- Database backups automated

### 13.2 RTO/RPO
- RTO (Recovery Time Objective) < 1 hour
- RPO (Recovery Point Objective) < 15 min
- Test disaster recovery quarterly

### 13.3 Rollback Plan
- Always able to rollback previous version
- Helm charts versioning
- Database migrations reversible

## 14. Философия и Вайб

> **"Контейнеры - это средство, не цель"**

- Не усложняй без необходимости
- Всё в git, всё версионируется
- Автоматизируй рутину (CI/CD, monitoring)
- Логируй и мониторь от начала
- Fail fast, recover fast
- Infrastructure as Code (everything)
