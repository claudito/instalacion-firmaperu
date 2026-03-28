# Guia: Ejecutar API como servicio en Windows Server

Esta guia deja `main.exe` corriendo como servicio para que inicie automaticamente cuando reinicie el servidor.

## 1. Verificar estructura y configuracion

En la carpeta del proyecto deben existir:

- `main.exe`
- `config.properties`
- `public\` (con sus imagenes)

Valida que en `config.properties` tengas el puerto correcto:

```properties
serverAddress=0.0.0.0:9091
```

## 2. Crear carpeta fija del servicio

Se recomienda mover el proyecto a una ruta estable, por ejemplo:

```powershell
C:\Servicios\FirmaPeru\
```

Ejemplo de estructura final:

```text
C:\Servicios\FirmaPeru\
  main.exe
  config.properties
  public\
```

## 3. Instalar el servicio con NSSM (recomendado)

`main.exe` no se instala solo como servicio de Windows. La forma mas estable es usar **NSSM** (Non-Sucking Service Manager).

1. Descarga NSSM:
   - https://nssm.cc/download
2. Descomprime y copia `nssm.exe` (x64) a una ruta, por ejemplo:
   - `C:\Tools\nssm\nssm.exe`
3. Abre **PowerShell como Administrador**.
4. Crea el servicio:

```powershell
C:\Tools\nssm\nssm.exe install FirmaPeruAPI
```

Se abrira una ventana de configuracion. Coloca:

- `Path`: `C:\Servicios\FirmaPeru\main.exe`
- `Startup directory`: `C:\Servicios\FirmaPeru`
- `Arguments`: (vacio)

En la pestaña **Details**:

- `Display name`: `Firma Peru API`
- `Description`: `Servicio API de Firma Peru`

En la pestaña **Startup**:

- `Startup type`: `Automatic`

Opcional (recomendado), en pestaña **I/O**:

- `Output (stdout)`: `C:\Servicios\FirmaPeru\logs\stdout.log`
- `Error (stderr)`: `C:\Servicios\FirmaPeru\logs\stderr.log`

Luego haz clic en **Install service**.

## 4. Iniciar y validar el servicio

En PowerShell (Administrador):

```powershell
Start-Service FirmaPeruAPI
Get-Service FirmaPeruAPI
```

Debe aparecer en estado `Running`.

## 5. Probar acceso local y por red

Desde el servidor:

```powershell
netstat -ano | findstr :9091
```

Debe mostrar el puerto `9091` en escucha.

Desde otra maquina de la red, prueba:

```text
http://IP_DEL_SERVIDOR:9091
```

Si no responde, revisa firewall.

## 6. Abrir firewall para el puerto 9091 (si aplica)

Ejecuta en PowerShell (Administrador):

```powershell
New-NetFirewallRule -DisplayName "FirmaPeru API 9091" -Direction Inbound -Protocol TCP -LocalPort 9091 -Action Allow
```

## 7. Comandos utiles de operacion

```powershell
Stop-Service FirmaPeruAPI
Start-Service FirmaPeruAPI
Restart-Service FirmaPeruAPI
Get-Service FirmaPeruAPI
```

Si cambias `config.properties` o reemplazas `main.exe`, reinicia el servicio:

```powershell
Restart-Service FirmaPeruAPI
```

## 8. Configurar recuperacion ante fallos (recomendado)

Para que Windows lo reinicie automaticamente si falla:

```powershell
sc.exe failure FirmaPeruAPI reset= 86400 actions= restart/5000/restart/5000/restart/5000
```

## 9. Desinstalar el servicio (si necesitas rehacerlo)

```powershell
Stop-Service FirmaPeruAPI
C:\Tools\nssm\nssm.exe remove FirmaPeruAPI confirm
```

---

## Nota importante

- Ejecutar `main.exe` manualmente funciona solo durante la sesion actual.
- Como servicio, queda registrado en Windows y se levanta automaticamente tras reiniciar el servidor.
