---
description: Puede utilizar el empaquetador sin conexión de Adobe para preparar contenido para cualquiera de las soluciones DRM admitidas por Primetime Cloud DRM, con la tecnología ExpressPlay.
seo-description: Puede utilizar el empaquetador sin conexión de Adobe para preparar contenido para cualquiera de las soluciones DRM admitidas por Primetime Cloud DRM, con la tecnología ExpressPlay.
seo-title: Primetime Packager / Cloud DRM / TVSDK
title: Primetime Packager / Cloud DRM / TVSDK
uuid: e54a0e4d-c8ea-46d4-b1b0-bed8a680f8f5
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# Primetime Packager / Cloud DRM / TVSDK {#primetime-packager-cloud-drm-tvsdk}

Puede utilizar el empaquetador sin conexión de Adobe para preparar contenido para cualquiera de las soluciones DRM admitidas por Primetime Cloud DRM, con la tecnología ExpressPlay.

Este conjunto de instrucciones supone que ya ha configurado una cuenta de administrador de ExpressPlay: [inicio rápido de DRM de Primetime](../../../multi-drm-workflows/quick-start/quick-overview.md).
1. Elija la infraestructura que se utilizará para empaquetar el contenido. Primetime Packager admite el empaquetado de contenido basado en la línea de comandos y la configuración para su uso con los DRM FairPlay, Widevine y PlayReady. TVSDK admite actualmente los siguientes formatos y codificación (y hay más en proceso):

   * DASH (CENC) / PlayReady, Widevine - Para HTML5
   * HLS / FairPlay, acceso: para iOS

1. Elija un sistema de administración de claves (KMS):

   * Utilice el KMS de ExpressPlay ( [Almacenamiento de la clave de ExpressPlay](https://www.expressplay.com/developer/key-storage/)); este sistema administra las claves de contenido mediante la API RESTful de ExpressPlay.

      o...

   * Configure su propio KMS. Cree una base de datos de claves de contenido, seleccionable por Content-ID.

      En cualquier caso, el KMS administra un suministro de claves de contenido, y cada clave tiene un Content-ID asociado.

1. Empaquete el contenido. Con Primetime Packager, puede empaquetar un fragmento de contenido para una solución DRM específica o para varias soluciones DRM.

   Los siguientes comandos de ejemplo muestran algunos ejemplos de empaquetado de contenido para distintas soluciones DRM:

   * [Amplia con Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19)  (genera archivo MPD):

      ```
      java -jar OfflinePackager.jar \ 
        -in_path [ 
        <your_content.mp4>] \ 
        -out_type dash \ 
        -out_path [ 
        <your_out_file_path>] \ 
        -drm \ 
        -drm_sys WIDEVINE \ 
        -key_file_path "creds/widevine_key.bin" \ 
        -widevine_key_id [ 
        <some_keyID>] \ 
        -widevine_content_id [ 
        <some_content-ID] \ 
        -widevine_header provider:intertrust#content_id:2a
      ```

   * [FairPlay con Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) (genera un archivo M3U8):

      ```
      java -jar OfflinePackager.jar  
        -in_path [ 
        <your_content.mp4>]  
        -out_type hls  
        -out_path [ 
        <your_out_file_path>]  
        -drm  
        -drm_sys FAIRPLAY  
        -key_file_path "creds/fairplay_key.bin"  
        -key_url "user_provided_value"
      ```

      >[!NOTE]
      >
      >El valor `key_url` se copia como está en el archivo M3U8.

1. Cree un &quot;servidor de tienda&quot;.

       El servidor de tienda debe encargarse de las siguientes operaciones:
   
   1. Selección de contenido por parte del cliente. Esta implementación debe incluir un punto final para que los clientes soliciten un token de contenido para un ID de contenido específico.
   1. Derechos del cliente
   1. Solicitudes de token de licencia (ExpressPlay) del cliente ( [solicitud de token de licencia de ExpressPlay / referencia de respuesta](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. Cree su cliente.

       El cliente debe incluir una llamada a su servidor de tienda. Adobe recomienda que el cliente llame a la tienda después de que el usuario seleccione algún contenido y después de autenticar al usuario. A continuación, pase el token devuelto por ExpressPlay a su reproductor para utilizarlo en solicitudes de licencia. Las introducciones para implementar el componente DRM de sus reproductores están aquí:
   
   * [TVSDK del explorador para HTML5](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Con el token de licencia en mano, el cliente ahora puede derivar la URL de solicitud del token, realizar la solicitud de licencia a ExpressPlay y, a continuación, reproducir el contenido seleccionado para el usuario.
