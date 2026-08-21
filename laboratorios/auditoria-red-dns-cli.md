# Auditoría de Conexiones de Red e Integridad DNS mediante CLI en Windows

## 1. Objetivo del Laboratorio
Documentar los procedimientos de consola en Windows (CMD) para el triaje rápido de conexiones de red activas, identificación de procesos asociados (PID) y la verificación de integridad en la resolución de nombres local (archivo Hosts y caché DNS).

---

## 2. Inspección de Conexiones Activas y Mapeo de Procesos

Para identificar comunicaciones hacia direcciones IP externas o posibles servidores C2, se ejecutó la correlación entre sockets activos y ejecutables locales.

### Paso A: Filtrado de conexiones establecidas
```cmd
netstat -ano | findstr "ESTABLISHED"
