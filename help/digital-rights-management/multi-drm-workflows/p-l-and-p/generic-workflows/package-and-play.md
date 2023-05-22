---
description: Puede utilizar el empaquetador Bento4 de ExpressPlay para preparar contenido para cualquiera de las soluciones DRM compatibles con Primetime Cloud DRM, con tecnología ExpressPlay.
title: ExpressPlay Packager / Cloud DRM / TVSDK
exl-id: ff937279-3866-4d0a-9a19-cf61726299e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

Puede utilizar el empaquetador Bento4 de ExpressPlay para preparar contenido para cualquiera de las soluciones DRM compatibles con Primetime Cloud DRM, con tecnología ExpressPlay.

Esta tarea describe cómo utilizar una herramienta de terceros para preparar contenido protegido, en este caso *Herramientas ExpressPlay Bento4*, para su uso con diversas soluciones DRM. Para obtener más información, consulte la *Herramientas de Bento4* documentación sobre la [ExpressPlay](https://www.expressplay.com/developer/) sitio web.
1. Adquiera una cuenta de ExpressPlay y obtenga la información de ExpressPlay Customer Authenticator.

   Consulte [Inicio rápido de Primetime DRM Cloud.](../../quick-start/quick-overview.md)
1. Si está cifrando contenido para Primetime Access , adquiera el SDK de acceso a Adobe de Primetime desde Adobe, junto con los certificados necesarios (certificados de licencia, transporte y empaquetado).
1. Proporcione una clave de cifrado de contenido (CEK) y un ID de almacenamiento de clave de cifrado de contenido (CEKSID) para su uso en todos los sistemas DRM. (Los genera aleatoriamente mediante OpenSSL o similar).

   La clave CEK es la clave real que utiliza para cifrar los archivos de vídeo. O bien lo almacena de forma segura en su propio servidor en su propio sistema de administración de claves, o puede hacer uso de ExpressPlay [solución de almacenamiento de claves](https://www.expressplay.com/developer/key-storage/).

   Un CEKSID es el identificador de una CEK en particular. No se pasa (normalmente) la clave de cifrado. Por ejemplo, al solicitar un token de licencia, debe proporcionar el CEKSID.

1. Si está cifrando contenido para Access, utilice su CEK para crear metadatos de acceso de Primetime asociados al contenido.

1. Fragmente el contenido para prepararlo para el *Bento4 MP4DASH* herramienta.

   Para este paso puede utilizar la variable *MP4FRAGMENT* herramienta. Solo es necesario fragmentar el contenido una vez. Por ejemplo:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. Utilice el *MPDASH de Bento4* para &quot;DASH-ify&quot; y cifrar el contenido fragmentado.

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

       Este servidor necesita gestionar las siguientes operaciones:
   
   1. Selección del contenido por parte del cliente. Esta implementación necesita incluir un extremo para que los clientes soliciten un token de contenido para un ID de contenido específico.
   1. Derechos del cliente
   1. Solicitudes de token de licencia (ExpressPlay) del cliente ( [Referencia de respuesta/solicitud de token de licencia de ExpressPlay](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. Cree su cliente de.

   El cliente debe incluir una llamada al servidor de la tienda. El Adobe recomienda que el cliente llame a la tienda después de que el usuario seleccione algún contenido y después de que el usuario se autentique. A continuación, pase el token devuelto desde ExpressPlay a su reproductor para utilizarlo en las solicitudes de licencia. Las introducciones para implementar el componente DRM de sus reproductores se encuentran aquí:

   * TVSDK del explorador para HTML5
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Con el token de licencia en la mano, el cliente ahora puede derivar la URL de solicitud del token y realizar la solicitud de licencia a ExpressPlay, y luego reproducir el contenido protegido seleccionado para el usuario.
