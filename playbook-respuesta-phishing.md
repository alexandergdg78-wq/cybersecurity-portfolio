🛡️ Playbook de Respuesta a Incidentes: Análisis de Phishing y Malware
Autor: Alejandro Matias García | Analista de Ciberseguridad (SOC Tier 1)

Objetivo del Playbook: Estandarizar el proceso de triaje, contención, análisis y remediación ante una alerta de correo electrónico malicioso (Phishing) con posible infección de malware, protegiendo los activos y la continuidad del negocio.

🛠️ Herramientas Utilizadas en este Laboratorio
SIEM: Monitoreo y correlación de eventos.

EDR: Análisis de comportamiento en el Endpoint y aislamiento de red.

OSINT / Threat Intelligence:

VirusTotal (Análisis estático de hashes y URLs)

Any.Run (Sandbox para análisis dinámico de comportamiento)

AbuseIPDB (Reputación de Direcciones IP)

Firewall Perimetral: Bloqueo de Indicadores de Compromiso (IOCs).

🚨 Escenario del Incidente
El SIEM genera una alerta de prioridad ALTA: Un usuario del departamento de Finanzas ha reportado un correo sospechoso con el asunto "URGENTE: Factura Impaga Agosto". El correo contiene un archivo adjunto llamado Factura_Agosto.xlsm.

👣 Fases de Respuesta (Paso a Paso)
FASE 1: Triaje y Recolección de Datos (Reconocimiento)
Validar la alerta en el SIEM: Confirmar a qué hora llegó el correo y quién es el destinatario exacto.

Extracción de IOCs (Indicadores de Compromiso):

Dirección de correo del remitente.

Dirección IP de origen del correo.

Hash (Firma digital) del archivo adjunto Factura_Agosto.xlsm.

Verificación de impacto inicial: Consultar en el sistema de correo corporativo si este mismo email fue enviado a otros empleados de la compañía.

FASE 2: Contención Inmediata (Prevención de Movimiento Lateral)
Revisión de telemetría en el EDR: Buscar el nombre del equipo afectado. Verificar si el usuario hizo clic y ejecutó el archivo.

Análisis de comportamiento: Se detecta que tras la descarga del archivo, un proceso legítimo de Windows (ej. calc.exe o powershell.exe) intenta establecer una conexión externa por el puerto 443. Esto indica una técnica de Living off the Land (camuflaje).

Acción Táctica: Ejecutar inmediatamente el comando Network Isolate (Aislamiento de Red) desde la consola del EDR sobre la computadora afectada.

Resultado: El equipo queda desconectado de la red corporativa para evitar la propagación del malware, pero mantiene comunicación exclusiva con la consola de seguridad para su investigación.

FASE 3: Inteligencia de Amenazas e Investigación
Análisis Estático (VirusTotal):

Se ingresa el Hash del archivo en VirusTotal.

Resultado simulado: 0/70 motores lo detectan. Posible amenaza de "Día Cero" (Zero-Day) o malware muy reciente.

Análisis Dinámico en Sandbox (Any.Run):

Se sube el archivo .xlsm al entorno aislado de Any.Run.

Se ejecuta el archivo para observar su comportamiento real.

Descubrimiento: El macro del Excel se ejecuta en silencio y realiza una petición TCP hacia la Dirección IP 198.51.100.45 para descargar un payload adicional.

Validación de Reputación (AbuseIPDB):

Se consulta la IP 198.51.100.45 en AbuseIPDB.

Resultado: La IP tiene un puntaje de abuso del 100%, reportada múltiples veces por distribuir Ransomware y actuar como servidor de Comando y Control (C2). Se confirma el Positivo Verdadero.

FASE 4: Erradicación y Remediación
Bloqueo Perimetral: Ingresar al Firewall corporativo y bloquear cualquier tráfico entrante o saliente hacia la IP 198.51.100.45.

Purga de Correo: Ingresar al servidor de correo (ej. Microsoft Defender for Office 365 / Google Workspace) y eliminar el correo malicioso (Hard Delete) de la bandeja de entrada del usuario afectado y de cualquier otro empleado que lo haya recibido.

Limpieza del Endpoint: Con la máquina aún aislada, ejecutar un escaneo profundo (Full Scan) a través del EDR para eliminar el archivo malicioso y cualquier persistencia en el registro de Windows.

Levantamiento de Contención: Una vez confirmada la limpieza total, retirar el "Network Isolate" para devolver el equipo a la red y permitir que el empleado retome sus funciones.

FASE 5: Lecciones Aprendidas (Post-Incidente)
Actualización de Defensas: Agregar el Hash del archivo y la IP maliciosa a la lista negra (Blocklist) del EDR y el Firewall.

Concientización: Notificar al departamento de Recursos Humanos/Capacitación para enviar un refuerzo de entrenamiento sobre detección de Phishing al área de Finanzas.
