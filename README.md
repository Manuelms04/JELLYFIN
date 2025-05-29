<h1 align="center">🎓 TFG ASIR 🎓</h1>
<h1 align="center"> IMPLEMENTACIÓN DE UN SERVIDOR MULTIMEDIA CON JELLYFIN </h1>


---


&nbsp;

<h2 align="center"> 📘 Introducción 📘 </h2>


En el presente Trabajo de Fin de Grado del ciclo de ASIR, he diseñado e implementado un sistema completo para el despliegue y gestión de un servidor multimedia empleando [`JELLYFIN`](/MainFolder/info/jelly.md) como núcleo principal. El sistema ha sido construido en una máquina virtual Debian, y tiene como finalidad permitir la visualización, carga y administración de contenido multimedia desde cualquier dispositivo, tanto en red local como de manera remota a través de Internet


*Para lograr esto, se han integrado varias tecnologías complementarias:*

- [`UFW`](/MainFolder/info/ufw.md) para controlar el firewall y proteger el acceso a los servicios del servidor

- [`DOCKER`](/MainFolder/info/docker.md) y [`DOCKER COMPOSE`](/MainFolder/info/docker.md) para facilitar el despliegue y mantenimiento de los servicios

- [`DUCKDNS`](/MainFolder/info/ddns.md) para proporcionar un nombre de dominio dinámico accesible desde el exterior

- [`PROMETHEUS`](/MainFolder/info/pro.md) y [`GRAFANA`](/MainFolder/info/graf.md) para la monitorización activa del sistema

- [`TELEGRAM`](/MainFolder/info/tele.md) como canal de notificación de alertas

- [`SAMBA`](/MainFolder/info/samba.md) para compartir carpetas entre el servidor y otros equipos de la red

&nbsp;

> Este proyecto no solo cumple con los objetivos de integración y automatización de servicios, sino que también pone en práctica los conocimientos adquiridos durante el ciclo, abarcando áreas fundamentales como virtualización, redes, administración de sistemas, automatización, contenedores y servicios en la nube

&nbsp;


---

&nbsp;


<h2 align="center"> 🎯 Objetivos del proyecto 🎯 </h2>

*Los principales objetivos de este trabajo son:*

- Montar un servidor multimedia con [`JELLYFIN`](/MainFolder/info/jelly.md), capaz de gestionar bibliotecas audiovisuales y permitir la reproducción desde múltiples dispositivos

- Facilitar el acceso al contenido desde cualquier lugar, mediante el uso de [`DUCKDNS`](/MainFolder/info/ddns.md) para mantener actualizado el nombre de dominio frente a cambios en la IP pública
  
- Implementar el sistema sobre [`DOCKER`](/MainFolder/info/docker.md), permitiendo que todos los servicios estén contenedorizados y centralizados mediante [`DOCKER-COMPOSE.YML`](/MainFolder/info/docker.md)

- Incorporar herramientas de monitorización como [`PROMETHEUS`](/MainFolder/info/pro.md) y [`GRAFANA`](/MainFolder/info/graf.md), para supervisar el estado del servidor y sus recursos

- Enviar alertas automáticas a [`TELEGRAM`](/MainFolder/info/tele.md), con el fin de detectar y responder ante fallos o comportamientos anómalos

- Permitir la carga de contenido desde la red local, gracias a la integración de [`SAMBA`](/MainFolder/info/samba.md) como servicio de compartición de carpetas

