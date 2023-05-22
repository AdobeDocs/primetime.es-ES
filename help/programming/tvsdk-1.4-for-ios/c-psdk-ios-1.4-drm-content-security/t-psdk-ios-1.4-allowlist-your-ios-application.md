---
description: Puede crear listas de permitidos de sus aplicaciones de iOS con la herramienta de herramientas de macros de Adobe.
title: Lista de permitidos de la aplicación de iOS
exl-id: ff647647-6c5f-4a10-9040-8600f6103b99
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Lista de permitidos de la aplicación de iOS {#allowlist-your-ios-application}

Puede crear listas de permitidos de sus aplicaciones de iOS con la herramienta de herramientas de macros de Adobe.

Por lo general, al completar una aplicación de TVSDK, puede utilizar las herramientas de línea de comandos de DRM de Adobe Primetime para realizar la lista de permitidos de la aplicación.

>[!TIP]
>
>También puede utilizar estas herramientas para crear directivas DRM y cifrar contenido.

Permitir que se enumere la aplicación garantiza que el contenido protegido solo se pueda reproducir en el reproductor de vídeo. Sin embargo, para permitir la inclusión en una lista de aplicaciones de iOS, es necesario completar un procedimiento especial que funcione con las directivas de envío de aplicaciones de Apple.

Antes de enviar una aplicación de iOS, debe firmarla y publicarla en Apple.

>[!NOTE]
>
>Apple elimina la firma del desarrollador y vuelve a firmar la aplicación con su propio certificado.

Debido a la nueva firma, no se puede utilizar la información de la lista de permitidos que generó antes de enviarla a Apple App Store.

Para trabajar con esta directiva de envío, el Adobe ha creado un `machotools` herramienta que tomará la huella digital de su aplicación de iOS para crear un valor de compendio, firmar este valor e insertar este valor en su aplicación de iOS. Después de tomar la huella digital de su aplicación de iOS, puede enviarla al App Store de Apple. Cuando un usuario ejecuta la aplicación desde App Store, Primetime DRM realiza un cálculo en tiempo de ejecución de la huella digital de la aplicación y la confirma con el valor de resumen que se insertó anteriormente en la aplicación. Si la huella digital coincide, la aplicación se confirma como incluida en la lista de permitidos y se permite la reproducción del contenido protegido.

El Adobe `machotools` está incluida en el SDK de TVSDK de iOS, en [!DNL [...]/tools/DRM].

Para usar `machotools`:

1. Genere un par de claves.

   Para utilizar una utilidad como OpenSSL, abra una ventana de comandos e introduzca lo siguiente:

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. Cuando se le pida, introduzca una contraseña para proteger la clave privada.

   Las contraseñas deben contener al menos 12 caracteres, y los caracteres deben incluir una mezcla de caracteres ASCII en mayúsculas y minúsculas y números.
1. Para utilizar OpenSSL para generar una contraseña segura, abra una ventana de comandos e introduzca lo siguiente:

   ```shell
   openssl rand -base64 8
   ```

1. Generar una solicitud de firma de certificado (CSR).

   Para utilizar OpenSSL para generar una CSR, abra una Ventana de comandos e introduzca lo siguiente:

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. Firme automáticamente el certificado e introduzca cualquier duración.

   El ejemplo siguiente proporciona una caducidad de 20 años:

   ```shell
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. Convierta el certificado autofirmado en un archivo PKCS#12:

   ```shell
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   Puede utilizar el certificado autofirmado para firmar la aplicación de iOS.

1. Actualice la ubicación del archivo PFX y la contraseña.
1. Antes de crear la aplicación en Xcode, vaya a  **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** y agregue el siguiente comando al script de ejecución:

   ```shell
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. Ejecutar [!DNL machotools] para generar el valor hash del ID del publicador de la aplicación.

   ```shell
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. Cree una nueva directiva DRM o actualice la directiva existente para incluir el valor hash del ID de publicador devuelto.
1. Uso del [!DNL AdobePolicyManager.jar], cree una nueva directiva DRM (actualice la directiva existente) para incluir el valor hash del ID de publicador devuelto, un ID de aplicación opcional y los atributos de versión mínima y máxima en el incluido [!DNL flashaccess-tools.properties] archivo.

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. Empaquete el contenido mediante la nueva política de DRM y confirme la reproducción del contenido de la lista de permitidos en la aplicación de iOS.
