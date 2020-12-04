---
description: Cuando los metadatos DRM de un vídeo se incluyen en el flujo de medios, puede realizar la autenticación durante la reproducción.
seo-description: Cuando los metadatos DRM de un vídeo se incluyen en el flujo de medios, puede realizar la autenticación durante la reproducción.
seo-title: Autenticación DRM durante la reproducción
title: Autenticación DRM durante la reproducción
uuid: b3ff8edd-a3d4-470e-8899-580eca9fff4a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Autenticación DRM durante la reproducción {#drm-authentication-during-playback}

Cuando los metadatos DRM de un vídeo se incluyen en el flujo de medios, puede realizar la autenticación durante la reproducción.

Con la rotación de licencias, un recurso se cifra con varias licencias de DRM. Cada vez que se descubren nuevos metadatos DRM, se utilizan los métodos `DRMHelper` para comprobar si los metadatos DRM requieren autenticación DRM.

>[!TIP]
>
>Antes de iniciar la reproducción, determine si está trabajando con una licencia enlazada a dominio y si se requiere autenticación de dominio. Si es así, complete la autenticación de dominio y únase al dominio.

1. Cuando se descubren nuevos metadatos DRM en un recurso, se distribuye un evento en la capa de la aplicación.

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
       @Override 
       public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           ... 
       } 
   };
   ```

1. Use `DRMMetadata` para comprobar si se necesita autenticación.

   * Si no se requiere autenticación, no es necesario que haga nada y la reproducción continúa sin interrupciones.
   * Si se requiere autenticación, complete la autenticación DRM.

      Dado que esta operación es asincrónica y se gestiona en un subproceso diferente, no afecta a la interfaz de usuario ni a la reproducción de vídeo.

1. Si falla la autenticación, el usuario no puede continuar viendo el vídeo y la reproducción se detiene.

<!--<a id="example_939B95F831A245869F9248E2767F260C"></a>-->

Por ejemplo:

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo =  
          drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null ||  
          !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the  
        // current player time and the DRM metadata start time. For the time being,  
        // we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences =  
          PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
        String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
                ... 
            } 
 
            @Override 
            public void onAuthenticationError(int major,  
                                              int minor,  
                                              String erroString,  
                                              String serverErrorURL) { 
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

