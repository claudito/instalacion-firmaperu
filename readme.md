### Guía de Instalación Api Firma Perú

### Requisito
Esta implementación usa [7-zip](https://www.7-zip.org/).

Para instalar 7z en **Windows 10/11** seguir los siguientes pasos:
1) Descargar e instalar 7z de [aquí](https://www.7-zip.org/)
2) La ruta de instalacion por defecto es C:\Program Files\7-Zip
3) Abrir un cmd *(simbolo de sistema o consola de comandos)*
4)Ejecutar, para poder agregar el path de manera global.
``bash
      setx PATH "%PATH%;C:\Program Files\7-Zip"
    ``` 


1. Descargue el ejecutable
   
   Windows 64-bit: [main.exe](https://github.com/claudito/instalacion-firmaperu/main.exe)
   
2. Copia la carpeta **public** del repositorio esta contiene 2 imagenes: iFirma.png e iLogo.png
3. Crea un archivo **config.properties** con los siguientes parametros :
    ``` bash
    # Identificador proporcionado por SEGDI-PCM
    clientId=K57845459hkj
    # Identificador proporcionado por SEGDI-PCM
    clientSecret=TYUOPDLDFDG
    # Direccion Ip y Puerto de escucha Firma Perú
    serverAddress=0.0.0.0:9091
    # Clave secreta para generar Tokens
    secretKeyJwt=muysecretokenjwt
    # Usuario que accedera a la API
    userAccessApi=usuarioAccesoApi
    # Tiempo de expiración del Token en minutos. Ejemplo 5 minutos (Opcional)
    timeExpireToken=5

    ``` 
4. En caso desee habilitar protocolo **https** es necesario que ingrese los siguientes parametros :
    ``` bash
    # Certificado SSL/TLS (Opcional)
    certificateFileTls=cert.pem
    # Clave Privada SSL/TLS (Opcional)
    privateKeyFileTls=key.pem
    ```
5. Si necesitas controlar la rotación del log utiliza los siquientes parametros:
    ``` bash
    # Tamaño máximo en MB antes de rotar (Opcional)
    maxSize=10
    # Número máximo de archivos de backup (Opcional)
    maxBackups=3
    # Máximo de días a mantener los logs (Opcional)
    maxAge=3
    ```
6. Ejecuta el componente por cmd
    ``` bash
    main
    ```
