# DevOps Local Environment

Этот проект предоставляет локальную DevOps-среду на основе Docker Compose с инструментами для разработки и тестирования инфраструктуры.

## Сервисы

В проекте используются следующие сервисы:

- **DevOps контейнер (`devops`)**  
  Основной контейнер для работы с инфраструктурой:  
  - Terraform  
  - Ansible  
  - Python + boto3  
  - kubectl  
  - Helm  
  - AWS CLI  
  - Git, SSH, Make  

- **Kubernetes (Kind)**  
  Локальный Kubernetes-кластер для тестирования манифестов и Helm charts.

- **Prometheus**  
  Система мониторинга.

- **Grafana**  
  Визуализация метрик. Доступ: `http://localhost:3000`  
  - Можно изменить через переменные окружения `GF_SECURITY_ADMIN_USER` и `GF_SECURITY_ADMIN_PASSWORD`.

- **Kafka + Zookeeper**  
  Локальный брокер сообщений для тестирования топиков и потоков данных.

- **GitLab Runner**  
  Для тестирования CI/CD пайплайнов локально.

- **Docker Registry**  
  Локальный приватный реестр для образов.

---

## Структура проекта:
project/
├─ docker-compose.yml
├─ devops/ # Dockerfile и утилиты DevOps контейнера
├─ workspace/ # Основная рабочая директория для Terraform, Ansible, Kubernetes
│ ├─ terraform/
│ ├─ ansible/
│ ├─ kubernetes/
│ └─ scripts/
├─ prometheus/
│ └─ prometheus.yml
├─ grafana/
│ └─ dashboards/
├─ kafka-data/ # Volume для Kafka
└─ .gitignore

- `workspace/` — папка для работы с кодом и конфигурациями через DevOps контейнер.
- Отдельные конфиги для Prometheus, Grafana и Kafka хранятся в своих папках.

---

## Как запустить

1. Собрать и запустить контейнеры:

```bash
docker-compose up -d --build