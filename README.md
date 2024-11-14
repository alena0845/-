# Руководство по установке Grafana + Prometheus + Node Exporter + VictoriaMetrics
## 1. Введение

В этом руководстве описаны этапы установки и базовой настройки системы мониторинга с использованием Grafana, Prometheus, Node Exporter и VictoriaMetrics.
## 2. Установка Prometheus
### Пошаговая инструкция:

    Загрузите актуальную версию Prometheus с официального сайта:
```
wget https://github.com/prometheus/prometheus/releases/download/v2.x.x/prometheus-2.x.x.linux-amd64.tar.gz
```
Распакуйте скачанный архив:
```
tar -xvzf prometheus-2.x.x.linux-amd64.tar.gz
cd prometheus-2.x.x.linux-amd64
```
Запустите Prometheus:
```
    ./prometheus --config.file=prometheus.yml

    При необходимости настройте конфигурационный файл prometheus.yml для кастомных нужд.
```
## 3. Установка Node Exporter
Пошаговая инструкция:

    Скачайте Node Exporter с репозитория Prometheus:
```
wget https://github.com/prometheus/node_exporter/releases/download/vX.X.X/node_exporter-X.X.X.linux-amd64.tar.gz
```
Извлеките содержимое архива:
```
tar -xvzf node_exporter-X.X.X.linux-amd64.tar.gz
cd node_exporter-X.X.X.linux-amd64
```
Для запуска выполните:
```
    ./node_exporter
```
    Проверьте доступность Node Exporter по адресу http://localhost:9100/metrics.

## 4. Установка VictoriaMetrics
Пошаговая инструкция:

    Загрузите VictoriaMetrics с официального сайта:
```
wget https://github.com/VictoriaMetrics/VictoriaMetrics/releases/download/vX.X.X/victoria-metrics-linux-amd64-vX.X.X.tar.gz
```
Распакуйте архив:
```
tar -xvzf victoria-metrics-linux-amd64-vX.X.X.tar.gz
cd victoria-metrics-linux-amd64
```
Запустите VictoriaMetrics:
```
./victoria-metrics-prod -retentionPeriod=1 -storageDataPath=/path/to/data
```
Добавьте в prometheus.yml конфигурацию для отправки метрик в VictoriaMetrics:
```
    remote_write:
      - url: "http://localhost:8428/api/v1/write"
````
## 5. Установка Grafana
Пошаговая инструкция:

    Добавьте репозиторий и установите Grafana:
```
sudo apt-get install -y software-properties-common
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
sudo apt-get update
sudo apt-get install grafana
```
Запустите Grafana:
```
    sudo systemctl start grafana-server
    sudo systemctl enable grafana-server

    Откройте интерфейс Grafana в браузере по адресу http://localhost:3000 (стандартные логин/пароль: admin / admin).
    В разделе "Configuration" > "Data Sources" добавьте Prometheus или VictoriaMetrics как источник данных.
```
## 6. Интеграция компонентов

    В файле prometheus.yml настройте сбор метрик от Node Exporter:
```
scrape_configs:
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']
```
В Grafana создайте дашборды для отображения метрик, собираемых Prometheus или VictoriaMetrics.

### Конфигурация docker-compose.yaml

<img width="710" alt="изображение" src="https://github.com/user-attachments/assets/83cf1308-cde8-4a2e-806d-da2647578c93">

<img width="710" alt="изображение" src="https://github.com/user-attachments/assets/55b9331d-71f1-4ebc-bb46-6b61d9aba181">

<img width="710" alt="изображение" src="https://github.com/user-attachments/assets/2322bfe5-f585-4147-acfe-0a9066413916">

<img width="710" alt="изображение" src="https://github.com/user-attachments/assets/9855b366-accf-484b-be45-f0ad7ba97c8f">

<img width="710" alt="изображение" src="https://github.com/user-attachments/assets/0bf45927-5113-4b91-9dd4-6c455d86886f">

<img width="710" alt="изображение" src="https://github.com/user-attachments/assets/3d73ea32-bb0c-401c-8854-76ffc7c5fb26">



### Демонстрация Prometheus

<img width="1439" alt="изображение" src="https://github.com/user-attachments/assets/090732fc-27d4-4829-a27f-0f550bfda38f">


### Демонстрация Grafana

<img width="1439" alt="изображение" src="https://github.com/user-attachments/assets/99747e1d-d1d2-4ad9-8158-3c8cd3c5d683">


### Файл Prometheus.yaml

<img width="1085" alt="изображение" src="https://github.com/user-attachments/assets/c6f45cb0-ab18-4c06-916b-8b413c4e9102">




