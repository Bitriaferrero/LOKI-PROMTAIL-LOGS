# LOKI-PROMTAIL-LOGS
DOCKER LOCKI para RECIBIR LOGS DESDE PROMTAIL.
DOCKER PROMTAIL En el propio docker para poder acceder a los logs del direcotrio /var/log de host del docker.

Para poder recibir  logs desde otros host simplemente preparar en el host deseado la config del promtail apuntando a la ip donde tengamos loki de la forma siguiente:

promtail/config.yml

server:
  http_listen_port: 9080
  grpc_listen_port: 0

positions:
  filename: /tmp/positions.yaml

clients:
  # Apuntar a la ip donde tengas el loki para enviarle los LOGS.
  - url: http://192.168.1.107:3100/loki/api/v1/push

scrape_configs:
- job_name: system
  static_configs:
  - targets:
      - localhost
    # Definir los directorios de logs que deseo enviar a LOKI   
    labels:
      job: varlogs-rasberry4
      __path__: /var/log/*log

