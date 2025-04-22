## DOCKER

- En este proyecto de TFG, Docker se utiliza principalmente para simplificar la instalación, configuración y gestión de los servicios Jellyfin, Prometheus y Grafana dentro de la máquina virtual. Aquí te explico con más detalle para qué se usa Docker en este contexto:

### *🐳 ¿Por qué se usa Docker en este trabajo?*

- `Aislamiento de servicios`
    - Cada aplicación (Jellyfin, Prometheus, Grafana) corre en su propio contenedor, lo cual evita conflictos entre dependencias y versiones. Esto hace que el sistema sea más estable y fácil de mantener.

- `Facilidad de despliegue`
    - Gracias a Docker Compose, puedes levantar todos los servicios necesarios con un solo comando (docker-compose up -d). Esto ahorra mucho tiempo frente a la instalación manual de cada software.

- `Portabilidad`
    - Todo el sistema puede replicarse fácilmente en otra máquina con Docker instalado, simplemente copiando los archivos de configuración (como el docker-compose.yml).

- `Escalabilidad y mantenimiento`
    - Si en el futuro se quiere añadir otro servicio (como por ejemplo un contenedor para copias de seguridad, un proxy inverso o un gestor de torrents), se puede hacer muy fácilmente modificando el docker-compose.yml.

- `Control y supervisión`
    - Al correr los servicios en contenedores, es fácil iniciar, detener, reiniciar o monitorizar cada uno usando comandos simples como docker ps o docker logs.

- `Consistencia del entorno`
    - No importa en qué máquina se ejecute el proyecto, los contenedores garantizan que todo funcionará igual siempre que se mantenga el mismo docker-compose.yml
