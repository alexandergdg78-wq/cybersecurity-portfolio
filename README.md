# Cybersecurity Portfolio – Matías García

## 🇪🇸 Sobre mí
Aspirante a Analista de Ciberseguridad (SOC).  
Formación práctica en análisis de logs, escaneo de vulnerabilidades y detección de amenazas.  
Interesado en Blue Team y monitoreo de seguridad.

## 🇬🇧 About me
Aspiring Junior Cybersecurity Analyst focused on SOC operations, log analysis and threat detection.  
Hands-on practice with security tools.

---

## 🔧 Habilidades / Skills
- Networking básico / Networking fundamentals  
- Linux / Windows  
- Análisis de logs / Log analysis  
- Seguridad básica / Security fundamentals  
- SOC concepts  
- Nmap  
- Threat detection basics  

---

## 🧪 Proyectos / Projects
📂 nmap-scan  
📂 ssh-log-analysis  
📂 malware-analysis  

---

## 🎯 Objetivo profesional / Career Goal
Conseguir mi primer empleo como Analista de Ciberseguridad Junior (SOC).  
Seeking first role as Junior SOC Analyst.
🛠️ Lab 01: Gestión de Permisos y Mínimo Privilegio (Linux)
Objetivo: Simular la protección de datos sensibles en un entorno de infraestructura para pagos.

Acción: Creación de un archivo de datos confidenciales y restricción total de permisos mediante chmod 000.

Resultado: Se verificó el bloqueo del sistema ante intentos de lectura no autorizados (Permission denied).

Concepto aplicado: Principio de Mínimo Privilegio (PoLP).


### 🛡️ Laboratorio de Análisis de Seguridad (SOC)
*Prácticas enfocadas en la defensa y auditoría de sistemas Linux.*
### 🔬 Lab 02: Triaje de Amenazas y Análisis de Reputación (VirusTotal)

**Objetivo:** Realizar el triaje y enriquecimiento de una alerta de seguridad sospechosa en un endpoint.
**Escenario:** Se recibe una alerta en el SIEM detectando la ejecución de un archivo desconocido. Se utiliza el Hash para investigar su naturaleza sin ejecutarlo localmente.
**Resultado:** Se confirma la detección como *True Positive* correspondiente a un Ransomware (WannaCry).

**Mapeo framework MITRE ATT&CK:**
| Táctica (Tactic) | Técnica (Technique) | Descripción de la Amenaza |
| :--- | :--- | :--- |
| **Impact (TA0040)** | **Data Encrypted for Impact (T1486)** | El malware busca cifrar los datos del usuario para interrumpir la disponibilidad del sistema. |

**Acción de Contención:**
Aislamiento inmediato del host afectado de la red corporativa y bloqueo del Hash en el EDR.

**Evidencias:**
![Detección de Amenaza en VirusTotal](virustotal_deteccion.png)

### 🌐 Lab 04: Análisis Avanzado de Phishing con Cadenas de Redirección

**Objetivo:** Investigar un incidente de Phishing complejo para identificar técnicas de evasión y anomalías geográficas.
**Escenario:** Triaje manual de una URL sospechosa (`www.1wins365.online`). El analista detecta un comportamiento anómalo que las herramientas automáticas pasaron por alto.
**Resultado:** Se confirma un *True Positive* de Phishing de alto nivel, utilizando redirecciones múltiples para ocultar la infraestructura maliciosa.

**Nuevos Indicadores Técnicos y Anomalías Identificadas:**
1. **Cadena de Redirección Sospechosa:** El atacante usa redirecciones complejas (HTTP -> HTTPS -> subdirectorio `/m/`) para evadir sistemas de detección automáticos.
2. **Geografía Identificada:** Origen de la solicitud en Reino Unido (GB) escaneado desde Finlandia (FI), una combinación inusual para la supuesta marca objetivo.
3. **Aspecto Visual Deceptivo:** El clon de la página final imita perfectamente a un sitio de apuestas legítimo ('1Win') para engañar a la víctima.

**Mapeo framework MITRE ATT&CK:**
| Táctica (Tactic) | Técnica (Technique) | Descripción de la Amenaza |
| :--- | :--- | :--- |
| **Initial Access (TA0001)** | **Phishing: Spearphishing Link (T1566.002)** | Uso de enlaces engañosos en campañas de Phishing masivas. |
| **Command and Control (TA0011)** | **Application Layer Protocol: Web Protocols (T1071.001)** | Uso de protocolos web estándar (HTTP/S) y redirecciones complejas para ocultar el C2. |

**Evidencias:**

![Análisis Técnico de Cadena de Redirección](Captura%20de%20pantalla%20(71).png) 



### 🛡️ Lab 05: Inteligencia de Amenazas (CTI) y Triaje de IPs

