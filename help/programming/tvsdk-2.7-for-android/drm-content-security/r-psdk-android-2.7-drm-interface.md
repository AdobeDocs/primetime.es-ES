---
description: El elemento clave del lado del cliente de la solución DRM de Primetime es el Administrador de DRM. La aplicación de ejemplo que se incluye con el SDK para Android también incluye una clase DRMHelper que se puede utilizar para facilitar la implementación de determinadas operaciones de DRM.
title: Información general sobre la interfaz DRM Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Información general sobre la interfaz DRM Primetime {#primetime-drm-interface-overview}

El elemento clave del lado del cliente de la solución DRM de Primetime es el Administrador de DRM. La aplicación de ejemplo que se incluye con el SDK para Android también incluye una clase DRMHelper que se puede utilizar para facilitar la implementación de determinadas operaciones de DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM proporciona un flujo de trabajo escalable y eficaz para implementar la protección de contenido en aplicaciones TVSDK. Protege y administra los derechos del contenido de vídeo creando una licencia para cada archivo multimedia digital.

Para obtener más información, consulte el código del reproductor de muestra DRM que se incluye en el paquete TVSDK.

Estos son los elementos de API más importantes para trabajar con DRM:

* Referencia en el reproductor de contenido al objeto del administrador de DRM que implementa el subsistema de DRM:

  ```java
  MediaPlayer.getDRMManager();
  ```

  >[!TIP]
  >
  >Esta API devolverá un válido `DRMManager` objeto solo después de `MediaPlayerEvent.DRM_METADATA` está despedido. Si llama a `getDRMManager()` antes de que se active este evento, podría devolver NULL.

* El `DRMHelper` clase auxiliar, que resulta útil al implementar flujos de trabajo de DRM.
* A `DRMHelper` método de cargador de metadatos, que carga metadatos DRM cuando se encuentran en una dirección URL independiente del contenido.

  ```java
  public static void loadDRMMetadata(final DRMManager drmManager,  
     final String drmMetadataUrl,  
     final DRMLoadMetadataListener loadMetadataListener);
  ```

* A `DRMHelper` para comprobar los metadatos DRM y determinar si se requiere autenticación.

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

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obtener más información sobre DRM, consulte la [Documentación de DRM](https://helpx.adobe.com/primetime/user-guide.html).
