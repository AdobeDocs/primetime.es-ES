---
description: Puede utilizar el paquete Bento4 de ExpressPlay para preparar contenido para cualquiera de las soluciones DRM compatibles con Primetime Cloud DRM, con tecnología ExpressPlay.
title: Paquete ExpressPlay / Cloud DRM / TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Paquete ExpressPlay / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

Puede utilizar el paquete Bento4 de ExpressPlay para preparar contenido para cualquiera de las soluciones DRM compatibles con Primetime Cloud DRM, con tecnología ExpressPlay.

En esta tarea se describe cómo utilizar una herramienta de terceros para preparar contenido protegido, en este caso *ExpressPlay Bento4 Tools*, para su uso con varias soluciones DRM. Para obtener más información, consulte la documentación de *Bento4 tools* en el sitio web [ExpressPlay](https://www.expressplay.com/developer/).
1. Adquiera una cuenta de ExpressPlay y obtenga su información de autenticador del cliente de ExpressPlay.

   Consulte [Inicio rápido de la nube de DRM de Primetime.](../../quick-start/quick-overview.md)
1. Si está cifrando contenido para Primetime Access , adquiera el SDK de acceso al Adobe de Primetime desde el Adobe, junto con los certificados necesarios (certificados de licencia, transporte y empaquetado).
1. Proporcione una clave de cifrado de contenido (CEK) y un ID de almacenamiento clave de cifrado de contenido (CEKSID) para su uso en todos los sistemas DRM. (Los genera aleatoriamente usando OpenSSL o similar).

   El CEK es la clave real que se utiliza para cifrar los archivos de vídeo. Puede almacenarlo de forma segura en su propio servidor en su propio sistema de administración de claves o puede utilizar la [solución de almacenamiento de claves](https://www.expressplay.com/developer/key-storage/) de ExpressPlay.

   Un CEKSID es el identificador de un CEK en particular. No transfiere (normalmente) la clave de cifrado. Por ejemplo, al solicitar un token de licencia, proporcione el CEKSID.

1. Si está cifrando contenido para Access, utilice su CEK para crear metadatos de acceso de Primetime asociados con su contenido.

1. Fragmente el contenido para prepararlo para la herramienta *Bento4 MP4DASH*.

   Para este paso, puede utilizar la herramienta *MP4FRAGMENT*. Solo es necesario fragmentar el contenido una vez. Por ejemplo:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. Utilice la herramienta *Bento4 MPDASH* para &quot;identificar DASH&quot; y cifrar el contenido fragmentado.

   Utilice este comando para especificar todos los sistemas DRM que utilizará y pasar cualquier metadato de acceso de Primetime generado a partir de los pasos anteriores. Por ejemplo:

   ```
   /mp4dash -f  
   --use-segment-list  
   --use-segment-timeline  
   --encryption-key=<CEKSID>:<CEK>  
   --playready  
   --Widevine  
   --Widevine-header=provider:intertrust#content_id:2a  
   --primetime  
   --primetime-metadata=@AAXS.metadata 
    Fragmented.mp4 -o DASH_OUTPUT
   ```

1. Cree un &quot;servidor de tienda&quot;.

       Este servidor debe gestionar las siguientes operaciones:
   
   1. Selección de contenido por parte del cliente. Esta implementación debe incluir un punto final para que los clientes soliciten un token de contenido para un ID de contenido específico.
   1. Derecho del cliente
   1. Solicitudes de token de licencia (ExpressPlay) del cliente ( [solicitud de token de licencia de ExpressPlay/referencia de respuesta](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. Cree su cliente.

   El cliente debe incluir una llamada a su servidor de tienda. Adobe recomienda que el cliente llame a la tienda después de que el usuario seleccione algún contenido y después de autenticar al usuario. A continuación, pase el token devuelto desde ExpressPlay a su reproductor para utilizarlo en solicitudes de licencia. Las introducciones para implementar el componente DRM de sus reproductores están aquí:

   * TVSDK de navegador para HTML5
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Con el token de licencia en mano, el cliente ahora puede derivar la URL de solicitud del token y realizar la solicitud de licencia a ExpressPlay y, a continuación, reproducir el contenido seleccionado y protegido para el usuario.
