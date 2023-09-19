---
description: Puede utilizar las funciones del sistema de Digital Rights Management de Primetime (DRM) para proporcionar acceso seguro al contenido de vídeo. Como alternativa, puede utilizar soluciones de DRM de terceros como alternativa a la solución de DRM de Primetime integrada de Adobe.
title: Información general sobre la interfaz DRM Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Información general {#primetime-drm-interface-overview}

Puede utilizar las funciones del sistema de Digital Rights Management de Primetime (DRM) para proporcionar acceso seguro al contenido de vídeo. Como alternativa, puede utilizar soluciones de DRM de terceros como alternativa a la solución de DRM de Primetime integrada de Adobe.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Consulte con su representante de Adobes la información más actualizada sobre la disponibilidad de soluciones de DRM de terceros.

El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) de Primetime es el Administrador de DRM. La aplicación de ejemplo incluida con el SDK para Android incluye una `DRMHelper` que muestra cómo hacer que ciertas operaciones de DRM sean más fáciles de implementar.

Primetime DRM proporciona un flujo de trabajo escalable y eficaz para implementar la protección de contenido en aplicaciones TVSDK. Protege y administra los derechos del contenido de vídeo creando una licencia para cada archivo multimedia digital.

Consulte el código del reproductor de muestras DRM incluido en el paquete TVSDK.

Estos son los elementos de API más importantes para trabajar con DRM:

* Referencia en el reproductor de contenido al objeto del administrador de DRM que implementa el subsistema de DRM:

  ```java
  MediaPlayer.getDRMManager();
  ```

  >[!TIP]
  >
  >Esta API devolverá un válido `DRMManager` objeto solo después de `MediaPlayerEvent.DRM_METADATA` está despedido. Si llama a `getDRMManager()` antes de que se active este evento, podría devolver NULL.

* El `DRMHelper` clase auxiliar, que resulta útil al implementar flujos de trabajo de DRM.

  Puede ver `DRMHelper` in `ReferencePlayer`.

* A `DRMHelper` método de cargador de metadatos, que carga metadatos DRM cuando se encuentran en una dirección URL independiente del contenido.

  ```java
  public static void loadDRMMetadata(final DRMManager drmManager,  
     final String drmMetadataUrl,  
     final DRMLoadMetadataListener loadMetadataListener);
  ```

* A `DRMHelper` para comprobar los metadatos DRM y determinar si es necesaria la autenticación.

  ```java
  /** 
  * Return whether authentication is needed for the provided 
  * DRMMetadata. 
  * 
  * @param drmMetadata 
  * The desired DRMMetadata on which to check whether auth is needed. 
  * @return whether authentication is required for the provided metadata 
  */ 
  public static boolean isAuthNeeded(DRMMetadata drmMetadata);
  ```

* `DRMHelper` método para realizar la autenticación.

  ```java
  /** 
  * Helper method to perform DRM authentication. 
  * 
  * @param drmManager 
  * the DRMManager, used to perform the authentication. 
  * @param drmMetadata 
  * the DRMMetadata, containing the DRM specific information. 
  * @param authenticationListener 
  * the listener, on which the user can be notified about the 
  * authentication process status. 
  * @param authUser 
  * the DRM username provider by the user. 
  * @param authPass 
  * the DRM password provided by the user. 
  */ 
  public static void performDrmAuthentication(final DRMManager drmManager,  
  final DRMMetadata drmMetadata,  
  final String authUser,  
  final String authPass,  
  final DRMAuthenticationListener authenticationListener);
  ```

* Eventos que notifican a la aplicación sobre diversas actividades y estados de DRM.

<!--<a id="section_899BD9061D484E1BBA46E84617C36867"></a>-->

Elementos de API adicionales relevantes:

* [com.adobe.ave.drm.DRManager](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMManager.html)
* [com.adobe.ave.drm.DRMMetdata](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMMetadata.html)
* [com.adobe.ave.drm.DRMPolicy](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMPolicy.html)
* [com.adobe.ave.drm.DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationMethod.html)
* [com.adobe.ave.drm.DRMAuthenticationCompleteCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationCompleteCallback.html)
* [com.adobe.ave.drm.DRMOperationErrorCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMOperationErrorCallback.html)
* com.adobe.mediacore.drm.DRMAuthenticateListener

<!-- 
Comment Type: draft
(https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/drm/DRMAuthenticateListener.html)

-->
<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obtener más información sobre DRM, consulte la [Documentación de Adobe Primetime DRM](https://helpx.adobe.com/primetime/user-guide.html).
