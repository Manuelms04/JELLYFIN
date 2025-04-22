# 🎓 TFG ASIR - Servidor Multimedia con Jellyfin en Máquina Virtual

---

Este proyecto consiste en la implementación de un servidor multimedia utilizando Jellyfin dentro de una máquina virtual basada en Debian. El sistema incluye monitorización con `Prometheus` y `Grafana`, y es accesible desde la red local o remota mediante `DuckDNS`.

---

## Referencia 

> [`VIDEO 1 YT`](https://youtu.be/ZJiUetTJVxw?si=ET_eLOi5_8n4LdUq>)

> [`VIDEO 2 YT`](https://youtu.be/4RSUCgCIPqo?si=OHxE6xW3Y7VyMilL)

> [`GIT HUB`](https://github.com/fernandoayoso/TFG_FernandoGarciaAyoso)


---

## Aplicaciones

> [`DUCKDNS`](/MainFolder/info/ddns.md)
 
> [`DOCKER`](/MainFolder/info/docker.md)
 
> [`GRAFANA`](/MainFolder/info/graf.md)

> [`PROMETHEUS`](/MainFolder/info/pro.md)

---

## ✅ 1. Requisitos

- **VirtualBox** instalado en el equipo principal.
- **Imagen ISO de Debian 12** (o Ubuntu Server 22.04).
- Máquina Virtual con:
  - 2 CPU
  - 2 GB de RAM
  - 20 GB de disco duro (dinámico)
  - Red en modo "puente" o NAT
- Carpeta compartida (para almacenamiento multimedia).
- Conexión a Internet (el host proporciona conectividad).

---

## 💾 2. Instalación del Sistema Operativo

1. Descargar Debian desde [https://www.debian.org/distrib/](https://www.debian.org/distrib/)
2. Crear una VM en VirtualBox:
   - Tipo: Linux
   - Versión: Debian (64-bit)
3. Asociar la ISO e instalar el sistema operativo.
4. Crear un usuario con permisos `sudo`.

---

## ⚙️ 3. Preparación del Sistema

En la VM, se debe abrir la terminal y ejecutar:

```bash
sudo apt update
```

```bash
sudo apt upgrade -y
```

```bash
sudo apt install net-tools htop curl wget git ufw
```


## 📦 4. Instalación de Docker

**Para instalar Docker y Docker Compose, seguir los siguientes pasos:**

- Instalar Docker:
```bash
sudo apt update
```

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
```

```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
```

```bash
sudo apt update
```

```bash
sudo apt install docker-ce
```


- Verificar que Docker se haya instalado correctamente:

```bash
sudo docker --version
```

### Instalar Docker Compose:

```bash
sudo apt install docker-compose
```

- Verificar la instalación de Docker Compose:

```bash
docker-compose --version
```

## 📦 5. Instalación de Jellyfin con Docker
Ahora vamos a crear los contenedores de Jellyfin, Prometheus y Grafana usando Docker.

### Paso 1: Crear el archivo docker-compose.yml
Dentro de la máquina virtual, crea un directorio para tu proyecto y dentro de él crea el archivo docker-compose.yml:

```bash
mkdir servidor_multimedia
```

```bash
cd servidor_multimedia
```

```bash
nano docker-compose.yml
```

### Paso 2: Definir los servicios en el archivo docker-compose.yml
Agrega lo siguiente en el archivo docker-compose.yml:

```bash
version: "3"

services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
    restart: unless-stopped
    ports:
      - "8096:8096"  # Puerto de Jellyfin
    volumes:
      - /path/to/your/media:/media  # Cambia esta ruta por la carpeta donde se almacenan tus archivos multimedia
      - /path/to/config:/config  # Configuración de Jellyfin
    environment:
      - TZ=Europe/Madrid
    networks:
      - media-network

  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    restart: unless-stopped
    ports:
      - "9090:9090"  # Puerto de Prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml  # Configuración de Prometheus
    networks:
      - media-network

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    restart: unless-stopped
    ports:
      - "3000:3000"  # Puerto de Grafana
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin  # Contraseña de administrador de Grafana
    networks:
      - media-network

networks:
  media-network:
    driver: bridge
```

### Paso 3: Configuración de Prometheus
Crea el archivo `prometheus.yml` que será montado en el contenedor de Prometheus. Este archivo define cómo Prometheus obtiene las métricas de los contenedores y otros servicios.

Ejemplo de `prometheus.yml` básico:

```bash
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'jellyfin'
    static_configs:
      - targets: ['jellyfin:8096']
```

Guardar este archivo como prometheus.yml en el mismo directorio donde está el archivo docker-compose.yml.

6. Levantar los contenedores con Docker Compose

- Una vez que todo esté configurado, usa Docker Compose para levantar los contenedores:

```bash
docker-compose up -d
```

- Verifica que los contenedores estén funcionando:

```bash
docker ps
```

## 7. Acceder a los servicios
- Jellyfin: Accede desde el navegador en `http://IP_DE_LA_VM:8096`.

- Prometheus: Accede a la interfaz web de Prometheus en `http://IP_DE_LA_VM:9090`.

- Grafana: Accede a la interfaz web de Grafana en `http://IP_DE_LA_VM:3000`. El usuario es `admin` y la contraseña es `admin`.

## 8. Configurar Grafana para visualizar métricas de Prometheus
- En Grafana, ve a `Configuration` y selecciona `Data Sources`. Agrega Prometheus como fuente de datos y usa la URL: `http://prometheus:9090`. Luego, crea tus dashboards personalizados.

## 🔐 9. Acceso remoto con DuckDNS
*Crear una cuenta en DuckDNS.*

- Crear un script `duck.sh`:

```bash
echo url="https://www.duckdns.org/update?domains=TU_DOMINIO&token=TU_TOKEN&ip=" | curl -k -o duck.log -K -
```

- Asignar permisos para que el script sea ejecutable:

```bash
chmod 700 duck.sh
```

- Añadir al crontab para ejecutar el script cada 5 minutos:

```bash
crontab -e
```

*Se añade la siguiente linea*

```bash
*/5 * * * * /ruta/duck.sh >/dev/null 2>&1
```

## 🧾 Créditos y Autor

- *Autor:*
  - [`MANUEL MORENO SOSA`](https://github.com/Manuelms04)
- *Curso:*
  - `2º ASIR`
- *Centro:*
  - `IES Rodrigo Caro`
- *Fecha:*
  - `Mayo 2025`



