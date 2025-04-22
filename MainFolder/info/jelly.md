## JELLYFIN

- Jellyfin es la pieza central de este proyecto. Se trata de un servidor multimedia **libre, gratuito y de código abierto** que permite organizar, gestionar y reproducir contenido desde cualquier dispositivo dentro o fuera de la red local. A continuación, se detallan las razones de su uso en este TFG:

---

### *Ventajas de Jellyfin*

- `Software 100% libre y sin restricciones`
    - A diferencia de otras opciones como Plex o Emby, Jellyfin no requiere suscripciones ni cuentas. No tiene funciones bloqueadas ni recopila datos de los usuarios.

- `Organización automática del contenido multimedia`
    - Escanea las carpetas configuradas, descarga automáticamente carátulas, sinopsis, nombres de capítulos, metadatos, etc. Todo se presenta en una interfaz atractiva.

- `Acceso desde red local o remotamente`
    - Gracias a la integración con DuckDNS, es posible acceder al servidor desde cualquier parte del mundo mediante un dominio personalizado.

- `Compatible con múltiples dispositivos`
    - Existen clientes para Android, iOS, navegadores, Smart TVs, y más. También puede reproducirse directamente desde cualquier navegador web.

- `Fácil despliegue con Docker`
    - Se instala y ejecuta dentro de un contenedor Docker, facilitando la configuración, portabilidad y escalabilidad del servicio.

- `Privacidad y control total`
    - Todo el sistema es autoalojado. El usuario tiene control completo sobre los archivos, configuración, acceso y seguridad.

---

##  Papel de Jellyfin en el TFG

> Jellyfin es el núcleo del proyecto. Todo el entorno se ha construido para alojarlo, supervisarlo y permitir su acceso remoto de forma segura.

- **Docker** → Despliegue rápido, aislado y reproducible.
- **Prometheus** → Recolección de métricas sobre su estado y uso.
- **Grafana** → Visualización de datos como uso de CPU, tráfico, etc.
- **DuckDNS** → Permite acceder a Jellyfin desde fuera de la red.

Con esta infraestructura, se logra un **sistema multimedia completo, profesional y autoalojado**, ideal como entorno de aprendizaje técnico.

---

##  Resumen técnico-académico

> En este Trabajo de Fin de Grado, Jellyfin se implementa como servidor multimedia dentro de una máquina virtual Debian. Desplegado mediante Docker, permite gestionar y transmitir contenidos como series, películas o música, organizados automáticamente con metadatos obtenidos de Internet.  

> Se combina con Prometheus y Grafana para la monitorización y visualización de su rendimiento, y con DuckDNS para habilitar el acceso remoto seguro mediante DNS dinámico. Esta arquitectura reproduce un entorno real de producción, fomentando habilidades clave como virtualización, contenedores, servicios en red, autoalojamiento y gestión de sistemas.

---

Puedes encontrar la configuración de Docker en el archivo `docker-compose.yml` del proyecto.

Asegúrate de tener configuradas correctamente las rutas de almacenamiento multimedia y las carpetas de configuración en tu contenedor.