**Objetivo:** Analizar la reputación de direcciones IP sospechosas utilizando bases de datos de Inteligencia de Amenazas (OSINT).
**Escenario:** Durante el monitoreo de red, se detectan múltiples intentos de conexión desde una IP externa (`198.23.210.153`). El analista debe determinar si es tráfico legítimo o infraestructura atacante.
**Resultado:** Se clasifica la IP en la "Zona Gris" (56% de Confianza de Abuso), requiriendo revisión manual y bloqueo preventivo en el Firewall. Se identifica que la IP pertenece a un Data Center, ocultando el origen real del atacante.

**Indicadores de Compromiso (IoCs) Identificados:**
1. **Dirección IP:** `198.23.210.153`
2. **Geolocalización:** Buffalo, New York (EE.UU.) - Uso estratégico de servidores norteamericanos para evadir bloqueos por geolocalización (Geo-blocking).
3. **ISP y Tipo de Uso:** `HostPapa` (Data Center / Web Hosting). Confirmación de que es un servidor alquilado para lanzar ataques automatizados, no una red residencial.
4. **Hostname Sospechoso:** `incubus.globalgoldplated.com`

**Mapeo framework MITRE ATT&CK:**
| Táctica (Tactic) | Técnica (Technique) | Descripción de la Amenaza |
| :--- | :--- | :--- |
| **Resource Development (TA0042)** | **Acquire Infrastructure: Virtual Private Server (T1583.003)** | El atacante alquila servidores en Data Centers comerciales (ej. HostPapa) para lanzar ataques de forma anónima. |
| **Reconnaissance (TA0043)** | **Active Scanning (T1595)** | Escaneo de puertos y fuerza bruta lanzados desde la infraestructura comprometida. |

**Evidencias:**

![Triaje de IP en AbuseIPDB](Captura%20de%20pantalla%20(77).png)




# 💻 Lab 06: Triaje de Registros de Seguridad (Windows Event Logs)

## 🎯 Objetivo del Laboratorio
Demostrar la capacidad de realizar un análisis de Nivel 1 (Tier 1) sobre eventos de seguridad en Windows, aislando falsos positivos mediante el filtrado de Event IDs y ejecutando forensia básica para determinar la legitimidad de las conexiones.

## 🛠️ Herramienta Utilizada
* Visor de Eventos de Windows (Windows Event Viewer)

## 📝 Desarrollo del Análisis

**1. Filtrado de Ruido (Aislamiento de Eventos)**
El sistema operativo presentaba inicialmente un volumen superior a los 23.000 registros de seguridad. Para identificar accesos al equipo, apliqué un filtro aislando exclusivamente el **Event ID 4624** (Inicio de sesión exitoso). Esta acción redujo el "ruido" a una muestra manejable de ~5.200 eventos relevantes.

**2. Forensia Básica (Extracción de Atributos)**
En el SOC, confirmar un acceso exitoso no es suficiente; es imperativo saber *cómo* se accedió. Al analizar la información detallada de un evento 4624 específico, ubiqué el parámetro crítico de investigación: el **Tipo de inicio de sesión (Logon Type)**.
* *Resultado hallado:* Tipo 5.

**3. Criterio Analítico y Resolución**
Un *Logon Type 5* (Service Logon) indica que la conexión no fue interactiva (realizada por un humano frente a la pantalla o vía red), sino que fue ejecutada por un componente interno o servicio de Windows operando en segundo plano.
* **Veredicto Analítico:** Falso Positivo / Comportamiento Legítimo del sistema operativo. Incidente cerrado sin necesidad de escalamiento.
<img width="1366" height="768" alt="Captura de pantalla (79)" src="https://github.com/user-attachments/assets/703c035a-75c4-4858-8c8a-ad4f171ae60b" />


* [Análisis Forense de Cabeceras de Correo: Identificación de Falso Positivo (Phishing Triage)](analisis-phishing-osde.md)

* [Análisis de Logs de Firewall: Detección y Contención de Escaneo de Puertos](analisis-firewall-reconocimiento.md)

* * [Análisis de Ejecución Anómala: Detección de Fileless Malware vía PowerShell](analisis-fileless-powershell.md)

* [Análisis y Triaje de Incidente Crítico: Detección y Contención de Ransomware] analisis-ransomware-contencion.md  


























**Actividad reciente:** Auditoría forense en vivo y enumeración de sistemas.
*   **Enumeración:** Identificación de usuarios del sistema mediante `/etc/passwd`.
*   **Análisis de Procesos:** Monitoreo de recursos y servicios críticos (`ssm-agent`, `systemd-journald`) usando `ps aux`.
*   **Objetivo:** Establecimiento de líneas base (baseline) de seguridad y detección de anomalías en entornos de producción.

![Análisis de procesos Linux](Captura%20de%20pantalla%20(32).png)
