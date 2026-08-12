# Laboratorio SOC: Detecciones en Splunk y Análisis de Tráfico en Wireshark

## 1. Detección de Evasión y Modificación de Cuentas en Splunk (SPL)

### Contexto de Análisis
Al auditar intentos de creación de usuarios locales o escalado de privilegios, basar la alerta únicamente en el `EventID 4720` (Cuenta creada) genera puntos ciegos. Un atacante que agrega un usuario a un grupo administrador (`net localgroup administrators  /add`) genera un `EventID 4732`.

Para mitigar esto, se audita la línea de comandos completa (`CommandLine`) en el **EventID 4688** (Creación de proceso) o **Sysmon Event ID 1**.

### Regla de Búsqueda (SPL)
Detección de ejecución de PowerShell con técnicas de ocultación de consola y bypass de políticas:

\`\`\`spl
index=windows sourcetype="WinEventLog:Security" EventCode=4688
| search CommandLine="*-ExecutionPolicy Bypass*" OR CommandLine="*-WindowStyle Hidden*"
| table _time, host, AccountName, NewProcessName, CommandLine
| sort -_time
\`\`\`

---

## 2. Matriz de Análisis de Tráfico en Wireshark (TCP Flags)

Durante la fase de reconocimiento (Port Scanning con herramientas como Nmap), la identificación del estado de los puertos en el objetivo depende de las respuestas del protocolo TCP:

| Estado del Puerto | Respuesta en Wireshark | Comportamiento del Objetivo |
| :--- | :--- | :--- |
| **Abierto (Open)** | `[SYN, ACK]` | Servicio escuchando. El servidor acepta la conexión. |
| **Cerrado (Closed)** | `[RST, ACK]` | Equipo encendido, sin servicio en ese puerto (conexión rechazada). |
| **Filtrado (Filtered)** | `TCP Retransmission` / `ICMP Unreachable` | Un Firewall/IPS descarta el paquete (`DROP`) o lo bloquea explícitamente. |

> **Filtro de visualización clave en Wireshark:**
> `tcp.flags.syn == 1 and tcp.flags.ack == 1` (Muestra respuestas de puertos abiertos).
