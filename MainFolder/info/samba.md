<h1 align="center">SAMBA</h1>

- Samba es el servicio que permite compartir carpetas entre el servidor multimedia y otros dispositivos conectados a la red local, facilitando la carga y el acceso a archivos multimedia de forma rápida y directa.

---

### *¿Por qué se usa Samba en este trabajo?*

- Compartición de archivos multimedia
    - Gracias a Samba, se puede compartir la carpeta que contiene películas, series o música entre la máquina virtual y cualquier otro dispositivo de la red, como un PC con Windows o una Smart TV.

- Acceso sencillo desde otros equipos
    - Cualquier equipo conectado a la misma red puede acceder a la carpeta compartida introduciendo `\\IP_DE_LA_MV\Media` en el explorador de archivos, haciendo más cómodo subir o gestionar contenido multimedia.

- Integración directa con Jellyfin
    - Al montar la carpeta compartida en el contenedor de Jellyfin, se permite que este acceda directamente a los archivos multimedia sin necesidad de moverlos manualmente al contenedor.

- Control de acceso por usuario
    - Samba permite definir usuarios autorizados, mejorando la seguridad del acceso a las carpetas compartidas dentro del entorno local.

- Fácil de instalar y configurar
    - Su instalación y configuración son rápidas, y se integran fácilmente con el resto de servicios del servidor desplegados mediante Docker.

---

<p align="center">
  <img src="/MainFolder/img/samba.png" alt="SAMBA" width="700" height="350">
</p>

