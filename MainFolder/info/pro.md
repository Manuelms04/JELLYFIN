<h1 align="center">PROMETHEUS</h1>

- Prometheus es el componente encargado de recolectar y almacenar métricas del servidor multimedia y sus servicios, permitiendo una monitorización continua y detallada de su estado y rendimiento

---

### *¿Por qué se usa Prometheus en este trabajo?*

- `MONITORIZACIÓN DEL SERVIDOR EN TIEMPO REAL`
    - Prometheus se encarga de recopilar métricas de los servicios que se encuentran corriendo en la máquina virtual, especialmente de Jellyfin y del propio sistema. Esto permite saber cómo está funcionando el servidor en todo momento

- `RECOPILACIÓN AUTOMÁTICA DE MÉTRICAS`
    - Prometheus hace consultas periódicas (scrapes) a los servicios configurados (como Jellyfin o el sistema operativo) y guarda datos como uso de CPU, memoria, estado del contenedor, etc

- `BASE PARA LA VISUALIZACIÓN EN GRAFANA`
    - Aunque Prometheus por sí solo puede mostrar datos, su verdadero poder se ve cuando se conecta con Grafana. Prometheus actúa como la base de datos de métricas que Grafana usa para generar dashboards visuales e intuitivos

- `LIGERO Y FÁCIL DE INTEGRAR CON DOCKER`
    - Está diseñado para trabajar en entornos de contenedores como Docker, por lo que es muy fácil de configurar usando el archivo docker-compose.yml

- `DETECCIÓN TEMPRANA DE PROBLEMAS`
    - Gracias a los datos que recopila, se puede detectar comportamientos anómalos en el servidor (como sobrecarga de CPU, falta de memoria o caídas de servicio) antes de que afecten a los usuarios

---

<p align="center">
  <img src="/MainFolder/img/pro.png" alt="PROMETHEUS" width="800" height="325">
</p>


