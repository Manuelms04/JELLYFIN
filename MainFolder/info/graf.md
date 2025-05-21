<h1 align="center">GRAFANA</h1>

- Grafana es la herramienta que permite visualizar, analizar y supervisar de forma gráfica los datos recogidos por Prometheus sobre el estado y rendimiento del servidor multimedia y sus servicios

---

### *¿Por qué se usa Grafana en este trabajo?*

- `Visualización avanzada de métricas`
    - Grafana convierte los datos recogidos por Prometheus en gráficas, paneles y dashboards interactivos. Esto hace que la información del estado del servidor sea mucho más comprensible y útil.

- `Interfaz intuitiva y personalizable`
    - Con Grafana se puede crear dashboards personalizados para visualizar lo único que interesa: uso de CPU, memoria, red, actividad de Jellyfin, etc. Es ideal para tener una visión rápida del estado del sistema.

- `Complemento perfecto para Prometheus`
    - Prometheus guarda las métricas, pero Grafana las presenta de forma visual, permitiendo analizar el rendimiento del servidor de manera más eficiente y amigable.

- `Acceso web desde cualquier dispositivo`
    - Al estar configurado con Docker, puedes acceder a Grafana desde el navegador usando `http://IP_VM:3000`, lo que facilita su uso desde cualquier equipo, ya sea dentro o fuera de la red (si se usa junto con DuckDNS).

- `Alertas y supervisión inteligente`
    - Grafana permite configurar alertas personalizadas (por ejemplo, si el uso de CPU supera cierto porcentaje), lo cual es útil para mantener el servidor funcionando correctamente incluso sin supervisión constante.

---

<p align="center">
  <img src="/MainFolder/img/graf.png" alt="GRAFANA" width="800" height="200">
</p>

