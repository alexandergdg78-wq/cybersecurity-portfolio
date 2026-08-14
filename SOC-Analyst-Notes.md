# Análisis de Eventos de Autenticación en Windows (SOC L1)

## Caso de Estudio: Detección de Fuerza Bruta por RDP

### 1. Resumen del Incidente
Inundación de intentos fallidos de inicio de sesión seguidos de una autenticación exitosa mediante Remote Desktop Protocol.

### 2. Event IDs Identificados
* **Event ID 4625:** Fallo de autenticación (`0xC000006A` - Nombre válido, contraseña incorrecta).
* **Event ID 4624:** Autenticación exitosa.
* **Logon Type 10:** Conexión remota por RDP.

### 3. Playbook de Respuesta Inmediata
1. **Contención:** Inactivar cuenta en Active Directory y cerrar la sesión RDP activa.
2. **Aislamiento:** Aislar la estación de trabajo de la red vía EDR para evitar movimiento lateral.
3. **Bloqueo Perimetral:** Bloquear la IP origen en el Firewall/Gateway.
4. **Escalado:** Reportar al equipo L2 / Incident Response con el ticket documentado.
