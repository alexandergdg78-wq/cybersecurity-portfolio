Análisis de Logs de Firewall: Detección y Contención de Escaneo de Puertos (Reconocimiento).

1. Objetivo del Laboratorio
Identificar un escaneo de puertos automatizado dirigido a la infraestructura de la empresa, diferenciando los intentos de intrusión del tráfico web legítimo, para aplicar medidas de contención sin interrumpir la operatividad del negocio.

2. Análisis del Incidente (Triaje)

Detección: Se registraron múltiples bloqueos simultáneos en el Firewall hacia puertos administrativos críticos (21 FTP, 22 SSH, 23 Telnet) provenientes de la IP de origen 203.0.113.50.

Evaluación de Impacto: La misma IP registró conexiones permitidas hacia los puertos 80 (HTTP) y 443 (HTTPS). Se determinó que el servidor no fue comprometido, ya que estos puertos están intencionalmente abiertos para alojar la página web pública de la organización.

Diagnóstico: El atacante ejecutó una herramienta automatizada (Port Scanning) correspondiente a la fase de Reconocimiento de la Cyber Kill Chain para mapear vulnerabilidades.

3. Acción de Respuesta (Mitigación)

Se descartó la opción de aislar el servidor de la red para evitar un ataque de denegación de servicio autoinfligido y mantener la página web operativa.

Se aplicó una regla de denegación (Drop Rule) directamente en el Firewall para bloquear todo el tráfico entrante exclusivo desde la IP maliciosa 203.0.113.50.

El incidente fue contenido y el reporte escalado al equipo de Nivel 2 para el monitoreo de la subred del atacante.
