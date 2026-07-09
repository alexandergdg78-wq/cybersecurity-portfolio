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














**Actividad reciente:** Auditoría forense en vivo y enumeración de sistemas.
*   **Enumeración:** Identificación de usuarios del sistema mediante `/etc/passwd`.
*   **Análisis de Procesos:** Monitoreo de recursos y servicios críticos (`ssm-agent`, `systemd-journald`) usando `ps aux`.
*   **Objetivo:** Establecimiento de líneas base (baseline) de seguridad y detección de anomalías en entornos de producción.

![Análisis de procesos Linux](Captura%20de%20pantalla%20(32).png)
