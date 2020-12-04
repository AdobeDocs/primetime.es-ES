---
description: Utilice la función CEK externo para vend y empaquetar licencias mediante el CKMS existente.
seo-description: Utilice la función CEK externo para vend y empaquetar licencias mediante el CKMS existente.
seo-title: Uso de CEK externo para otorgar licencias y empaquetarlas
title: Uso de CEK externo para otorgar licencias y empaquetarlas
uuid: 1bfd8c6c-4ae9-47de-8247-085b5360127d
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Uso de CEK externo para otorgar licencias y paquetes{#using-external-cek-to-vend-and-package-licenses}

Utilice la función CEK externo para vend y empaquetar licencias mediante el CKMS existente.

## EncryptContentWithExternalKey.java

Esta es una herramienta de línea de comandos que cifrará AAXS un vídeo y creará metadatos que *no* contendrán el CEK (protegido con el certificado público de un servidor de licencias AAXS). En su lugar, la herramienta incrusta un ID CEK en los metadatos del vídeo.

Durante la adquisición de licencias, el servidor de licencias AAXS observa un indicador en los metadatos que identifica que este contenido se protegía mediante un CEK externo. El servidor de licencias extraerá el ID de CEK de los metadatos y, a continuación, consulta un repositorio/CKMS seguro para recuperar el CEK adecuado.

## Flujo de trabajo de paquetes

1. Asegúrese de utilizar Java 1.6.0_24 o posterior.
1. Para ver el uso de la herramienta: `java -jar AdobePackager_ExternalCEK.jar`
1. Para empaquetar contenido:

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* El código fuente de Java se puede crear usando la variable ANT `build-samples.xml` incluida
>* El SDK de Flash Access ( `adobe-flashaccess-sdk.jar`) debe estar en la ruta de clases

>



## Flujo de trabajo del servidor

1. Configure la implementación de referencia.
1. Si existe alguna, limpie las implementaciones anteriores de implementación de referencia:

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. Verifique que haya un archivo [!DNL CEKDepot.properties] junto con su [!DNL flashaccess-refimpl.properties]

1. Inicio de una solicitud de licencia de Adobe Primetime Player
1. Observe los registros de impacto de referencia para algo similar a:

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. Es posible que tenga que cambiar la configuración de [!DNL log4j.xml] para iniciar sesión en un nivel `DEBUG` ( `INFO` está configurada de manera predeterminada)

## Problemas conocidos

Ninguno
