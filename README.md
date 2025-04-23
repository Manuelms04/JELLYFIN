<h1 align="center">🎓 TFG ASIR 🎓</h1>
<h1 align="center"> IMPLEMENTACIÓN DE UN SERVIDOR MULTIMEDIA CON JELLYFIN </h1>

---

<h2 align="center"> 📘 Introducción 📘 </h2>


- Este proyecto consiste en la implementación de un servidor multimedia con Jellyfin dentro de una máquina virtual con Debian, utilizando contenedores gestionados mediante Docker y Docker Compose. El sistema incluye un entorno de monitorización con Prometheus y Grafana, lo que permite supervisar su estado en tiempo real.

- Además, se ha configurado el acceso remoto mediante DuckDNS, garantizando la conexión externa sin necesidad de IP fija. Como valor añadido, se ha integrado un sistema de alertas automáticas por Telegram, que notifica cualquier fallo o anomalía detectada, permitiendo una gestión proactiva del servidor y aumentando su fiabilidad
---

## Referencia 

> [`VIDEO 1 YT`](https://youtu.be/ZJiUetTJVxw?si=ET_eLOi5_8n4LdUq>)

> [`VIDEO 2 YT`](https://youtu.be/4RSUCgCIPqo?si=OHxE6xW3Y7VyMilL)

> [`GIT HUB`](https://github.com/fernandoayoso/TFG_FernandoGarciaAyoso)


---

<h2 align="center">Software Implementado</h2>

<div align="center">
  <table>
    <tr>
      <td><a href="/MainFolder/info/jelly.md"> JELLYFIN </a></td>
      <td><a href="/MainFolder/info/ddns.md"> DUCKDNS </a></td>
      <td><a href="/MainFolder/info/docker.md"> DOCKER </a></td>
    </tr>
    <tr>
      <td><a href="/MainFolder/info/pro.md"> PROMETHEUS </a></td>
      <td><a href="/MainFolder/info/graf.md"> GRAFANA </a></td>
      <td><a href="/MainFolder/info/tele.md"> TELEGRAM </a></td>
    </tr>
  </table>
</div>




<!---
> [`JELLYFIN`](/MainFolder/info/jelly.md)

> [`DUCKDNS`](/MainFolder/info/ddns.md)
 
> [`DOCKER`](/MainFolder/info/docker.md)

> [`PROMETHEUS`](/MainFolder/info/pro.md)
 
> [`GRAFANA`](/MainFolder/info/graf.md)

> [`TELEGRAM`](/MainFolder/info/tele.md)
--->

---

## ✅ 1. Requisitos ✅

- Imagen ISO de Debian 12
- Máquina Virtual con:
  - 2 CPU
  - 2 GB de RAM
  - 20 GB de disco (dinámico)
  - Red en modo puente o NAT
- Carpeta compartida para almacenamiento multimedia
- Conexión a Internet
- Cuenta en [DuckDNS](https://www.duckdns.org/)
- Cuenta de Telegram y bot creado

---

## 💾 2. Instalación del Sistema Operativo 💾

1. Descargar Debian: https://www.debian.org/distrib/
2. Crear una MV en VirtualBox:
   - Tipo: Linux
   - Versión: Debian (64-bit)
3. Instalar el sistema operativo en la MV
4. Crear un usuario con permisos sudo

---

## ⚙️ 3. Preparación del Sistema ⚙️

Ejecutar en la terminal de la MV:

```bash
sudo apt update && sudo apt upgrade -y
```

```bash
sudo apt install net-tools htop curl wget git ufw
```

---

## 🐳 4. Instalación de Docker y Docker Compose 🐳

**Para instalar Docker y Docker Compose, seguir los siguientes pasos:**

- Instalar Docker:
```bash
sudo apt update
```

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```bash
sudo apt update
```

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose
```

- Verificar que Docker se haya instalado correctamente:

```bash
sudo docker --version
```

```bash
docker-compose --version
```

---

## 📦 5. Despliegue de Servicios con Docker Compose 📦

*Ahora vamos a crear los contenedores de Jellyfin, Prometheus y Grafana usando Docker.*

- ### Paso 1: Crear el archivo docker-compose.yml
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

- ### Paso 2: Definir los servicios en el archivo docker-compose.yml
Agregar lo siguiente en el archivo docker-compose.yml:

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
      - /path/to/your/media:/media  # Cambiar esta ruta por la carpeta donde se almacenan los archivos multimedia
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

- ### Paso 3: Configuración de Prometheus
Crea el archivo `prometheus.yml` que será montado en el contenedor de Prometheus. Este archivo define cómo Prometheus obtiene las métricas de los contenedores y otros servicios

Crear `prometheus.yml` en el mismo directorio

```bash
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'jellyfin'
    static_configs:
      - targets: ['jellyfin:8096']
```

Guardar este archivo como `prometheus.yml` en el mismo directorio donde está el archivo docker-compose.yml

---

 ## ⬆️ 7. Levantar los contenedores con Docker Compose ⬆️

- Una vez que todo esté configurado, usa Docker Compose para levantar los contenedores:

```bash
docker-compose up -d
```

- Verifica que los contenedores estén funcionando:

```bash
docker ps
```

---

## 📡 7. Acceso a los servicios 📡
- Jellyfin: Accede desde el navegador en `http://IP_DE_LA_MV:8096`

- Prometheus: Accede a la interfaz web de Prometheus en `http://IP_DE_LA_MV:9090`

- Grafana: Accede a la interfaz web de Grafana en `http://IP_DE_LA_MV:3000`. El usuario es `admin` y la contraseña es `admin`

---

## 🔔 8. Configuración de Alertas con Telegram 🔔

1. Crear un bot en Telegram con `@BotFather`

2. Obtener el token del bot

3. Obtener tu ID de usuario en Telegram: `https://api.telegram.org/botTOKEN/getUpdates`

4. Añadir la alerta en Grafana:
  - Ir a Alerting → Contact points
  - Añadir un Webhook con esta URL:

```bash
https://api.telegram.org/bot<TU_TOKEN>/sendMessage?chat_id=<TU_ID>&text=${message}
```

---

## 9. 📊 Configurar Grafana para visualizar métricas de Prometheus 📊
- En Grafana, ve a `Configuration` y selecciona `Data Sources`. Agrega Prometheus como fuente de datos y usa la URL: `http://prometheus:9090`. Luego, crea tus dashboards personalizados.

---

## 🌍 10. Acceso Remoto con DuckDNS 🌍

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

---

## 🧾 Autor

- *Autor:*
  - [`MANUEL MORENO SOSA`](https://github.com/Manuelms04)
- *Curso:*
  - `2º ASIR`
- *Centro:*
  - `IES Rodrigo Caro`
- *Fecha:*
  - `Mayo 2025`



