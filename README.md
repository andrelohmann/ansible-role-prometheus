andrelohmann.prometheus
=======================

Install and configure prometheus

Role Variables
--------------

    prometheus_config:
      global:
        scrape_interval: 15s
      external_labels:
        monitor: codelab-monitor
      scrape_configs:
      - job_name: prometheus
        scrape_interval: 5s
        scrape_timeout: 5s
        static_configs:
        - targets:
          - 'localhost:9090'
          labels:
            group: prometheus
    prometheus_rules:
      groups:
      - name: cpu-node
        rules:
        - record: 'job_instance_mode:node_cpu_seconds:avg_rate5m'
          expr: 'avg by (job, instance, mode) (rate(node_cpu_seconds_total[5m]))'

Example Playbook
----------------

    - hosts: prometheus
      roles:
      - andrelohmann.prometheus

License
-------

MIT

Author Information
------------------

https://github.com/andrelohmann
