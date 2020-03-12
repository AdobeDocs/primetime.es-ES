---
description: Cuando los metadatos DRM de un vídeo están separados del flujo multimedia, debe autenticarse antes de iniciar la reproducción.
seo-description: Cuando los metadatos DRM de un vídeo están separados del flujo multimedia, debe autenticarse antes de iniciar la reproducción.
seo-title: Autenticación DRM antes de la reproducción
title: Autenticación DRM antes de la reproducción
uuid: be319b04-a506-4278-8275-db32cd3f18aa
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Autenticación DRM antes de la reproducción {#drm-authentication-before-playback}

Cuando los metadatos DRM de un vídeo están separados del flujo multimedia, debe autenticarse antes de iniciar la reproducción.

Un recurso de vídeo puede tener asociado un archivo de metadatos DRM, por ejemplo:

* `"url": "https://www.domain.com/asset.m3u8"`
* `"drmMetadata": "https://www.domain.com/asset.metadata"`

En este ejemplo, puede utilizar `DRMHelper` métodos para descargar el contenido del archivo de metadatos DRM, analizarlo y comprobar si es necesaria la autenticación DRM.

1. Se utiliza `loadDRMMetadata` para cargar el contenido de la URL de metadatos y analizar los bytes descargados en un `DRMMetadata`.

   >[!TIP]
   >
   >Este método es asincrónico y crea su propio subproceso.

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   Por ejemplo:

   ```java
   DRMHelper.loadDRMMetadata(drmManager,  
                                      metadataURL,  
                                      new DRMLoadMetadataListener());
   ```

1. Notifique al usuario que esta operación es asincrónica; es recomendable que lo sepa.

   Si los usuarios no saben que la operación es asincrónica, es posible que se pregunten por qué la reproducción no se ha iniciado aún. Por ejemplo, puede mostrar una rueda giratoria mientras se descargan y analizan los metadatos DRM.

1. Implemente las rellamadas en la `DRMLoadMetadataListener`.

       La función &quot;loadDRMMetadata&quot; llama a estos controladores de eventos.
       
 &quot;java     interfaz
 pública DRMLoadMetadataListener {     
     
     public void onLoadMetadataUrlStart();
       
     /**
     * @param authNeeded
     * si se necesita autenticación DRM.
       * @param drmMetadata
     * obtuvo la DRMMetadata analizada.    */
     public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata);
       public void onLoadMetadataUrlError();
       }
     
     &quot;
     
     A continuación se proporcionan más detalles sobre los controladores:
   
   * `onLoadMetadataUrlStart` detecta cuándo ha comenzado la carga de la URL de metadatos.
   * `onLoadMetadataUrlComplete` detecta cuándo ha terminado de cargarse la URL de metadatos.
   * `onLoadMetadataUrlError` indica que los metadatos no se han podido cargar.

1. Una vez completada la carga, inspeccione el `DRMMetadata` objeto para determinar si se requiere autenticación DRM.

   ```java
   public static boolean isAuthNeeded(DRMMetadata drmMetadata);
   ```

   Por ejemplo:

   ```java
   @Override 
   public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata) {  
       Log.i(LOG_TAG + "#onLoadMetadataUrlComplete",  
             "Loaded metadata URL contents. Auth needed:" + authNeeded + "."); 
       if (!authNeeded) { 
           // Auth is not required. Start player activity.     
           showLoadingSpinner(false);     
           startPlayerActivity(ASSET_URL); 
           return; 
       } 
   } 
   ```

1. Lleve a cabo una de las siguientes tareas:

   * Si no se requiere autenticación, comience la reproducción.
   * Si se requiere autenticación, complete la autenticación adquiriendo la licencia.

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
      */ 
      public static void performDrmAuthentication( 
           final DRMManager drmManager,  
           final DRMMetadata drmMetadata, 
           final String authUser,  
           final String authPass,  
           final DRMAuthenticationListener authenticationListener);
      ```

      En este ejemplo, para simplificar, el nombre y la contraseña del usuario se codifican explícitamente:

      ```java
      DRMHelper.performDrmAuthentication(drmManager,  
                                         drmMetadata,  
                                         DRM_USERNAME,  
                                         DRM_PASSWORD, new DRMAuthenticationListener() { 
          @Override 
          public void onAuthenticationStart() { 
              Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
              // Spinner is already showing. 
          } 
          @Override 
          public void onAuthenticationError(int major,  
                                            int minor,  
                                            String errorString,  
                                            String serverErrorURL) { 
              Log.e(LOG_TAG +  
                    "#onAuthenticationError",  
                    "DRM authentication failed. " +  
                    major + " 0x" + Long.toHexString(minor)); 
              showToast(getString(R.string.drmAuthenticationError));   
              showLoadingSpinner(false); 
          } 
          @Override 
          public void onAuthenticationComplete(byte[] authenticationToken) { 
              Log.i(LOG_TAG +  
                    "#onAuthenticationComplete", "Auth successful. Launching content."); 
              showLoadingSpinner(false); 
              startPlayerActivity(ASSET_URL); 
          } 
      }); 
      ```

1. Use un detector de eventos para comprobar el estado de autenticación.

   Este proceso implica una comunicación de red, por lo que también es una operación asincrónica.

   ```java
   public interface DRMAuthenticationListener { 
       /** 
       * Called to indicate that DRM authentication has started. 
       */ 
       public void onAuthenticationStart(); 
       /** 
       * Called to indicate that DRM authentication has been successful. 
       * 
       * @param authenticationToken 
       * the obtained token, which can be stored locally. 
       */ 
       public void onAuthenticationComplete(byte[] authenticationToken); 
       /** 
       * Called to indicate that an error occurred while performing the DRM 
       * authentication. 
       * 
       * @param major 
       * the major code. 
       * @param minorC 
       * the minor code. 
       * @param errorString 
       * the exception thrown. 
       * @param serverErrorURL 
       * the URL of the server  
       * on which the error occurred 
       */ 
       public void onAuthenticationError(int major,  
                                         int minor,  
                                         String errorString,  
                                         String serverErrorURL); 
   } 
   ```

1. Si la autenticación se realiza correctamente, inicie la reproducción.
1. Si la autenticación no se realiza correctamente, notifíquelo al usuario y no inicie la reproducción.

   La aplicación debe gestionar cualquier error de autenticación. Al no autenticarse correctamente antes de reproducir, TVSDK se encuentra en un estado de error y la reproducción se detiene. La aplicación debe resolver el problema, restablecer el reproductor y volver a cargar el recurso.