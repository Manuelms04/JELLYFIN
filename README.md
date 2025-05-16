<h1 align="center">🎓 TFG ASIR 🎓</h1>
<h1 align="center"> IMPLEMENTACIÓN DE UN SERVIDOR MULTIMEDIA CON JELLYFIN </h1>


---


<h2 align="center"> 📘 Introducción 📘 </h2>


En el presente Trabajo de Fin de Grado del ciclo de Administración de Sistemas Informáticos en Red (ASIR), he diseñado e implementado un sistema completo para el despliegue y gestión de un servidor multimedia empleando Jellyfin como núcleo principal. El sistema ha sido construido en una máquina virtual Debian, y tiene como finalidad permitir la visualización, carga y administración de contenido multimedia desde cualquier dispositivo, tanto en red local como de manera remota a través de Internet.


Para lograr esto, se han integrado varias tecnologías complementarias:

- `Docker` y `Docker Compose` para facilitar el despliegue y mantenimiento de los servicios

- `DuckDNS` y `Caddy` para permitir acceso remoto seguro mediante HTTPS

- `Prometheus` y `Grafana` para la monitorización activa del sistema

- `Telegram` como canal de notificación de alertas

- `SAMBA` para compartir carpetas entre el servidor y otros equipos de la red


Este proyecto no solo cumple con los objetivos de integración y automatización de servicios, sino que también pone en práctica los conocimientos adquiridos durante el ciclo, abarcando áreas fundamentales como virtualización, redes, administración de sistemas, automatización, contenedores y servicios en la nube.



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
  - `80 y 443` → HTTPS *(Caddy)*
 

---

<h2 align="center"> 🗺️ Mapa Conceptual 🗺️ </h2>

<p align="center">
  <img src="/MainFolder/img/mapa.png" alt="MAPA" width="900" height="450">
</p>

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


<h2 align="center"> 🧠 Conclusión 🧠 </h2>

- Este proyecto representa la integración real de múltiples tecnologías y competencias clave del ciclo ASIR, en un entorno moderno, escalable y completamente funcional. Permite al usuario disfrutar de una experiencia multimedia rica, mientras mantiene control total sobre el estado del sistema, incluso de forma remota

- Además, este trabajo demuestra cómo se pueden implementar soluciones avanzadas sin depender de licencias comerciales ni grandes infraestructuras, únicamente con software libre, contenedores y servicios en la nube. La estructura modular permite ampliar el sistema en el futuro, añadiendo funcionalidades como autenticación, transcodificación o copias de seguridad automáticas


---


<h2 align="center"> 🧱 Desafíos Encontrados 🧱 </h2>

*Durante la realización del proyecto se presentaron varios desafíos que requirieron análisis, pruebas y adaptaciones para poder avanzar con éxito. A continuación, se detallan los principales:*

- `CONFIGURACIÓN DE RED Y ACCESO EXTERNO SEGURO`
    - Uno de los principales retos fue lograr que el servidor Jellyfin fuera accesible desde el exterior sin comprometer la seguridad. La combinación de DuckDNS (DNS dinámico) y Caddy (proxy inverso con HTTPS automático) implicó entender bien el funcionamiento de los certificados SSL, redireccionamientos y puertos necesarios

- `INTEGRACIÓN DE MÚLTIPLES SERVICIOS EN UN ÚNICO DOCKER-COMPOSE.YML`
    - Coordinar diferentes servicios (Jellyfin, Prometheus, Grafana, Caddy, etc.) dentro del mismo archivo docker-compose.yml exigió gestionar correctamente volúmenes, redes internas, y dependencias entre contenedores. Fue clave mantener un orden claro para evitar conflictos

- `PERMISOS DE CARPETAS COMPARTIDAS CON SAMBA`
    - Configurar Samba para que permitiera escritura desde otros equipos y a la vez mantener la seguridad del sistema fue complejo. Requirió ajustar permisos de usuario, máscaras de creación (create mask y directory mask) y validar el acceso desde diferentes sistemas operativos
    
- `MONITORIZACIÓN PERSONALIZADA CON PROMETHEUS Y GRAFANA`
    - No fue suficiente con instalar Prometheus y Grafana, hubo que aprender a configurar correctamente los exporters, definir el archivo prometheus.yml y crear dashboards en Grafana que mostrarán información útil. También fue un desafío hacer que Grafana enviará alertas a Telegram correctamente


- `ACTUALIZACIÓN AUTOMÁTICA DE LA IP PÚBLICA CON DUCKDNS`
    - Al trabajar con una IP dinámica, se implementó un script para actualizar la IP periódicamente. La programación de esta tarea en cron y su correcta ejecución supuso una curva de aprendizaje adicional

- `GESTIÓN DE ERRORES Y PRUEBAS DE FIABILIDAD`
    - Se realizaron pruebas forzadas de fallo (apagado de contenedores, consumo excesivo de recursos, caídas de red) para verificar que los sistemas de monitorización y alerta funcionaban correctamente. Esto permitió ajustar los umbrales de alertas y garantizar la estabilidad del sistema


---


<h2 align="center"> 🔗 Referencias 🔗 </h2>


- [METADATOS 1 (musica)](https://musicbrainz.org/)
- [METADATOS 2 (musica)](https://www.theaudiodb.com/)
- [PROM + GRAF](https://youtu.be/dtscyg03kII?feature=shared)
- [DuckDNS / SSL](https://youtu.be/GO9Ji7Nslj0?feature=shared)


---


<h2 align="center"> 🧾 Autor 🧾 </h2>

- *Autor:*
  - [`MANUEL MORENO SOSA`](https://github.com/Manuelms04)
- *Curso:*
  - `2º ASIR`
- *Centro:*
  - `IES Rodrigo Caro`
- *Fecha:*
  - `Junio 2025`


