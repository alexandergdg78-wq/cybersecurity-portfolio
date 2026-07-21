Título del Proyecto: Análisis de Prevención de Pérdida de Datos (DLP): Detección y Contención de Exfiltración.

1. Objetivo del Laboratorio
Monitorizar, detectar y mitigar un intento de exfiltración de datos confidenciales hacia servicios de almacenamiento en la nube no autorizados (Shadow IT), evaluando el contexto del usuario y aplicando medidas de contención sin pérdida de evidencia forense.

2. Análisis del Incidente (Triaje)

Detección: El sistema DLP generó una alerta de severidad Alta por tráfico saliente (Outbound) anómalo desde el equipo PC-FINANZAS-01.

Indicadores de Riesgo (Contexto):

Horario Inusual: La actividad se registró a las 03:15 AM, fuera de la ventana operativa normal del departamento financiero.

Volumen de Datos: Transferencia masiva de un archivo empaquetado (backup_historico.zip) de 45 GB.

Destino No Autorizado: El tráfico se dirigía hacia mega.nz, un servicio de nube personal no avalado por las políticas de seguridad corporativa.

3. Acción de Respuesta (Mitigación y Escalado)

Se ordenó la interrupción inmediata de la transferencia bloqueando la conexión hacia el dominio de destino a nivel de red, previniendo la fuga total de los activos de información.

Se retuvo el equipo en estado de encendido, aislado de la salida a internet, para preservar la memoria RAM y los registros locales para el análisis forense.

El incidente fue escalado al Nivel 2 y al equipo de Respuesta a Incidentes (IR) para verificar el origen de la actividad (compromiso de credenciales vs. negligencia interna) mediante contacto directo con el titular de la cuenta.
