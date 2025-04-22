## DuckDNS

- DuckDNS es la herramienta que permite que el servidor multimedia montado en la máquina virtual sea accesible desde cualquier lugar del mundo, a través de Internet, usando un nombre de dominio personalizado

---

### *¿Por qué se usa DuckDNS en este trabajo?*

- `Acceso remoto sencillo al servidor`
    - DuckDNS permite que puedas acceder al servidor Jellyfin (y también a Grafana o Prometheus si lo necesitas) desde fuera de tu red local, usando un nombre de dominio como mi-servidor.duckdns.org en lugar de memorizar u        na IP pública.

- `Evita problemas con IPs dinámicas`
    - Muchas conexiones domésticas (como las de Movistar, Orange, etc.) cambian la IP pública cada cierto tiempo. DuckDNS soluciona esto actualizando automáticamente el dominio cada vez que tu IP cambia.

- `Solución gratuita y ligera`
    - A diferencia de otros servicios de DNS dinámico (como No-IP o DynDNS), DuckDNS es totalmente gratuito, fácil de usar, y funciona perfectamente para este tipo de proyectos personales o educativos.

- `Integración simple con Linux`
    - Solo necesitas un pequeño script (duck.sh) y una entrada en el crontab para que el sistema actualice tu dirección IP cada 5 minutos automáticamente. Esto garantiza que tu dominio siempre apunte a tu servidor.

- `Ideal para proyectos autoalojados`
    - Si estás montando servicios que deben ser accesibles remotamente, como un servidor multimedia (Jellyfin), usar DuckDNS te permite compartir el contenido con otros sin complicaciones técnicas

---
 
![DuckDNS](/MainFolder/img/ddns.png)
