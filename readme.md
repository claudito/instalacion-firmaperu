# 📘 Guía de Instalación API Firma Perú

------------------------------------------------------------------------

## ✅ Pre-requisitos

Esta implementación utiliza **7-Zip** para la gestión de archivos
comprimidos.

🔗 Sitio oficial:\
https://www.7-zip.org/

### Instalación en Windows 10 / 11

1.  Descargar e instalar **7-Zip** desde: 👉 https://www.7-zip.org/

2.  La ruta de instalación por defecto es:

```bash
 C:\Program Files\7-Zip
```
   

3.  Abrir **CMD (Símbolo del sistema)**.

4.  Ejecutar el siguiente comando para agregar 7-Zip al PATH global:

``` cmd
setx PATH "%PATH%;C:\Program Files\7-Zip"
```

⚠️ Importante:\
Cerrar y volver a abrir la consola luego de ejecutar el comando.

------------------------------------------------------------------------

## ⚙️ Configuración

### 1️⃣ Descargar el ejecutable

👉 **[Descargar
main.exe](https://raw.githubusercontent.com/claudito/instalacion-firmaperu/main/main.exe)**

------------------------------------------------------------------------

### 2️⃣ Copiar carpeta `public`

Copiar desde el repositorio la carpeta:

    public/

Debe contener:

-   iFirma.png
-   iLogo.png

------------------------------------------------------------------------

### 3️⃣ Crear archivo `config.properties`

``` properties
# Identificador proporcionado por SEGDI-PCM
clientId=K57845459hkj

# Identificador proporcionado por SEGDI-PCM
clientSecret=TYUOPDLDFDG

# Dirección IP y Puerto de escucha
serverAddress=0.0.0.0:9091

# Clave secreta JWT
secretKeyJwt=muysecretokenjwt

# Usuario acceso API
userAccessApi=usuarioAccesoApi

# Expiración del Token (minutos)
timeExpireToken=5
```

------------------------------------------------------------------------

### 4️⃣ Configuración HTTPS (Opcional)

``` properties
certificateFileTls=cert.pem
privateKeyFileTls=key.pem
```

------------------------------------------------------------------------

### 5️⃣ Rotación de Logs (Opcional)

``` properties
maxSize=10
maxBackups=3
maxAge=3
```

------------------------------------------------------------------------

### 6️⃣ Ejecutar componente

Abrir CMD en la carpeta del proyecto y ejecutar:

``` cmd
main
```

------------------------------------------------------------------------

## 📁 Estructura final requerida

    instalacion-firmaperu/
    │
    ├── public/
    │   ├── iFirma.png
    │   └── iLogo.png
    │
    ├── config.properties
    └── main.exe

⚠️ **Importante** 
- `main.exe` debe estar en la misma carpeta que
`config.properties`. 
- La carpeta `public` y sus imágenes son
obligatorias.

------------------------------------------------------------------------
