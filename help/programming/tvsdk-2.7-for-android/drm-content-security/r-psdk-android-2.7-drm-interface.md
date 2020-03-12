---
description: El elemento clave del lado del cliente de la solución Primetime DRM es el Administrador de DRM. La aplicación de ejemplo que se incluye con el SDK para Android también incluye una clase DRMHelper que puede utilizarse para facilitar la implementación de determinadas operaciones DRM.
seo-description: El elemento clave del lado del cliente de la solución Primetime DRM es el Administrador de DRM. La aplicación de ejemplo que se incluye con el SDK para Android también incluye una clase DRMHelper que puede utilizarse para facilitar la implementación de determinadas operaciones DRM.
seo-title: Información general sobre la interfaz de DRM de Primetime
title: Información general sobre la interfaz de DRM de Primetime
uuid: d77a98c8-c1f5-4fe3-8d0b-3d21e288f228
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Información general sobre la interfaz de DRM de Primetime {#primetime-drm-interface-overview}

El elemento clave del lado del cliente de la solución Primetime DRM es el Administrador de DRM. La aplicación de ejemplo que se incluye con el SDK para Android también incluye una clase DRMHelper que puede utilizarse para facilitar la implementación de determinadas operaciones DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM proporciona un flujo de trabajo escalable y eficaz para implementar la protección de contenido en aplicaciones TVSDK. Para proteger y administrar los derechos del contenido de vídeo, cree una licencia para cada archivo de medios digitales.

Para obtener más información, consulte el código del reproductor de muestra DRM que se incluye en el paquete TVSDK.

Estos son los elementos de API más importantes para trabajar con DRM:

* Referencia en el reproductor de medios al objeto del administrador de DRM que implementa el subsistema de DRM:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >Esta API devolverá un `DRMManager` objeto válido solo después de que se `MediaPlayerEvent.DRM_METADATA` active la opción. Si llama `getDRMManager()` antes de que se active este evento, puede que devuelva NULL.

* Clase `DRMHelper` auxiliar, que resulta útil al implementar flujos de trabajo de DRM.
* Método `DRMHelper` de cargador de metadatos que carga los metadatos DRM cuando se encuentran en una URL independiente del medio.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* Un `DRMHelper` método para comprobar los metadatos DRM y determinar si se requiere autenticación.

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

* `DRMHelper` para realizar la autenticación.

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

Para obtener más información sobre DRM, consulte la documentación [de](https://helpx.adobe.com/primetime/user-guide.html)DRM.
