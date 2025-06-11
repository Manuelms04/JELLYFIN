<h1 align="center">JELLYFIN</h1>

- Jellyfin es la pieza central de este proyecto. Se trata de un servidor multimedia **libre, gratuito y de código abierto** que permite organizar, gestionar y reproducir contenido desde cualquier dispositivo dentro o fuera de la red local

---

## Ventajas de Jellyfin

- `SOFTWARE 100% LIBRE Y SIN RESTRICCIONES`
    - A diferencia de otras opciones como Plex o Emby, Jellyfin no requiere suscripciones ni cuentas. No tiene funciones bloqueadas ni recopila datos de los usuarios

- `ORGANIZACIÓN AUTOMÁTICA DEL CONTENIDO MULTIMEDIA`
    - Escanea las carpetas configuradas, descarga automáticamente carátulas, nombres de capítulos, metadatos, etc. Todo se presenta en una interfaz atractiva

- `COMPATIBLE CON MÚLTIPLES DISPOSITIVOS`
    - Existen clientes para Android, iOS, navegadores, Smart TVs, y más. También puede reproducirse directamente desde cualquier navegador web

- `FÁCIL DESPLIEGUE CON DOCKER`
    - Se instala y ejecuta dentro de un contenedor Docker, facilitando la configuración, portabilidad y escalabilidad del servicio
      
- `PRIVACIDAD Y CONTROL TOTAL`
    - Todo el sistema es autoalojado. El usuario tiene control completo sobre los archivos, configuración, acceso y seguridad

---

##  Papel de Jellyfin en el Proyecto

- En este Proyecto, `Jellyfin` se implementa como servidor multimedia dentro de una máquina virtual `Debian`. Desplegado mediante `Docker`, permite gestionar y transmitir contenidos como series, películas o música, organizados automáticamente con metadatos obtenidos de Internet

- Se combina con `Prometheus` y `Grafana` para la monitorización y visualización de su rendimiento, y con `DuckDNS` para habilitar el acceso remoto seguro mediante `DNS dinámico`. Esta arquitectura reproduce un entorno real de producción, fomentando habilidades clave como virtualización, contenedores, servicios en red, autoalojamiento y gestión de sistemas

> Con esta infraestructura, se logra un **sistema multimedia completo, profesional y autoalojado**, ideal como entorno de aprendizaje técnico 

---

Se puede encontrar la configuración de Docker en el archivo `docker-compose.yml` en el `Paso 2` del apartado de [`🎬 DESPLIEGUE DE JELLYFIN 🎬`](https://github.com/Manuelms04/JELLYFIN/blob/main/MainFolder/info/4.md#paso-2-definir-los-servicios-en-el-archivo-docker-composeyml) del proyecto

---

<p align="center">
  <img src="/MainFolder/img/jelly.png" alt="JELLYFIN" width="800" height="425">
</p>


