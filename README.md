<h1 align="center">🎓 TFG ASIR 🎓</h1>
<h1 align="center"> IMPLEMENTACIÓN DE UN SERVIDOR MULTIMEDIA CON JELLYFIN </h1>


---


<h2 align="center"> 📘 Introducción 📘 </h2>


- Este proyecto consiste en la implementación de un servidor multimedia con `Jellyfin` dentro de una `MV`, utilizando contenedores gestionados mediante `Docker` y `Docker Compose`

- Incluye un entorno de `Monitorización con Prometheus y Grafana`, lo que permite supervisar en tiempo real el estado y rendimiento del servidor

- El acceso remoto se ha configurado mediante `DuckDNS`, garantizando la conexión externa sin necesidad de una IP fija. Para asegurar las conexiones, se ha desplegado `Caddy`, para proporcionar certificados SSL automáticos, gestionando `HTTPS` de forma sencilla y eficaz

- Además, se ha integrado un sistema de `Alertas automáticas por Telegram`, que notifica fallos o anomalías detectadas, facilitando una gestión proactiva y mejorando la fiabilidad del sistema

- Como funcionalidad adicional, se ha implementado la `Integración de Samba`, permitiendo el acceso y compartición de archivos multimedia entre el servidor y otros dispositivos de la red local


---


<h2 align="center"> 💻 Software Implementado 💻 </h2>

<div align="center">
  <table>
    <tr>
      <td><a href="/MainFolder/info/jelly.md"> JELLYFIN </a></td>
      <td><a href="/MainFolder/info/docker.md"> DOCKER </a></td>
      <td><a href="/MainFolder/info/ddns.md"> DUCKDNS </a></td>
      <td><a href="/MainFolder/info/caddy.md"> CADDY </a></td>
    </tr>
    <tr>
      <td><a href="/MainFolder/info/pro.md"> PROMETHEUS </a></td>
      <td><a href="/MainFolder/info/graf.md"> GRAFANA </a></td>
      <td><a href="/MainFolder/info/tele.md"> TELEGRAM </a></td>
      <td><a href="/MainFolder/info/samba.md"> SAMBA </a></td>
    </tr>
  </table>
</div>


---


<h2 align="center">✅ Requisitos ✅</h2>

- **Imagen ISO de Debian 12**
- **Máquina Virtual configurada con:**
  - 2 CPU
  - 2 GB de RAM
  - 20 GB de disco duro (preferiblemente dinámico)
  - Red en modo **puente** o **NAT con reenvío de puertos**
