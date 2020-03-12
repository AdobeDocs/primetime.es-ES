---
description: Puede utilizar el empaquetador Bento4 de ExpressPlay para preparar contenido para cualquiera de las soluciones DRM admitidas por Primetime Cloud DRM, con tecnología ExpressPlay.
seo-description: Puede utilizar el empaquetador Bento4 de ExpressPlay para preparar contenido para cualquiera de las soluciones DRM admitidas por Primetime Cloud DRM, con tecnología ExpressPlay.
seo-title: ExpressPlay Packager / Cloud DRM / TVSDK
title: ExpressPlay Packager / Cloud DRM / TVSDK
uuid: 0d2f5a8d-15c4-42ba-acb8-1dc8d5bc62de
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

Puede utilizar el empaquetador Bento4 de ExpressPlay para preparar contenido para cualquiera de las soluciones DRM admitidas por Primetime Cloud DRM, con tecnología ExpressPlay.

Esta tarea describe cómo utilizar una herramienta de terceros para preparar contenido protegido, en este caso *ExpressPlay Bento4 Tools*, para su uso con una variedad de soluciones DRM. Para obtener más información, consulte la documentación de las herramientas *de* Bento4 en el sitio web de [ExpressPlay](https://www.expressplay.com/developer/) .
1. Adquiera una cuenta de ExpressPlay y obtenga la información del autenticador del cliente de ExpressPlay.

   Consulte Inicio rápido de [Primetime DRM Cloud.](../../quick-start/quick-overview.md)
1. Si va a cifrar contenido para Primetime Access, adquiera el SDK de Adobe Access de Primetime de Adobe, junto con los certificados necesarios (certificados de licencia, transporte y empaquetado).
1. Proporcione una clave de cifrado de contenido (CEK) y un ID de almacenamiento de claves de cifrado de contenido (CEKSID) para su uso en todos los sistemas DRM. (Las genera aleatoriamente mediante OpenSSL o similar).

   El CEK es la clave real que se utiliza para cifrar los archivos de vídeo. Puede almacenarlo de forma segura en su propio servidor en su propio sistema de administración de claves o puede utilizar la solución [de almacenamiento](https://www.expressplay.com/developer/key-storage/)clave de ExpressPlay.

   Un CEKSID es el identificador de un CEK en particular. No pasa (normalmente) la clave de cifrado. Por ejemplo, al solicitar un token de licencia, debe proporcionar el CEKSID.

1. Si va a cifrar contenido para Access, utilice el CEK para crear metadatos de Primetime Access asociados al contenido.

1. Fragmente su contenido para prepararlo para la herramienta *Bento4 MP4DASH* .

   Para este paso puede utilizar la herramienta *MP4FRAGMENT* . Solo tiene que fragmentar el contenido una vez. Por ejemplo:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. Utilice la herramienta *Bento4 MPDASH* para &quot;DASH-ify&quot; y cifrar su contenido fragmentado.

   Utilice este comando para especificar todos los sistemas DRM que utilizará y pasar los metadatos de Primetime Access generados a partir de los pasos anteriores. Por ejemplo:

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
   1. Derechos del cliente
   1. Solicitudes de token de licencia (ExpressPlay) del cliente (solicitud de token de licencia [ExpressPlay/referencia](../../license-token-req-resp-ref/license-req-resp-overview.md)de respuesta)

1. Cree su cliente.

   El cliente debe incluir una llamada a su servidor de tienda. Adobe recomienda que el cliente llame a la tienda después de que el usuario seleccione contenido y después de autenticar al usuario. A continuación, pase el token devuelto por ExpressPlay a su reproductor para utilizarlo en solicitudes de licencia. Las introducciones para implementar el componente DRM de sus reproductores están aquí:

   * TVSDK del explorador para HTML5
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Con el token de licencia en mano, el cliente ahora puede derivar la URL de solicitud del token y realizar la solicitud de licencia a ExpressPlay y, a continuación, reproducir el contenido protegido seleccionado para el usuario.
