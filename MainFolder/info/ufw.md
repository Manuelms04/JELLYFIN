<h1 align="center">UFW</h1>

- UFW es una herramienta que facilita la configuración de un firewall en sistemas Linux, proporcionando una capa adicional de seguridad para el servidor multimedia y otros servicios desplegados en la máquina virtual

---

### *¿Por qué se usa UFW en este trabajo?*

- `PROTECCIÓN DEL SERVIDOR`
    - UFW ayuda a proteger el servidor Jellyfin y los demás servicios (Grafana, Prometheus, etc.) restringiendo el acceso solo a los puertos y direcciones IP necesarias, evitando accesos no autorizados

- `CONFIGURACIÓN SIMPLE Y CLARA`
    - Ofrece comandos sencillos para permitir o denegar tráfico en los puertos utilizados, lo que facilita la gestión del firewall incluso para usuarios con poca experiencia en seguridad de red

- `MEJORA DE LA SEGURIDAD EN ACCESO REMOTO`
    - Al combinarse con DuckDNS para acceso remoto, UFW asegura que solo las conexiones legítimas a los puertos 80, 443 u otros configurados estén abiertas, reduciendo el riesgo de ataques externos

- `CONTROL DEL TRÁFICO`
    - Permite definir reglas específicas para distintos servicios y protocolos, asegurando que cada contenedor Docker o servicio del proyecto tenga solo los accesos estrictamente necesarios

- `INTEGRACIÓN NATIVA CON SISTEMAS LINUX`
    - UFW se integra perfectamente con el sistema operativo de la máquina virtual, funcionando como una interfaz amigable sobre iptables sin necesidad de configuraciones complejas

---

<p align="center">
  <img src="/MainFolder/img/ufw.jpg" alt="UFW Firewall" width="600" height="300">
</p>

