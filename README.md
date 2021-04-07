# prometheus_config
Example config of a prometheus instance that connect 3 different instances and sum the metrics

Require some specific configurations on istio and kubernetes.

global:
  scrape_interval:     15s

scrape_configs:
- job_name: 'federate-cluster1'
  scrape_interval: 15s

  honor_labels: true
  metrics_path: '/federate'

  params:
    'match[]':
        - '{job="kubernetes-pods"}'

  static_configs:
    - targets: ['prometheus.X.X.X.X.nip.io']
    - labels:
        cluster: 'cluster1'
    - targets: ['prometheus.X.X.X.X.nip.io']
    - labels:
        cluster: 'cluster2'
    - targets: ['prometheus.X.X.X.X.nip.io']
    - labels:
        cluster: 'cluster3'

