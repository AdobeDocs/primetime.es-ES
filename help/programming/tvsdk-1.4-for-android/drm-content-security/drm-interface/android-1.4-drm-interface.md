---
description: Puede utilizar las funciones del sistema de Digital Rights Management Primetime (DRM) para proporcionar acceso seguro al contenido de vídeo. Alternativamente, puede utilizar soluciones DRM de terceros como una alternativa a la solución DRM integrada de Primetime de Adobe.
title: Información general sobre la interfaz de DRM de Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Información general {#primetime-drm-interface-overview}

Puede utilizar las funciones del sistema de Digital Rights Management Primetime (DRM) para proporcionar acceso seguro al contenido de vídeo. Alternativamente, puede utilizar soluciones DRM de terceros como una alternativa a la solución DRM integrada de Primetime de Adobe.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Consulte con su representante de Adobe para obtener la información más actualizada sobre la disponibilidad de soluciones DRM de terceros.

El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) de Primetime es el administrador de DRM. La aplicación de ejemplo incluida con el SDK para Android incluye una clase `DRMHelper` que muestra cómo facilitar la implementación de determinadas operaciones DRM.

Primetime DRM proporciona un flujo de trabajo escalable y eficiente para implementar la protección de contenido en aplicaciones TVSDK. Para proteger y administrar los derechos del contenido de vídeo, debe crear una licencia para cada archivo multimedia digital.

Consulte el código del reproductor de muestra de DRM incluido en el paquete TVSDK.

Estos son los elementos API más importantes para trabajar con DRM:

* Referencia en el reproductor de medios al objeto de administrador de DRM que implementa el subsistema DRM:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >Esta API devolverá un objeto `DRMManager` válido solo después de activar `MediaPlayerEvent.DRM_METADATA`. Si llama a `getDRMManager()` antes de que se active este evento, es posible que devuelva NULL.

* La clase de ayuda `DRMHelper`, que resulta útil al implementar flujos de trabajo de DRM.

   Puede ver `DRMHelper` en `ReferencePlayer`.

* Un método de carga de metadatos `DRMHelper`, que carga los metadatos DRM cuando se encuentran en una dirección URL independiente del contenido.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* Un método `DRMHelper` para comprobar los metadatos de DRM para determinar si se necesita autenticación.

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

* Eventos que notifican a la aplicación sobre varias actividades y estados de DRM.

<!--<a id="section_899BD9061D484E1BBA46E84617C36867"></a>-->

Elementos de API relevantes adicionales:

* [com.adobe.ave.drm.DRMManager](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMManager.html)
* [com.adobe.ave.drm.DRMMetdata](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMMetadata.html)
* [com.adobe.ave.drm.DRMPolicy](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMPolicy.html)
* [com.adobe.ave.drm.DRMAuthauthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationMethod.html)
* [com.adobe.ave.drm.DRMAuthauthenticationCompleteCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationCompleteCallback.html)
* [com.adobe.ave.drm.DRMOperationErrorCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMOperationErrorCallback.html)
* com.adobe.mediacore.drm.DRMAuthenticateListener

<!-- 
Comment Type: draft
(https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/drm/DRMAuthenticateListener.html)

-->
<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obtener más información sobre DRM, consulte la [documentación de Adobe Primetime DRM](https://helpx.adobe.com/primetime/user-guide.html).
