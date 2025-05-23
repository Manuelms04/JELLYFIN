<h1 align="center">DuckDNS</h1>

- DuckDNS es la herramienta que permite que el servidor multimedia montado en la máquina virtual sea accesible desde cualquier lugar del mundo, a través de Internet, usando un nombre de dominio personalizado

---

### *¿Por qué se usa DuckDNS en este trabajo?*

- `ACCESO REMOTO SENCILLO AL SERVIDOR`
    - DuckDNS permite que se pueda acceder al servidor Jellyfin (y también a Grafana o Prometheus si lo necesitas) desde fuera de tu red local, usando un nombre de dominio como mi-servidor.duckdns.org en lugar de memorizar una IP pública.

- `EVITA PROBLEMAS CON IPS DINÁMICAS`
    - Muchas conexiones domésticas (como las de Movistar, Orange, etc.) cambian la IP pública cada cierto tiempo. DuckDNS soluciona esto actualizando automáticamente el dominio cada vez que cambie la IP.

- `SOLUCIÓN GRATUITA Y LIGERA`
    - A diferencia de otros servicios de DNS dinámico (como No-IP o DynDNS), DuckDNS es totalmente gratuito, fácil de usar, y funciona perfectamente para este tipo de proyectos personales o educativos.

- `INTEGRACIÓN SIMPLE CON LINUX`
    - Solo necesitas un pequeño script (duck.sh) y una entrada en el crontab para que el sistema actualice la dirección IP cada 5 minutos automáticamente. Esto garantiza que tu dominio siempre apunte a tu servidor.

- `IDEAL PARA PROYECTOS AUTOALOJADOS`
    - Si estás montando servicios que deben ser accesibles remotamente, como un servidor multimedia (Jellyfin), usar DuckDNS te permite compartir el contenido con otros sin complicaciones técnicas

---
 
<p align="center">
  <img src="/MainFolder/img/duck.png" alt="DuckDNS" width="750" height="200">
</p>

