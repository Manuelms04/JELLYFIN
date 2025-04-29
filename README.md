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

<div align="center">

| [`JELLYFIN`](/MainFolder/info/jelly.mdd) | [`DOCKER`](/MainFolder/info/docker.md) |
|------------------------------------------|----------------------------------------|
| [`DUCKDNS`](/MainFolder/info/ddns.md)    | [`CADDY`](/MainFolder/info/caddy.md)   |
| [`PROMETHEUS`](/MainFolder/info/pro.md)  | [`GRAFANA`](/MainFolder/info/graf.md)  |
| [`TELEGRAM`](/MainFolder/info/tele.md)   | [`SAMBA`](/MainFolder/info/samba.md)   |
 
</div>


---


<h2 align="center">✅ Requisitos ✅</h2>

- **Imagen ISO de Debian 12**
- **Máquina Virtual configurada con:**
  - 2 CPU
  - 2 GB de RAM
  - 20 GB de disco duro *(preferiblemente dinámico)*
  - Red en modo **puente** o **NAT con reenvío de puertos**
- **Acceso a Internet funcional desde la MV**
- **Cuenta en [`DuckDNS`](https://www.duckdns.org/)** *(para nombre de dominio dinámico)*
- **Cuenta de Telegram con bot creado** *(para recibir alertas desde Grafana)*
- **Software necesario instalado en Debian:**
  - `curl`, `git`, `nano`, `wget`
  - `docker` y `docker-compose`
  - `samba` *(para compartir archivos multimedia)*
  - `cron` *(para actualizar IP en DuckDNS)*
- **Carpeta compartida local para medios multimedia** *(en la MV o desde el host)*
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




<div align="center">

| [`🔧 PREPARACIÓN DEL SISTEMA OPERATIVO DEBIAN 🔧`](/MainFolder/info/1.md) | [`📈 CONFIGURACIÓN DE PROMETHEUS 📈`](/MainFolder/info/5.md) |
|-------------------------------------------------------------------------|-------------------------------------------------------------|
| [`🌍 CONFIGURACIÓN DE DUCKDNS 🌍`](/MainFolder/info/2.md)               | [`📊 CONFIGURACIÓN DE GRAFANA 📊`](/MainFolder/info/6.md)   |
| [`🐳 INSTALACIÓN DE DOCKER Y DOCKER COMPOSE 🐳`](/MainFolder/info/3.md) | [`🔐 CONFIGURACIÓN DE HTTPS CON CADDY 🔐`](/MainFolder/info/7.md) |
| [`🎬 DESPLIEGUE DE JELLYFIN 🎬`](/MainFolder/info/4.md)                 | [`🔔 ALERTAS AUTOMÁTICAS POR TELEGRAM 🔔`](/MainFolder/info/8.md) |
| [`📁 INTEGRACIÓN DE SAMBA PARA ARCHIVOS MULTIMEDIA 📁`](/MainFolder/info/9.md) |                                                              |

</div>




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



