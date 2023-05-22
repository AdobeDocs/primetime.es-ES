---
description: Puede utilizar el empaquetador sin conexión de Adobe para preparar contenido para cualquiera de las soluciones de DRM admitidas por Primetime Cloud DRM, con tecnología ExpressPlay.
title: Empaquetador de Primetime/DRM en la nube/TVSDK
exl-id: 2055c18b-62de-41bf-9644-f366609e0198
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Empaquetador de Primetime/DRM en la nube/TVSDK {#primetime-packager-cloud-drm-tvsdk}

Puede utilizar el empaquetador sin conexión de Adobe para preparar contenido para cualquiera de las soluciones de DRM admitidas por Primetime Cloud DRM, con tecnología ExpressPlay.

Este conjunto de instrucciones supone que ya ha configurado una cuenta de administrador de ExpressPlay: [Inicio rápido de Primetime DRM Cloud](../../../multi-drm-workflows/quick-start/quick-overview.md).
1. Elija la infraestructura que desea utilizar para empaquetar el contenido. Primetime Packager admite el empaquetado de contenido basado en la línea de comandos y la configuración para su uso con los DRM FairPlay, Widevine y PlayReady. TVSDK admite actualmente los siguientes formatos y cifrado (con más en proceso):

   * DASH (CENC) / PlayReady, Widevine - Para HTML 5
   * HLS / FairPlay, Acceso - Para iOS

1. Elija un sistema de administración de claves (KMS):

   * Utilizar el KMS de ExpressPlay ( [Almacenamiento de claves ExpressPlay](https://www.expressplay.com/developer/key-storage/)); este sistema administra las claves de contenido mediante la API RESTful de ExpressPlay.

      o...

   * Configure su propio KMS. Cree una base de datos de claves de contenido, seleccionables por ID de contenido.

      En cualquier caso, el KMS administra un suministro de claves de contenido, y cada clave tiene un ID de contenido asociado.

1. Empaquete el contenido. Con Primetime Packager, puede empaquetar un fragmento de contenido para una solución DRM específica o para varias soluciones DRM.

   Los siguientes comandos de ejemplo muestran algunos ejemplos de contenido de paquetes para diferentes soluciones de DRM:

   * [Widevine con Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19) (genera el archivo MPD):

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

   * [FairPlay con Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) (Genera un archivo M3U8):

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
      >El `key_url` El valor de se copia tal como está en el archivo M3U8.

1. Cree un &quot;servidor de tienda&quot;.

       El servidor de tienda debe gestionar las siguientes operaciones:
   
   1. Selección del contenido por parte del cliente. Esta implementación necesita incluir un extremo para que los clientes soliciten un token de contenido para un ID de contenido específico.
   1. Derechos del cliente
   1. Solicitudes de token de licencia (ExpressPlay) del cliente ( [Referencia de respuesta/solicitud de token de licencia de ExpressPlay](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. Cree su cliente de.

       El cliente debe incluir una llamada al servidor de la tienda. El Adobe recomienda que el cliente llame a la tienda después de que el usuario seleccione algún contenido y después de que el usuario se autentique. A continuación, pase el token devuelto desde ExpressPlay a su reproductor para utilizarlo en las solicitudes de licencia. Las introducciones para implementar el componente DRM de sus reproductores se encuentran aquí:
   
   * [TVSDK del explorador para HTML5](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Con el token de licencia en la mano, el cliente ahora puede derivar la URL de solicitud del token y realizar la solicitud de licencia a ExpressPlay y luego reproducir el contenido seleccionado para el usuario.
