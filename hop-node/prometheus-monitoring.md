---
description: Monitor metrics with Prometheus
---

# Prometheus Monitoring

_Notice: The Prometheus integration is very primitive and doesn't contain many metrics yet._ [_Pull requests_](https://github.com/hop-protocol/hop) _are welcome!_

You can use [Prometheus](https://prometheus.io/) to monitor metrics

### Enabling metrics

Enable metrics in your hop node config file `~/.hop-node/config.json`

```json
  "metrics": {
    "enabled": true,
    "port": 8080
  }
```

### Running Prometheus

Create `prometheus.yml` config

```yaml
global:
  scrape_interval:     15s

  external_labels:
    monitor: 'hop-node-monitor'

scrape_configs:
  - job_name: 'prometheus'

    scrape_interval: 5s

    static_configs:
      - targets: ['localhost:8080']
```

Run Prometheus with docker

```bash
docker run -v $PWD/prometheus.yml:/etc/prometheus/prometheus.yml --net=host -p 9090:9090 prom/prometheus
```

### Running Grafana

Run Grafana with docker

```bash
docker run --net=host -p 3000:3000 grafana/grafana
```
