ArCom Defender – Cliente
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

🔹 1️⃣ Instalación inicial

Descargar todo el proyecto en el servidor o máquina local.

Ejecutar el script de instalación:

sudo ./setup.sh


El script:

Verifica si Python 3 está instalado y lo instala si es necesario

Crea el directorio quarantine/

Instala las dependencias Python

Instala opcionalmente Nginx y Fail2Ban

Aplica reglas de firewall (nftables.rules)

Configura ModSecurity y Fail2Ban

🔹 2️⃣ Comprobación de actualizaciones

Antes de ejecutar el monitor, es recomendable comprobar si hay actualizaciones:

python3 updater.py


Compara la versión local (version.txt) con la versión remota en el servidor central

Descarga automáticamente archivos nuevos si hay actualización

Hace backup de los archivos anteriores

Actualiza version.txt con la nueva versión

🔹 3️⃣ Ejecución del monitor

Para iniciar la protección del cliente:

python3 file_monitor.py


Carga la configuración de policy.json

Vigila archivos y directorios críticos

Aplica reglas YARA para detectar malware o scripts sospechosos

Aplica limitación de tasa y protecciones del firewall

Si detecta archivos sospechosos:

Los mueve a quarantine/

Envía alertas al servidor central (opcional)

🔹 4️⃣ Integración con WAF y Fail2Ban

ModSecurity protege Nginx de ataques web (SQLi, XSS, exploits)

Fail2Ban bloquea IPs sospechosas según filtros y jails

El cliente complementa estas protecciones detectando actividad maliciosa adicional

🔹 5️⃣ Uso diario

El monitor puede ejecutarse en segundo plano o como servicio (systemd)

Detecta y aísla automáticamente archivos sospechosos

Mantiene logs y cuarentena de los archivos detectados

Se puede actualizar periódicamente con updater.py

Permite que el administrador central envíe órdenes (por ejemplo disable)

🔹 6️⃣ Beneficios

Protege el servidor contra malware, phishing, DDoS y scripts maliciosos

Permite actualizaciones automáticas sin reinstalación manual

Mantiene un registro completo de detecciones y acciones

Integrable con un servidor central para monitorización y bloqueo global

🔹 7️⃣ Flujo resumido
[setup.sh] --> [updater.py] --> [file_monitor.py]
      |                 |             |
      |                 |             +--> Vigila archivos y directorios
      |                 |             +--> Aplica reglas YARA
      |                 |             +--> Mueve archivos sospechosos a quarantine
      |                 |             +--> Envía alertas al servidor
      |                 |
      +--> Instala paquetes y dependencias
      +--> Configura firewall, WAF y Fail2Ban

🔹 8️⃣ Buenas prácticas

Mantener policy.json y yara_rules.yar actualizados

Revisar periódicamente los archivos en quarantine/

Ejecutar updater.py regularmente

Solo desplegar el cliente en servidores propios o con permiso explícito
