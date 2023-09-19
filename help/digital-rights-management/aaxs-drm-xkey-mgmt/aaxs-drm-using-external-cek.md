---
description: Utilice la función CEK externo para vender y empaquetar licencias utilizando el CKMS existente.
title: Uso de CEK externo para vender y empaquetar licencias
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Uso de CEK externo para vender y empaquetar licencias{#using-external-cek-to-vend-and-package-licenses}

Utilice la función CEK externo para vender y empaquetar licencias utilizando el CKMS existente.

## EncryptContentWithExternalKey.java

Se trata de una herramienta de línea de comandos que cifrará con AAXS un vídeo y creará metadatos que *no* contener el CEK (protegido con un certificado público del servidor de licencias AXS). En su lugar, la herramienta incrusta un ID de CEK en los metadatos del vídeo.

Durante la adquisición de la licencia, el servidor de licencias de AAXS observa un indicador en los metadatos que indica que este contenido se protegió mediante una CEK externa. El servidor de licencias extraerá el ID de CEK de los metadatos y, a continuación, consultará un repositorio/CKMS seguro para recuperar el CEK adecuado.

## Empaquetando flujo de trabajo

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
>* El código fuente Java se puede crear con el ANT incluido `build-samples.xml`
>* El SDK de Flash Access ( `adobe-flashaccess-sdk.jar`) debe estar en la ruta de clase
>

## Flujo de trabajo del servidor

1. Configure la Implementación de referencia.
1. Si existe alguna, limpie las implementaciones de implementación de referencia anteriores:

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. Compruebe que haya un [!DNL CEKDepot.properties] archivo junto con su [!DNL flashaccess-refimpl.properties]

1. Iniciar una solicitud de licencia desde un reproductor de Adobe Primetime
1. Busque en los registros Impl de referencia algo similar a:

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. Es posible que tenga que cambiar su [!DNL log4j.xml] configuración para iniciar sesión en `DEBUG` level ( `INFO` está configurado de forma predeterminada)

## Problemas conocidos

Ninguno