- Aplicar técnicas de automatización, como el uso de scripts para mantener actualizada la IP pública, tareas programadas con [`CRON`](https://crontab.cronhub.io/), y gestión básica de firewall con [`UFW`](/MainFolder/info/ufw.md)

&nbsp;


---

&nbsp;


<h2 align="center"> 🗺️ Mapa Conceptual 🗺️ </h2>

<p align="center">
  <img src="/MainFolder/img/mapa.png" alt="MAPA" width="900" height="450">
</p>

&nbsp;


---

&nbsp;


<h2 align="center"> 💻 Software Implementado 💻 </h2>

<div align="center">
  <table>
    <tr>
      <td><a href="/MainFolder/info/jelly.md"> JELLYFIN </a></td>
      <td><a href="/MainFolder/info/ufw.md"> UFW </a></td>
      <td><a href="/MainFolder/info/ddns.md"> DUCKDNS </a></td>
      <td><a href="/MainFolder/info/docker.md"> DOCKER </a></td>
    </tr>
    <tr>
      <td><a href="/MainFolder/info/pro.md"> PROMETHEUS </a></td>
      <td><a href="/MainFolder/info/graf.md"> GRAFANA </a></td>
      <td><a href="/MainFolder/info/tele.md"> TELEGRAM </a></td>
      <td><a href="/MainFolder/info/samba.md"> SAMBA </a></td>
    </tr>
  </table>
</div>

 &nbsp;


---

&nbsp;

<h2 align="center">✅ Requisitos ✅</h2>

- **Imagen ISO de Debian 12**
- **Máquina Virtual configurada con:**
  - 3 CPU
  - 8 GB de RAM
  - 80 GB de disco duro *(preferiblemente dinámico)*
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
  - `80 y 443` → Puertos para acceso web remoto 
 
&nbsp;

---

&nbsp;

<h2 align="center"> 📋 Índice de Instalación Paso a Paso 📋 </h2>

> [`🔧 PREPARACIÓN DEL SISTEMA OPERATIVO DEBIAN 🔧`](/MainFolder/info/1.md)

> [`🌍 CONFIGURACIÓN DE DUCKDNS 🌍`](/MainFolder/info/2.md)

> [`🐳 INSTALACIÓN DE DOCKER Y DOCKER COMPOSE 🐳`](/MainFolder/info/3.md)

> [`🎬 DESPLIEGUE DE JELLYFIN 🎬 `](/MainFolder/info/4.md)

> [`📈 CONFIGURACIÓN DE PROMETHEUS 📈`](/MainFolder/info/5.md)

> [`📊 CONFIGURACIÓN DE GRAFANA 📊`](/MainFolder/info/6.md)

> [`🔔 ALERTAS AUTOMÁTICAS POR TELEGRAM 🔔`](/MainFolder/info/8.md)

> [`📁 INTEGRACIÓN DE SAMBA PARA ARCHIVOS MULTIMEDIA 📁`](/MainFolder/info/9.md)

&nbsp;

---

&nbsp;

<h2 align="center"> 🧠 Conclusión 🧠 </h2>

- Este proyecto representa la integración real de múltiples tecnologías y competencias clave del ciclo ASIR, en un entorno moderno, escalable y completamente funcional. Permite al usuario disfrutar de una experiencia multimedia rica, mientras mantiene control total sobre el estado del sistema, incluso de forma remota

- Además, este trabajo demuestra cómo se pueden implementar soluciones avanzadas sin depender de licencias comerciales ni grandes infraestructuras, únicamente con software libre, contenedores y servicios en la nube. La estructura modular permite ampliar el sistema en el futuro, añadiendo funcionalidades como autenticación, transcodificación o copias de seguridad automáticas

&nbsp;

---

&nbsp;

<h2 align="center"> 🧱 Desafíos Encontrados 🧱 </h2>

*Durante la realización del proyecto se presentaron varios desafíos que requirieron análisis, pruebas y adaptaciones para poder avanzar con éxito. A continuación, se detallan los principales:*

- `CONFIGURACIÓN DE RED Y ACCESO EXTERNO SEGURO`
    - Uno de los principales retos fue lograr que el servidor Jellyfin fuera accesible desde el exterior sin comprometer la seguridad. La configuración del acceso remoto implicó comprender cómo gestionar dominios dinámicos con DuckDNS (DNS dinámico) configurar correctamente los puertos de redirección y garantizar el acceso al servidor sin comprometer la seguridad
      
- `INTEGRACIÓN DE MÚLTIPLES SERVICIOS EN UN ÚNICO DOCKER-COMPOSE.YML`
    - Coordinar diferentes servicios (Jellyfin, Prometheus, Grafana, etc.) dentro del mismo archivo docker-compose.yml exigió gestionar correctamente volúmenes, redes internas, y dependencias entre contenedores. Fue clave mantener un orden claro para evitar conflictos

- `PERMISOS DE CARPETAS COMPARTIDAS CON SAMBA`
    - Configurar Samba para que permitiera escritura desde otros equipos y a la vez mantener la seguridad del sistema fue complejo. Requirió ajustar permisos de usuario, máscaras de creación (create mask y directory mask) y validar el acceso desde diferentes sistemas operativos
    
- `MONITORIZACIÓN PERSONALIZADA CON PROMETHEUS Y GRAFANA`
    - No fue suficiente con instalar Prometheus y Grafana, hubo que aprender a configurar correctamente los exporters, definir el archivo prometheus.yml y crear dashboards en Grafana que mostrarán información útil. También fue un desafío hacer que Grafana enviará alertas a Telegram correctamente


- `ACTUALIZACIÓN AUTOMÁTICA DE LA IP PÚBLICA CON DUCKDNS`
    - Al trabajar con una IP dinámica, se implementó un script para actualizar la IP periódicamente. La programación de esta tarea en cron y su correcta ejecución supuso una curva de aprendizaje adicional

- `GESTIÓN DE ERRORES Y PRUEBAS DE FIABILIDAD`
    - Se realizaron pruebas forzadas de fallo (apagado de contenedores, consumo excesivo de recursos, caídas de red) para verificar que los sistemas de monitorización y alerta funcionaban correctamente. Esto permitió ajustar los umbrales de alertas y garantizar la estabilidad del sistema

&nbsp;

---

&nbsp;

<h2 align="center"> 🔗 Referencias 🔗 </h2>

- [Genbyte](https://genbyte.blogspot.com/)    
- [Jonatan Castro](https://www.jonatancastro.com/)
- [Human Technology](https://github.com/Human-Technology)
- [Duck DNS](https://www.duckdns.org/)
- [Grafana](https://grafana.com/)
- [Prometheus](https://prometheus.io/)

- [METADATOS 1 (musica)](https://musicbrainz.org/)
- [METADATOS 2 (musica)](https://www.theaudiodb.com/)
- [PROM + GRAF](https://youtu.be/dtscyg03kII?feature=shared)
- [DuckDNS / SSL](https://youtu.be/GO9Ji7Nslj0?feature=shared)
- [PLUGINGS](https://youtu.be/SLzBe9jhix4?feature=shared)

&nbsp;

---

&nbsp;

<h2 align="center"> 🧾 Autor 🧾 </h2>

- *Autor:*
  - [`MANUEL MORENO SOSA`](https://github.com/Manuelms04)
- *Curso:*
  - `2º ASIR`
- *Centro:*
  - `IES Rodrigo Caro`
- *Fecha:*
  - `Junio 2025`


