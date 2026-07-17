Análisis Forense de Cabeceras de Correo: Identificación de Falso Positivo (Phishing Triage).

1. Objetivo del Laboratorio
Analizar un correo electrónico clasificado automáticamente como SPAM para determinar si se trata de un intento de suplantación de identidad (Spoofing/Phishing) o de un Falso Positivo.

2. Herramientas Utilizadas

Análisis de Cabeceras de Gmail (Original Header).

Inteligencia de Fuentes Abiertas (OSINT): AbuseIPDB.

3. Proceso de Triaje (Investigación)

Detección: Se identificó un correo sospechoso en la bandeja de SPAM con el asunto "Volvé a tu protección en minutos" proveniente de contacto@bina.seg.ar.

Extracción de IoC (Indicadores de Compromiso): Se extrajo la dirección IP de origen desde el código original del correo.

Análisis OSINT: Al consultar la IP en AbuseIPDB, se verificó que la infraestructura pertenece a la organización OSDE (Argentina).

Verificación de Protocolos de Seguridad: Se revisó la firma de las cabeceras, confirmando que los protocolos SPF, DKIM y DMARC arrojaron un resultado "PASS".

4. Conclusión (Resolución del Ticket)
Se determinó que el correo es un Falso Positivo. La alerta de SPAM se generó probablemente por el volumen de envío masivo de una campaña de marketing. El dominio remitente (bina.seg.ar) tiene correctamente autorizada la infraestructura de OSDE para el envío de sus correos. No hay riesgo de seguridad para el usuario final.
<img width="1366" height="768" alt="Captura de pantalla (82)" src="https://github.com/user-attachments/assets/f758e120-9085-439b-8652-1ae0fcc00958" />
<img width="1366" height="768" alt="Captura de pantalla (83)" src="https://github.com/user-attachments/assets/0c8bf960-dc6d-49e0-802c-c19315acec6d" />

