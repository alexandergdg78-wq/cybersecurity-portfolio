1. Objetivo del Laboratorio
Identificar y contener la ejecución de código malicioso oculto (Fileless Malware) iniciado a través de un documento ofimático armado, analizando la relación entre procesos padre e hijo.

2. Análisis del Incidente (Triaje)

Detección: El sistema EDR (Endpoint Detection and Response) generó una alerta crítica en el equipo PC-RRHH-05.

Vector de Infección: El usuario ejecutó un documento de Microsoft Excel (excel.exe), el cual, presuntamente mediante la habilitación de macros maliciosas, inició un proceso hijo no autorizado.

Técnica de Evasión: El proceso hijo consistió en la ejecución de la consola de Windows (powershell.exe) utilizando los parámetros -WindowStyle Hidden (para ocultar la actividad al usuario) y -EncodedCommand (para ofuscar el código malicioso en formato Base64 y evadir firmas de antivirus tradicionales).

3. Acción de Respuesta (Mitigación)

Se ordenó el aislamiento inmediato del equipo PC-RRHH-05 de la red corporativa y de internet para prevenir el Movimiento Lateral del malware hacia otros servidores.

El equipo se mantuvo encendido para preservar la evidencia volátil en la memoria RAM.

El ticket fue escalado al equipo de Nivel 2 y Análisis Forense para la decodificación del comando Base64 y la posterior remediación del sistema.
