## 📄 Filebeat Client (8.x)

**Tested with Filebeat 8.19.12** (current 8.x series version).

#### Minimal Configuration for `filebeat.yml`:

```yaml
filebeat.inputs:

  - type: log
    enabled: true
    paths:
      - /var/log/auth.log
    fields:
      log_file: auth.log
    fields_under_root: true

output.logstash:
  hosts: ["GRAYLOG_HOST:5044"]
```

#### Multi-Node (Load Balancing):

```yaml
output.logstash:
  hosts: ["GRAYLOG_HOST_1:5044", "GRAYLOG_HOST_2:5044","GRAYLOG_HOST_3:5044"]
  loadbalance: true
```

#### Test Output Connectivity:

```bash
sudo filebeat test output
```

> ⚠️ Do **not** use `output.elasticsearch` — Graylog Beats input requires **Logstash output**.
