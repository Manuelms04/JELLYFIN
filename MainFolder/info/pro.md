## PROMETHEUS

- Prometheus es el componente encargado de recolectar y almacenar métricas del servidor multimedia y sus servicios, permitiendo una monitorización continua y detallada de su estado y rendimiento

---

### *¿Por qué se usa Prometheus en este trabajo?*

- Monitorización del servidor en tiempo real
    - Prometheus se encarga de recopilar métricas de los servicios que tienes corriendo en la máquina virtual, especialmente de Jellyfin y del propio sistema. Esto permite saber cómo está funcionando tu servidor en todo           momento.

- Recopilación automática de métricas
    -Prometheus hace consultas periódicas (scrapes) a los servicios configurados (como Jellyfin o el sistema operativo) y guarda datos como uso de CPU, memoria, estado del contenedor, etc.

- Base para la visualización en Grafana
    - Aunque Prometheus por sí solo puede mostrar datos, su verdadero poder se ve cuando se conecta con Grafana. Prometheus actúa como la base de datos de métricas que Grafana usa para generar dashboards visuales e                intuitivos.

- Ligero y fácil de integrar con Docker
    - Está diseñado para trabajar en entornos de contenedores como Docker, por lo que es muy fácil de configurar usando el archivo docker-compose.yml.

- Detección temprana de problemas
    - Gracias a los datos que recopila, puedes detectar comportamientos anómalos en tu servidor (como sobrecarga de CPU, falta de memoria o caídas de servicio) antes de que afecten a los usuarios.

![PROMETHEUS](/MainFolder/img/pro.png)
