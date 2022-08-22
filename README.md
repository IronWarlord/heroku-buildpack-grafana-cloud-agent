# Heroku Buildpack for Grafana Cloud Agent

This is an unofficial Heroku buildpack for
[Grafana Cloud Agent](https://github.com/grafana/agent) deployments.

## Usage

### Binary
Automaticly downloads grafana agent binary that will be placed in `bin/grafana-agent`

### Config
Your config file should be placed into the root as `config/grafana-agent.yml`.

The buildpack will substitute any environment variables. Example:

```yaml
---
server:
  http_listen_port: $PORT

prometheus:
  wal_directory: "./"
  global:
    scrape_interval: 5s
  configs:
    - name: agent
      host_filter: false
      scrape_configs:
        - job_name: metrics
          metrics_path: /metrics
          scheme: https
          static_configs:
            - targets: ['target.abc.xyz']
      remote_write:
        - url: https://prom.abc.xyz/api/prom/push
          basic_auth:
            username: $USERNAME
            password: $PASSWORD
```
