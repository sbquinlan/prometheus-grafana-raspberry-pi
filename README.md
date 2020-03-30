# Prometheus &amp; Grafana on a Raspberry Pi
Using docker-compose to run Prometheus &amp; Grafana on a Raspberry Pi

## Install Docker & docker-compose

Instructions from [dev.to](https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl)

* Install docker `curl -sSL https://get.docker.com | sh`
* Add permissions for user pi to run docker commands `sudo usermod -aG docker pi`
* Install docker-compose `sudo pip3 install docker-compose`

## Run Prometheus & Grafana

* Build and run `docker-compose up --build`
* Or run in the background `docker-compose up -d`
* Prometheus should now be running at `http://raspberrypi.local:9090`
* Grafana should now be running at `http://raspberrypi.local:3000`

## Prometheus.yml for multiple targets

If you're wanting to scrape from multiple targets, the `prometheus.yml` could look something like this:

```yaml
# prometheus.yml
global:
  scrape_interval: 5s
  external_labels:
    monitor: 'my-monitor'
scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']
  - job_name: 'environment'
    static_configs:
      - targets: ['10.1.1.2:8000']
        labels:
          group: 'environment'
          location: 'Melbourne'
      - targets: ['11.1.1.2:8000']
        labels:
          group: 'environment'
          location: 'Adelaide'
alerting:
  alertmanagers:
    - scheme: http
      static_configs:
      - targets: ['alertmanager:9093']
#rule_files:
#  - 'alert.rules'
```

## To export your data

Use the [Snapshot API](https://prometheus.io/docs/prometheus/2.1/querying/api/#snapshot).

* Enable it by passing the flag when running Prometheus `--web.enable-admin-api`
* Curl the Snapshot API: `curl -XPOST http://raspberrypi.local:9090/api/v1/admin/tsdb/snapshot`

### Credit
Thanks to [finestructure](https://github.com/finestructure/blogpost-prometheus) for the base.

