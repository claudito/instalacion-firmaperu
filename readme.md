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

## 🖊️ Integración con FirmaPeru Invoker

### Ejemplo de uso desde el cliente (JavaScript)

```javascript
// Listamos los documentos que se desean firmar digitalmente
let pdfs = [];
pdfs[0] = { url: "http://miservidor.com/docs1.pdf", name: "doc1" };
pdfs[1] = { url: "http://miservidor.com/docs2.pdf", name: "doc2" };

// Enviamos la posición donde se ubicará la representación gráfica de la firma digital
let firmaParam = {};
firmaParam.posx = 10;
firmaParam.posy = 12;
firmaParam.reason = "Soy el autor del documento pdf";
firmaParam.role = "Programador Full Stack";
firmaParam.stampSigned = "http://miservidor.com/estampillafirma.png"; // opcional
firmaParam.pageNumber = 1;        // opcional: página donde se pondrá la firma visible
firmaParam.visiblePosition = false; // opcional: interfaz gráfica nativa de Firma Perú
firmaParam.signatureStyle = 1;    // opcional: 1=horizontal 2=vertical 3=solo estampado 4=solo descripción
firmaParam.stampTextSize = 14;    // opcional
firmaParam.stampWordWrap = 37;    // opcional

// Instanciamos FirmaPeru con la IP donde se ejecuta main.exe
let firma = new FirmaPeru("http://192.168.1.10:9091");

// ⚠️ Importante:
// El Sistema de Gestión Documental se encarga de la autenticación y envía el token al cliente.
// El siguiente método es solo de demostración y NO debe usarse en producción desde el cliente.
let token = await firma.autenticacion("usuarioAccesoApi");

// Realiza el proceso de Firma Digital
let url_base = await firma.ejecutar(pdfs, firmaParam, token);

// Obtenemos los documentos firmados y los mostramos en un iframe
document.getElementById("frame1").src = url_base + "/" + encodeURI("doc1") + "/" + encodeURI(token);
document.getElementById("frame2").src = url_base + "/" + encodeURI("doc2") + "/" + encodeURI(token);
```

### Referencia de parámetros de firma (`firmaParam`)

| Parámetro        | Tipo    | Requerido | Descripción |
|------------------|---------|-----------|-------------|
| `posx`           | number  | Sí        | Posición horizontal de la firma en el PDF |
| `posy`           | number  | Sí        | Posición vertical de la firma en el PDF |
| `reason`         | string  | Sí        | Razón o motivo de la firma |
| `role`           | string  | Sí        | Rol del firmante |
| `stampSigned`    | string  | No        | URL de imagen para la estampilla de firma |
| `pageNumber`     | number  | No        | Página del PDF donde se colocará la firma visible |
| `visiblePosition`| boolean | No        | Activa la interfaz gráfica nativa de Firma Perú para posicionar la firma |
| `signatureStyle` | number  | No        | Estilo de firma: `1` horizontal, `2` vertical, `3` solo estampado, `4` solo descripción |
| `stampTextSize`  | number  | No        | Tamaño del texto en la estampilla |
| `stampWordWrap`  | number  | No        | Cantidad de caracteres por línea en el texto de la estampilla |

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
