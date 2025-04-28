<h1 align="center">CADDY SERVER</h1>

- Caddy es un servidor web moderno y automatizado que facilita la configuración y gestión de sitios web, especialmente en entornos de contenedores. Su principal ventaja es la obtención automática de certificados SSL y su facilidad de uso para servir contenido web.

---

### *¿Por qué se usa Caddy en este trabajo?*

- Configuración automática de HTTPS
    - Caddy gestiona automáticamente los certificados SSL a través de Let's Encrypt, lo que asegura que todas las conexiones sean seguras sin necesidad de intervención manual. Esto es ideal para entornos donde la seguridad es una prioridad, como con servidores multimedia.

- Configuración mínima y sencilla
    - Con Caddy, no es necesario configurar de forma extensa el servidor web. Su archivo de configuración (`Caddyfile`) es extremadamente sencillo y permite definir reglas de reescritura de URL y proxy reverso de forma muy intuitiva.

- Integración con Docker
    - Caddy se integra perfectamente con Docker, lo que permite desplegarlo en contenedores sin complicaciones. Se puede configurar para que gestione el tráfico web de otros contenedores, como un servidor de Jellyfin, asegurando conexiones HTTPS sin esfuerzo adicional.

- Reverse Proxy avanzado
    - Con su funcionalidad de proxy inverso, Caddy puede redirigir el tráfico entrante a otros servicios como Jellyfin, asegurando que los usuarios puedan acceder al contenido de forma segura desde cualquier lugar.

- Acceso web desde cualquier dispositivo
    - Al estar configurado en Docker, Caddy se puede acceder desde cualquier navegador utilizando el dominio configurado (por ejemplo, https://manuelms.duckdns.org), lo que facilita su uso en una red local o externa (si se configura con DuckDNS).

- Certificados SSL sin necesidad de configuración manual
    - Caddy solicita y renueva automáticamente los certificados SSL de Let's Encrypt para el dominio configurado. Esto ahorra tiempo y garantiza que el sitio esté siempre protegido con HTTPS.

---

<p align="center">
  <img src="/MainFolder/img/caddy.png" alt="CADDY" width="800" height="200">
</p>
