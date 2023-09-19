---
description: Cuando los metadatos DRM de un vídeo son independientes del flujo de medios, realice la autenticación antes de comenzar la reproducción.
title: Autenticación DRM antes de la reproducción
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Autenticación DRM antes de la reproducción {#drm-authentication-before-playback}

Cuando los metadatos DRM de un vídeo son independientes del flujo de medios, realice la autenticación antes de comenzar la reproducción.

Un recurso de vídeo puede tener asociado un archivo de metadatos DRM. Por ejemplo:

* &quot;url&quot;: &quot;ht<span></span>tps://www.domain.com/asset.m3u8&quot;
* &quot;drmMetadata&quot;: &quot;ht<span></span>tps://www.domain.com/asset.metadata&quot;

Cuando este sea el caso, utilice `DRMHelper` métodos para descargar el contenido del archivo de metadatos DRM, analizarlo y comprobar si se necesita autenticación DRM.

1. Uso `loadDRMMetadata` para cargar el contenido de la URL de metadatos y analizar los bytes descargados en una `DRMMetadata`.

   Como cualquier otra operación de red, este método es asincrónico y crea su propio subproceso.

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

1. Como la operación es asincrónica, es aconsejable que el usuario sea consciente de ello. De lo contrario, se preguntará por qué su reproducción no está empezando. Por ejemplo, mostrar una rueda giratoria mientras se descargan y analizan los metadatos de DRM.
1. Implementar las llamadas de retorno en `DRMLoadMetadataListener`. El `loadDRMMetadata` llama a estos controladores de eventos (envía estos eventos).

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
   * `onLoadMetadataUrlComplete` detecta cuándo ha terminado de cargarse la dirección URL de metadatos.
   * `onLoadMetadataUrlError` indica que los metadatos no se han podido cargar.

1. Cuando finalice la carga, inspeccione el `DRMMetadata` para ver si es necesaria la autenticación DRM.

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

1. Si no se necesita autenticación, inicie la reproducción.
1. Si se necesita autenticación, realice la autenticación adquiriendo la licencia.

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

   Este ejemplo, para simplificar, codifica explícitamente el nombre y la contraseña del usuario.

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

1. Esto también implica comunicación de red, por lo que también es una operación asincrónica. Utilice un detector de eventos para comprobar el estado de autenticación.

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
1. Si la autenticación no se realiza correctamente, notifique al usuario y no inicie la reproducción.

La aplicación debe gestionar cualquier error de autenticación. Si no se autentica correctamente antes de reproducir, TVSDK se coloca en un estado de error. Es decir, cambia su estado a ERROR, se genera un error que contiene el código de error de la biblioteca DRM y se detiene la reproducción. La aplicación debe resolver el problema, restablecer el reproductor y volver a cargar el recurso.
