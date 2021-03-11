---
description: Utilice la función CEK externo para vend y empaquetar licencias utilizando su CKMS existente.
title: Uso de CEK externo para otorgar y empaquetar licencias
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Uso de CEK externo para otorgar y empaquetar licencias{#using-external-cek-to-vend-and-package-licenses}

Utilice la función CEK externo para vend y empaquetar licencias utilizando su CKMS existente.

## EncryptContentWithExternalKey.java

Esta es una herramienta de línea de comandos que cifrará AAXS en un vídeo y creará metadatos que *no* contendrán el CEK (protegido con el certificado público de un servidor de licencias AAXS). En su lugar, la herramienta incrusta un ID de CEK en los metadatos del vídeo.

Durante la adquisición de licencias, el servidor de licencias AAXS observa un indicador en los metadatos que identifica que este contenido estaba protegido mediante un CEK externo. El servidor de licencias extraerá el ID de CEK de los metadatos y, a continuación, consultará un repositorio/CKMS seguro para recuperar el CEK adecuado.

## Flujo de trabajo de paquetes

1. Asegúrese de que está utilizando Java 1.6.0_24 o posterior.
1. Para ver el uso de la herramienta: `java -jar AdobePackager_ExternalCEK.jar`
1. Para empaquetar contenido:

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* El código fuente Java se puede crear utilizando el ANT `build-samples.xml` incluido
>* El SDK de Flash Access ( `adobe-flashaccess-sdk.jar`) debe estar en la ruta de clase

>



## Flujo de trabajo del servidor

1. Configure la Implementación de referencia.
1. Si existe, limpie las implementaciones de implementación de referencia anteriores:

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. Compruebe que haya un archivo [!DNL CEKDepot.properties] junto a su [!DNL flashaccess-refimpl.properties]

1. Inicio de una solicitud de licencia desde un reproductor de Adobe Primetime
1. Observe los registros de Ref Impl para ver algo similar a:

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. Es posible que tenga que cambiar la configuración de [!DNL log4j.xml] para registrar a nivel `DEBUG` ( `INFO` está configurado de forma predeterminada)

## Problemas conocidos

Ninguna
