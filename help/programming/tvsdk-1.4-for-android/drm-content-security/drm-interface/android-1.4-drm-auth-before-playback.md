---
description: Cuando los metadatos DRM de un vídeo están separados del flujo multimedia, realice la autenticación antes de iniciar la reproducción.
seo-description: Cuando los metadatos DRM de un vídeo están separados del flujo multimedia, realice la autenticación antes de iniciar la reproducción.
seo-title: Autenticación DRM antes de la reproducción
title: Autenticación DRM antes de la reproducción
uuid: 326ef93d-53b0-4e3a-b16d-f3b886837cc0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Autenticación DRM antes de la reproducción {#drm-authentication-before-playback}

Cuando los metadatos DRM de un vídeo están separados del flujo multimedia, realice la autenticación antes de iniciar la reproducción.

Un recurso de vídeo puede tener un archivo de metadatos DRM asociado. Por ejemplo:

* &quot;url&quot;: &quot;<span></span>https://www.domain.com/asset.m3u8&quot;
* &quot;drmMetadata&quot;: &quot;<span></span>https://www.domain.com/asset.metadata&quot;

En este caso, utilice `DRMHelper` métodos para descargar el contenido del archivo de metadatos DRM, analizarlo y compruebe si es necesaria la autenticación DRM.

1. Se utiliza `loadDRMMetadata` para cargar el contenido de la URL de metadatos y analizar los bytes descargados en un `DRMMetadata`.

   Como cualquier otra operación de red, este método es asincrónico, creando su propio subproceso.

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   Por ejemplo:

   ```java
   DRMHelper.loadDRMMetadata(drmManager, metadataURL, new DRMLoadMetadataListener());
   ```

1. Dado que la operación es asincrónica, es recomendable que el usuario esté al tanto de ello. De lo contrario, se preguntará por qué su reproducción no está empezando. Por ejemplo, muestre una rueda giratoria mientras se descargan y analizan los metadatos DRM.
1. Implemente las rellamadas en la `DRMLoadMetadataListener`. El `loadDRMMetadata` llama a estos controladores de eventos (distribuye estos eventos).

   ```java
   public interface  
    <b>DRMLoadMetadataListener</b> { 
    public void  
    <b>onLoadMetadataUrlStart</b>(); 
    /** 
     * @param authNeeded 
     * whether DRM authentication is needed. 
     * @param drmMetadata 
     * the parsed DRMMetadata obtained.    */ 
    public void  
    <b>onLoadMetadataUrlComplete</b>(boolean authNeeded, DRMMetadata drmMetadata); 
    public void  
    <b>onLoadMetadataUrlError</b>(); 
   }
   ```

   * `onLoadMetadataUrlStart` detecta cuándo ha comenzado la carga de la URL de metadatos.
   * `onLoadMetadataUrlComplete` detecta cuándo ha terminado de cargarse la URL de metadatos.
   * `onLoadMetadataUrlError` indica que los metadatos no se han podido cargar.

1. Cuando finalice la carga, inspeccione el `DRMMetadata` objeto para ver si es necesaria la autenticación DRM.

   ```java
   public static boolean <b>isAuthNeeded</b>(DRMMetadata drmMetadata);
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
   ```

1. Si no se necesita autenticación, comience la reproducción.
1. Si es necesario autenticarse, realice la autenticación adquiriendo la licencia.

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

   En este ejemplo, para simplificar, se codifica explícitamente el nombre y la contraseña del usuario.

   ```java
   DRMHelper.performDrmAuthentication(drmManager, drmMetadata, DRM_USERNAME, DRM_PASSWORD,  
     new DRMAuthenticationListener() { 
       @Override 
       public void onAuthenticationStart() { 
           Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
           // Spinner is already showing. 
       } 
       @Override 
       public void onAuthenticationError(int major, int minor, String errorString, String serverErrorURL) {  
           Log.e(LOG_TAG + "#onAuthenticationError", "DRM authentication failed. " +  
             major + " 0x" + Long.toHexString(minor)); 
           showToast(getString(R.string.drmAuthenticationError));   
           showLoadingSpinner(false); 
       } 
       @Override 
       public void onAuthenticationComplete(byte[] authenticationToken) { 
           Log.i(LOG_TAG + "#onAuthenticationComplete", "Auth successful. Launching content."); 
           showLoadingSpinner(false); 
           startPlayerActivity(ASSET_URL); 
       } 
   }); 
   ```

1. Esto también implica una comunicación de red, por lo que también es una operación asincrónica. Use un detector de eventos para comprobar el estado de autenticación.

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
       public void onAuthenticationError(int major, int minor,  
         String errorString, String serverErrorURL); 
   } 
   ```

1. Si la autenticación se realiza correctamente, inicie la reproducción.
1. Si la autenticación no se realiza correctamente, notifíquelo al usuario y no inicie la reproducción.

La aplicación debe gestionar cualquier error de autenticación. Al no autenticarse correctamente antes de reproducir, TVSDK se coloca en un estado de error. Es decir, cambia su estado a ERROR, se genera un error que contiene el código de error de la biblioteca DRM y la reproducción se detiene. La aplicación debe resolver el problema, restablecer el reproductor y volver a cargar el recurso.

