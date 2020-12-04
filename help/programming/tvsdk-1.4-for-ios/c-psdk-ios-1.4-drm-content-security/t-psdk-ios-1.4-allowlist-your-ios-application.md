---
description: Puede realizar la lista de permitidos de sus aplicaciones de iOS mediante la herramienta de herramientas de MacOS de Adobe.
seo-description: Puede realizar la lista de permitidos de sus aplicaciones de iOS mediante la herramienta de herramientas de MacOS de Adobe.
seo-title: Lista de permitidos de la aplicación iOS
title: Lista de permitidos de la aplicación iOS
uuid: 52ce1dd7-5f10-418e-9916-cec60eae874e
translation-type: tm+mt
source-git-commit: 0d3d74cb2b36acb3682304122ab61ba8636f640f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Lista de permitidos de la aplicación de iOS {#allowlist-your-ios-application}

Puede realizar la lista de permitidos de sus aplicaciones de iOS mediante la herramienta de herramientas de MacOS de Adobe.

Por lo general, al completar una aplicación TVSDK, puede utilizar las herramientas de la línea de comandos de Adobe Primetime DRM para la lista de permitidos de la aplicación.

>[!TIP]
>
>También puede utilizar estas herramientas para crear políticas de DRM y cifrar contenido.

Si se permite la publicación de la aplicación, se garantiza que el contenido protegido solo se puede reproducir en el reproductor de vídeo. Sin embargo, para permitir que se muestre una aplicación de iOS, es necesario que complete un procedimiento especial que funcione con las políticas de envío de aplicaciones de Apple.

Antes de enviar una aplicación de iOS, debe firmarla y publicarla en Apple.

>[!NOTE]
>
>Apple quita la firma del desarrollador y vuelve a firmar la aplicación con su propio certificado.

Debido a la nueva firma, no se puede utilizar la información de la lista permitida que generó antes de enviarla a Apple App Store.

Para trabajar con esta directiva de envío, Adobe ha creado una herramienta `machotools` que imprimirá el dedo de la aplicación iOS para crear un valor de compendio, firmar este valor e inyectar este valor en la aplicación iOS. Después de imprimir el dedo de la aplicación de iOS, puede enviarla a Apple App Store. Cuando un usuario ejecuta la aplicación desde la App Store, Primetime DRM realiza un cálculo en tiempo de ejecución de la huella digital de la aplicación y lo confirma con el valor de compendio que se insertó anteriormente en la aplicación. Si la huella digital coincide, se confirma que la aplicación está permitida en la lista y se permite reproducir contenido protegido.

La herramienta Adobe `machotools` se incluye en el SDK para iOS TVSDK, en el [!DNL [...]/tools/DRM].

Para usar `machotools`:

1. Genere un par de claves.

   Para utilizar una utilidad como OpenSSL, abra una ventana de comandos e introduzca lo siguiente:

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. Cuando se le solicite, introduzca una contraseña para proteger la clave privada.

   Las contraseñas deben contener al menos 12 caracteres, y los caracteres deben incluir una mezcla de caracteres y números ASCII en mayúsculas y minúsculas.
1. Para utilizar OpenSSL para generar una contraseña segura, abra una ventana de comandos e introduzca lo siguiente:

   ```shell
   openssl rand -base64 8
   ```

1. Generar una solicitud de firma de certificado (CSR).

   Para utilizar OpenSSL para generar un CSR, abra una ventana de comandos e introduzca lo siguiente:

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. Firme automáticamente el certificado e introduzca cualquier duración.

   El siguiente ejemplo proporciona una caducidad de 20 años:

   ```shell
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. Convierta el certificado autofirmado en un archivo PKCS#12:

   ```shell
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   Puede utilizar el certificado con firma personal para firmar su aplicación de iOS.

1. Actualice la ubicación del archivo PFX y la contraseña.
1. Antes de crear la aplicación en Xcode, vaya a **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** y agregue el siguiente comando a la secuencia de comandos de ejecución:

   ```shell
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. Ejecute [!DNL machotools] para generar el valor hash del ID de editor de la aplicación.

   ```shell
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. Cree una nueva directiva DRM o actualice la directiva existente para incluir el valor hash de ID de editor devuelto.
1. Mediante el uso de [!DNL AdobePolicyManager.jar], cree una nueva directiva DRM (actualice la directiva existente) para incluir el valor hash de ID de editor devuelto, un ID de aplicación opcional y los atributos de versión mínimo y máximo en el archivo incluido [!DNL flashaccess-tools.properties].

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. Empaquete el contenido mediante la nueva directiva DRM y confirme la reproducción del contenido permitido de la lista en la aplicación de iOS.
