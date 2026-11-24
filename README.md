Proyecto final sistemas operativos
 
Este proyecto implementa una infraestructura con containers utilizando Docker Compose para el despliegue, balanceo de carga y 
monitoreo de servicios.

Este esta compuesto por:
-Nginx como proxy inverso y balanceador de carga.
-Tres instancias backend desarrolladas en Python con Flask.
-Prometheus para la recolección de métricas.
-Grafana para la visualización de métricas.
-cAdvisor para monitorear recursos de los contenedores.
-Nginx Prometheus Exporter para exponer métricas de Nginx.

Arquitectura:
-Nginx
 -Proxy inverso
 -Balanceador de carga

-Backends
 -backend1
 -backend2
 -backend3

-Monitoreo
 -Prometheus
 -backend1
 -backend2
 -backend3
 -cAdvisor
 -Nginx Exporter

-Visualización
 -Grafana

-Métricas recolectadas
 -Solicitudes HTTP
 -Uso de CPU
 -Uso de memoria
 -Tráfico de red
 -Uso de disco
 -Métricas de Nginx

Herramientas usadas:
-Docker
-Docker Compose
-Python 3.11
-Flask
-Prometheus
-Grafana
-Nginx
-cAdvisor
-Nginx Prometheus Exporter
-WSL2

Estructura del proyecto:
-proyecto-final-so/
 -docker-compose.yml
 -README.md
 -backend/
  -Dockerfile
  -app.py
  -requirements.txt
 -nginx/
  -nginx.conf
 -prometheus/
  -prometheus.yml
 -grafana/

Requisitos previos:
Antes de ejecutar el proyecto deben estar instalados:
-Docker Desktop
-Docker Compose
-WSL2
-Ubuntu en WSL

Levantar la infraestructura:
Desde la carpeta raíz del proyecto ejecutar docker compose up -d

Verificar los contenedores:
Usando docker ps deben aparecer estos servicios
-backend1
-backend2
-backend3
-nginx
-prometheus
-grafana
-cadvisor
-nginx-exporter

URLs de acceso:
-Aplicación Web (Nginx) http://localhost
-Prometheus http://localhost:9090
-Grafana http://localhost:3000
-cAdvisor http://localhost:8080

Prueba del balanceo de carga:
Ejecutar varias veces curl localhost
Se deben obtener respuestas alternadas entre
-Respuesta desde backend1
-Respuesta desde backend2
-Respuesta desde backend3
Lo anterior es para demostrar el correcto funcionamiento del balanceador de carga Nginx.

Métricas monitoreadas:
-Backends
 -Solicitudes HTTP totales.

-Nginx
 -Conexiones activas.
 -Solicitudes HTTP procesadas.

-cAdvisor
 -Uso de CPU por contenedor.
 -Uso de memoria por contenedor.
 -Tráfico de red.
 -Uso de almacenamiento.

Dashboards Grafana:
Configuramon paneles para visualizar
-Solicitudes HTTP http_requests_total
-Uso de memoria container_memory_usage_bytes
-Uso de CPU rate(container_cpu_usage_seconds_total[1m])
-Tráfico de red rate(container_network_receive_bytes_total[1m])
-Conexiones activas Nginx nginx_connections_active
-Solicitudes HTTP Nginx nginx_http_requests_total

Prueba de carga:
Para generar tráfico sobre la aplicación utilizamos
for i in {1..200}; do
    curl localhost > /dev/null
done
Puesto que este procedimiento nos permite observar actividad en los dashboards de Grafana y en las métricas recolectadas por 
Prometheus.

Detener la infraestructura:
Para esto se usa docker compose down

Autores:
-Robinson Garcia Rodriguez
-Ashley Gianella Mosquera
-Salome Cifuentes
