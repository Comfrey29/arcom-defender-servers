# ArCom Defender – Cliente

🛡️ Descripción

ArCom Defender es un sistema de protección integral para servidores, diseñado para detectar y bloquear malware, scripts maliciosos, intentos de phishing, DDoS y actividades sospechosas.

Incluye:

Monitorización de archivos y directorios (file_monitor.py)

Reglas YARA (yara_rules.yar)

Políticas de seguridad (policy.json)

Firewall y limitación de tasa (nftables.rules)

WAF para Nginx con ModSecurity (modsecurity.conf)

Protección con Fail2Ban (fail2ban/)

Directorio de cuarentena (quarantine/)

Actualizador automático (updater.py)

📁 Estructura del proyecto
arcom-defender/
├─ file_monitor.py
├─ updater.py
├─ setup.sh
├─ requirements.txt
├─ policy.json
├─ yara_rules.yar
├─ nftables.rules
├─ modsecurity.conf
├─ fail2ban/
│   ├─ filters.d/arcom-php.conf
│   └─ jail.d/arcom-jail.conf
├─ quarantine/
└─ README.md

🔹 Instalación inicial
sudo ./setup.sh


Verifica Python 3 y lo instala si falta

Crea quarantine/

Instala dependencias Python

Opcionalmente instala Nginx y Fail2Ban

Aplica reglas de firewall (nftables.rules)

Configura ModSecurity y Fail2Ban

🔹 Comprobación de actualizaciones
python3 updater.py


Compara la versión local (version.txt) con la versión remota

Descarga archivos nuevos si hay actualización

Hace backup de los archivos anteriores

Actualiza version.txt

🔹 Ejecución del monitor
python3 file_monitor.py


Vigila archivos y directorios críticos

Aplica reglas YARA

Aplica limitación de tasa y protecciones del firewall

Mueve archivos sospechosos a quarantine/

Envía alertas al servidor central (opcional)

🔹 Integración con WAF y Fail2Ban

ModSecurity protege Nginx de ataques web (SQLi, XSS, exploits)

Fail2Ban bloquea IPs sospechosas

El monitor complementa estas protecciones detectando actividad maliciosa adicional

🔹 Flujo resumido
[setup.sh] --> [updater.py] --> [file_monitor.py]
      |                 |             |
      |                 |             +--> Vigila archivos y directorios
      |                 |             +--> Aplica reglas YARA
      |                 |             +--> Mueve archivos sospechosos a quarantine
      |                 |             +--> Envía alertas al servidor
      |                 |
      +--> Instala paquetes y dependencias
      +--> Configura firewall, WAF y Fail2Ban

🔹 Buenas prácticas

Mantener policy.json y yara_rules.yar actualizados

Revisar periódicamente los archivos en quarantine/

Ejecutar updater.py regularmente

Solo desplegar el cliente en servidores propios o con permiso explícito
