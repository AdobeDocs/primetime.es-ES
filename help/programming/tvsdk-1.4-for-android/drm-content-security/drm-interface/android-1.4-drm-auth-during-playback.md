---
description: Cuando los metadatos DRM de un vídeo se incluyen en el flujo de medios, realice la autenticación durante la reproducción.
title: Autenticación DRM durante la reproducción
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Autenticación DRM durante la reproducción {#drm-authentication-during-playback}

Cuando los metadatos DRM de un vídeo se incluyen en el flujo de medios, realice la autenticación durante la reproducción.

Considere la función de rotación de licencias, en la que un recurso se cifra con varias licencias DRM. Cada vez que se descubran nuevos metadatos DRM, utilice `DRMHelper` métodos para comprobar si los metadatos DRM requieren autenticación DRM.

>[!NOTE]
>
>Este tutorial no gestiona licencias enlazadas a dominios. Lo ideal es que, antes de iniciar la reproducción, compruebe si está tratando con una licencia enlazada a un dominio. Si es así, realice la autenticación de dominios (si es necesario) y únase al dominio.

1. Cuando se descubren nuevos metadatos DRM en un recurso, se envía un evento en la capa de aplicación.

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
           @Override 
           public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           } 
   };
   ```

1. Utilice el `DRMMetadata` para comprobar si es necesaria la autenticación. Si no es así, no haga nada; la reproducción continúa sin interrupciones.
1. De lo contrario, realice la autenticación DRM. Dado que esta operación es asíncrona y se gestiona en un subproceso diferente, no afecta a la interfaz de usuario ni a la reproducción de vídeo.
1. Si la autenticación falla, el usuario no puede seguir viendo el vídeo y la reproducción termina. De lo contrario, la reproducción continuará ininterrumpidamente.

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo = drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the current player time and the 
        // DRM metadata start time. For the time being, we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
          String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
            } 
 
            @Override 
            public void onAuthenticationError(int major, int minor, String erroString, String serverErrorURL) { 
                if (getActivity() == null) { 
                    return; 
                } 
                _handler.post(new Runnable() { 
                    @Override 
                    public void run() { 
                        showToast(getString(R.string.drmAuthenticationError)); 
                        getActivity().finish(); 
                    } 
                }); 
            } 
 
            @Override 
            public void onAuthenticationComplete(byte[] authenticationToken) { 
            } 
        }); 
    } 
};
```
