<h1 align="center">DOCKER</h1>

- En este proyecto, Docker se utiliza principalmente para simplificar la instalación, configuración y gestión de los servicios Jellyfin, Prometheus y Grafana dentro de la máquina virtual. Lo podemos ordenar mas detalladamente:

---

### *¿Por qué se usa Docker en este trabajo?*

- `AISLAMIENTO DE SERVICIOS`
    - Cada aplicación (Jellyfin, Prometheus, Grafana) corre en su propio contenedor, lo cual evita conflictos entre dependencias y versiones. Esto hace que el sistema sea más estable y fácil de mantener.

- `FACILIDAD DE DESPLIEGUE`
    - Gracias a Docker Compose, se puede levantar todos los servicios necesarios con un solo comando (docker-compose up -d). Esto ahorra mucho tiempo frente a la instalación manual de cada software.

- `PORTABILIDAD`
    - Todo el sistema puede replicarse fácilmente en otra máquina con Docker instalado, simplemente copiando los archivos de configuración (como el docker-compose.yml).

- `ESCALABILIDAD Y MANTENIMIENTO`
    - Si en el futuro se quiere añadir otro servicio (como por ejemplo un contenedor para copias de seguridad, un proxy inverso o un gestor de torrents), se puede hacer muy fácilmente modificando el docker-compose.yml.

- `CONTROL Y SUPERVISIÓN`
    - Al correr los servicios en contenedores, es fácil iniciar, detener, reiniciar o monitorizar cada uno usando comandos simples como docker ps o docker logs.

- `CONSISTENCIA DEL ENTORNO`
    - No importa en qué máquina se ejecute el proyecto, los contenedores garantizan que todo funcionará igual siempre que se mantenga el mismo docker-compose.yml

---

<p align="center">
  <img src="/MainFolder/img/docker.png" alt="DOCKER" width="700" height="350">
</p>

