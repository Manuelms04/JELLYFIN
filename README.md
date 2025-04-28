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


<h2 align="center"> 💻 Software Implementado 💻 </h2>

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

> [`SAMBA`](/MainFolder/info/samba.md)

---

<h2 align="center">  ✅ Requisitos ✅ </h2>

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

<h2 align="center"> 💾 Instalación del Sistema Operativo 💾 </h2>

1. Descargar Debian: https://www.debian.org/distrib/
2. Crear una MV en VirtualBox:
   - Tipo: Linux
   - Versión: Debian (64-bit)
3. Instalar el sistema operativo en la MV
4. Crear un usuario con permisos sudo


---

<h2 align="center"> ⚙️ Preparación del Sistema ⚙️ </h2>

Ejecutar en la terminal de la MV:

```bash
sudo apt update && sudo apt upgrade -y
```

```bash
sudo apt install net-tools htop curl wget git ufw
```


---


<h2 align="center"> 🌍 Acceso Remoto con DuckDNS 🌍 </h2>

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


<h2 align="center"> 🐳 Instalación de Docker y Docker Compose 🐳 </h2>

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

<h2 align="center"> 📦 Despliegue de Servicios con Docker Compose 📦 </h2>

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

<h2 align="center"> ⬆️ Levantar los contenedores con Docker Compose ⬆️ </h2>

- Una vez que todo esté configurado, usa Docker Compose para levantar los contenedores:

```bash
docker-compose up -d
```

- Verifica que los contenedores estén funcionando:

```bash
docker ps
```

---


<h2 align="center"> 📡 Acceso a los servicios 📡 </h2>

- Jellyfin: Accede desde el navegador en `http://IP_DE_LA_MV:8096`

- Prometheus: Accede a la interfaz web de Prometheus en `http://IP_DE_LA_MV:9090`

- Grafana: Accede a la interfaz web de Grafana en `http://IP_DE_LA_MV:3000`. El usuario es `admin` y la contraseña es `admin`


---

<h2 align="center"> 🔔 Configuración de Alertas con Telegram 🔔 </h2>

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


<h2 align="center"> 📊 Configurar Grafana para visualizar métricas de Prometheus 📊 </h2>

- En Grafana, ve a `Configuration` y selecciona `Data Sources`. Agrega Prometheus como fuente de datos y usa la URL: `http://prometheus:9090`. Luego, crea tus dashboards personalizados.


---
---
---
---


<h2 align="center">📂 Integración de Samba para Compartir Archivos Multimedia 📂</h2>

<p align="center">Para facilitar el acceso y la carga de archivos multimedia desde otros equipos de la red local, se ha integrado un sistema de compartición de carpetas mediante <strong>Samba</strong>.</p>

---

<h3>1. 🔧 Instalación de Samba</h3>

*Ejecutar los siguientes comandos en la terminal de la máquina virtual Debian:*

```bash
sudo apt update
sudo apt install samba -y
```

<h3>2. 📁 Crear Carpeta Compartida</h3>

*Crear una carpeta destinada al almacenamiento compartido de archivos multimedia:*

```bash
sudo mkdir -p /home/usuario/MediaCompartida
sudo chmod -R 775 /home/usuario/MediaCompartida
```

<h3>3. 🔐 Crear Usuario Samba</h3>

*Añadir un usuario Samba para acceder desde otros dispositivos de la red:*

```bash
sudo smbpasswd -a tu_usuario
```

*Este será el usuario con el que se accede desde Windows u otros sistemas*

<h3>4. 📝 Configuración del archivo smb.conf</h3>

*Editar el archivo de configuración de Samba:*

```bash
sudo nano /etc/samba/smb.conf
```

*Y añadir al final del archivo:*

```bash
[Media]
   path = /home/usuario/MediaCompartida
   writable = yes
   browseable = yes
   valid users = tu_usuario
   create mask = 0664
   directory mask = 0775
```

<h3>5. 🔁 Reiniciar el servicio Samba</h3>

```bash
sudo systemctl restart smbd
```

<h3>6. 📡 Acceder desde otros equipos</h3>

*Desde otro ordenador con Windows, abre el explorador de archivos e introduce:*

```bash
\\IP_DE_LA_MV\Media
```

*Introduce las credenciales del usuario Samba cuando lo solicite*

<h3>🎯 BONUS: Integrar con Jellyfin</h3>

Para que Jellyfin acceda a esta carpeta compartida como su biblioteca multimedia, modificar el volumen en el archivo `docker-compose.yml`:

```bash
volumes:
  - /home/usuario/MediaCompartida:/media
```

*De esta forma, todo el contenido que se suba por Samba aparecerá automáticamente en Jellyfin para su reproducción o gestión*






---
---
---
---






# Configuración de Jellyfin Seguro (HTTPS) con Caddy en Debian 12 y DuckDNS

Guía para configurar un servidor Jellyfin accesible de forma segura mediante HTTPS utilizando **Caddy Server** y un dominio de DuckDNS

**Método utilizado: Caddy Server (fácil y gratuito)**

---

## Requisitos Previos
- Sistema operativo Debian 12 operativo
- Servidor Jellyfin instalado en el puerto `8096`
- Dominio configurado en DuckDNS (por ejemplo, `manuelms.duckdns.org`) y correctamente actualizado

---

## Paso 1: Instalación de Caddy Server en Debian 12

Ejecutar los siguientes comandos:

```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```
Caddy se instalará desde el repositorio oficial

## Paso 2: Configuración de Caddy como Proxy Inverso para Jellyfin
Editar el archivo de configuración de Caddy:

```bash
sudo nano /etc/caddy/Caddyfile
```

Agregar el siguiente contenido:

```bash
manuelms.duckdns.org {
    reverse_proxy localhost:8096
}
```

Guardar los cambios (`Ctrl+O`, `Enter`) y salir (`Ctrl+X`).

## Paso 3: Recargar Caddy para aplicar los cambios
```bash
sudo systemctl reload caddy
```

Caddy solicitará automáticamente un certificado SSL gratuito a Let's Encrypt, configurará HTTPS y gestionará la renovación automática del certificado

## Paso 4: Acceso al servidor Jellyfin
Para acceder al servidor Jellyfin de manera segura, ingresar en un navegador:

```bash
https://manuelms.duckdns.org
```

*La conexión se realizará a través de HTTPS*

- Consideraciones Finales
  - Es necesario abrir en el router los puertos 80 (HTTP) y 443 (HTTPS) redirigiéndolos hacia el servidor Debian

  - DuckDNS debe estar actualizado correctamente para asegurar la validez del certificado SSL

  - Caddy gestiona automáticamente tanto la adquisición como la renovación de certificados SSL

  - Este método es completamente gratuito y requiere un mínimo mantenimiento






---
---
---
---








<h2 align="center"> 🧾 Autor 🧾 </h2>

- *Autor:*
  - [`MANUEL MORENO SOSA`](https://github.com/Manuelms04)
- *Curso:*
  - `2º ASIR`
- *Centro:*
  - `IES Rodrigo Caro`
- *Fecha:*
  - `Mayo 2025`