- **Acceso a Internet funcional desde la VM**
- **Cuenta en [`DuckDNS`](https://www.duckdns.org/)** (para nombre de dominio dinámico)
- **Cuenta de Telegram con bot creado** (para recibir alertas desde Grafana)
- **Software necesario instalado en Debian:**
  - `curl`, `git`, `nano`, `wget`
  - `docker` y `docker-compose`
  - `samba` *(para compartir archivos multimedia)*
  - `cron` *(para actualizar IP en DuckDNS)*
- **Carpeta compartida local para medios multimedia** *(en la VM o desde el host)*
- **Puertos abiertos y configurados correctamente:**
  - `8096` → Jellyfin
  - `9090` → Prometheus
  - `3000` → Grafana
  - `80 y 443` → HTTPS *(Caddy)*
 

---


<h2 align="center"> 📋 Índice de Instalación Paso a Paso 📋 </h2>

> [`🔧 PREPARACIÓN DEL SISTEMA OPERATIVO DEBIAN 🔧`](/MainFolder/info/1.md)

> [`🌍 CONFIGURACIÓN DE DUCKDNS 🌍`](/MainFolder/info/2.md)

> [`🐳 INSTALACIÓN DE DOCKER Y DOCKER COMPOSE 🐳`](/MainFolder/info/3.md)

> [`🎬 DESPLIEGUE DE JELLYFIN 🎬 `](/MainFolder/info/4.md)

> [`📈 CONFIGURACIÓN DE PROMETHEUS 📈`](/MainFolder/info/5.md)

> [`📊 CONFIGURACIÓN DE GRAFANA 📊`](/MainFolder/info/6.md)

> [`🔐 CONFIGURACIÓN DE HTTPS CON CADDY 🔐`](/MainFolder/info/7.md)

> [`🔔 ALERTAS AUTOMÁTICAS POR TELEGRAM 🔔`](/MainFolder/info/8.md)

> [`📁 INTEGRACIÓN DE SAMBA PARA ARCHIVOS MULTIMEDIA 📁`](/MainFolder/info/9.md)


---


<h2 align="center"> 🔗 Referencias 🔗 </h2>

- [`VIDEO 1 YT`](https://youtu.be/ZJiUetTJVxw?si=ET_eLOi5_8n4LdUq>)

- [`VIDEO 2 YT`](https://youtu.be/4RSUCgCIPqo?si=OHxE6xW3Y7VyMilL)

- [`GIT HUB`](https://github.com/fernandoayoso/TFG_FernandoGarciaAyoso)


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






<!---


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






# Configuración de Jellyfin Seguro (HTTPS) usando Caddy Server en Docker Compose (Debian 12 + DuckDNS)

Guía para desplegar un servidor Jellyfin accesible de forma segura mediante HTTPS utilizando **Caddy Server** a través de **Docker Compose**, en conjunto con un dominio de **DuckDNS**.

---

## Requisitos Previos

- Sistema operativo Debian 12 funcional.
- Servidor Jellyfin instalado (o accesible) en el puerto `8096`.
- Dominio configurado en DuckDNS (por ejemplo, `manuelms.duckdns.org`) y correctamente actualizado.
- Docker y Docker Compose instalados en el sistema.
- Puertos **80** y **443** abiertos en el firewall y redirigidos en el router hacia el servidor Debian.

---

# Despliegue de Caddy Server usando Docker Compose

---

## Paso 1: Crear la estructura de directorios

Crear una carpeta para alojar la configuración de Caddy:

```bash
mkdir -p /home/usuario/caddy
cd /home/usuario/caddy
```

Paso 2: Crear el archivo Caddyfile
Crear un archivo llamado Caddyfile:

```bash
nano Caddyfile
```

Agregar el siguiente contenido:

```bash
manuelms.duckdns.org {
    reverse_proxy host.docker.internal:8096
}
```

Notas:

En sistemas Linux, si host.docker.internal no está disponible, puede ser necesario usar la IP del host (172.17.0.1) o la IP privada del servidor.

El proxy se encarga de redirigir las solicitudes HTTPS al servidor Jellyfin en el puerto 8096.

Paso 3: Crear el archivo docker-compose.yml
Crear un archivo llamado docker-compose.yml:

```bash
nano docker-compose.yml
```

Agregar el siguiente contenido:

```bash
version: "3.8"

services:
  caddy:
    image: caddy:latest
    container_name: caddy
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./Caddyfile:/etc/caddy/Caddyfile
      - caddy_data:/data
      - caddy_config:/config
    networks:
      - caddy_net

networks:
  caddy_net:

volumes:
  caddy_data:
  caddy_config:
```

### Descripción de la configuración:


<div align="center">
  <table>
    <tr>
      <td><strong>ELEMENTO</strong></td>
      <td><strong>DESCRIPCIÓN</strong></td>
    </tr>
    <tr>
      <td><code>caddy</code></td>
      <td>Servicio principal que ejecuta el contenedor de Caddy </td>
    </tr>
    <tr>
      <td><code>ports</code></td>
      <td>Publica los puertos 80 y 443 del contenedor al host </td>
    </tr>
    <tr>
      <td><code>volumes</code></td>
      <td>Permite la persistencia de configuraciones y certificados, por ejemplo /data o /config </td>
    </tr>
    <tr>
      <td><code>networks</code></td>
      <td>Crea una red interna para facilitar la comunicación entre contenedores, como caddy_net </td>
    </tr>
  </table>
</div>




Paso 4: Lanzar Caddy con Docker Compose
Desde el mismo directorio donde se encuentran Caddyfile y docker-compose.yml:

```bash
docker compose up -d
```

Esto descargará la imagen oficial de Caddy, levantará el contenedor, y configurará automáticamente HTTPS utilizando Let's Encrypt

Acceso al servidor Jellyfin
Una vez desplegado Caddy Server, Jellyfin estará accesible de manera segura mediante:

```bash
https://manuelms.duckdns.org
```

Caddy solicitará automáticamente un certificado SSL válido y se encargará de su renovación periódica

### Consideraciones Adicionales
  - Es fundamental que DuckDNS actualice correctamente la IP pública para evitar problemas con el certificado SSL

  - Jellyfin debe estar corriendo y accesible en el puerto 8096 desde la perspectiva de Caddy

  - En caso de que Jellyfin también esté en un contenedor, se recomienda conectarlo a la red caddy_net usando Docker Compose

*Si se requiere ver los registros de Caddy para solucionar problemas:*

```bash
docker compose logs -f caddy
```

*Para detener el servicio:*

```bash
docker compose down
```




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



