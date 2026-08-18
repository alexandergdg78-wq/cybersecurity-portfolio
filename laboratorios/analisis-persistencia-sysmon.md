# Auditoría de Persistencia en Windows y Eventos Clave con Sysmon

## 1. Introducción y Objetivos
En las operaciones de un Centro de Operaciones de Seguridad (SOC), la detección de técnicas de **persistencia** es fundamental. Una vez que un atacante logra acceso inicial, intentará asegurar su permanencia en el sistema ante reinicios o bloqueos. 

Este reporte documenta los eventos principales para el monitoreo de persistencia en Windows y una auditoría práctica realizada en la consola local mediante PowerShell.

---

## 2. Indicadores de Compromiso (Sysmon & Windows Event Logs)

### Eventos clave de Sysmon
* **Event ID 1 (Process Creation):** Monitorea la creación de nuevos procesos. Esencial para detectar ejecuciones anómalas (ej: `winword.exe` spawning `powershell.exe`).
* **Event ID 3 (Network Connection):** Registra conexiones de red salientes o entrantes realizadas por procesos en la máquina.
* **Event ID 11 (File Create):** Identifica la creación o descarga de archivos ejecutables/scripts en rutas temporales (`AppData\Local\Temp`).

### Eventos clave de Persistencia en Windows
* **Event ID 4698:** Creación de una Tarea Programada (*Scheduled Task*).
* **Event ID 7045:** Instalación de un nuevo servicio en el sistema (*New Service Installed*).

---

## 3. Auditoría Práctica mediante PowerShell (Claves Run)

Se ejecutó una inspección sobre las claves de registro de inicio automático del usuario (*Run Keys*) para identificar posibles binarios sospechosos o rutas no autorizadas.

### Comando ejecutado:
```powershell
Get-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run"
