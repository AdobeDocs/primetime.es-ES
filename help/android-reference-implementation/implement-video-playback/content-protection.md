---
description: El reproductor Primetime admite la integración de DRM Primetime como flujos de trabajo de DRM personalizados. Esto significa que la aplicación debe implementar los flujos de trabajo de autenticación DRM antes de reproducir el flujo.
seo-description: El reproductor Primetime admite la integración de DRM Primetime como flujos de trabajo de DRM personalizados. Esto significa que la aplicación debe implementar los flujos de trabajo de autenticación DRM antes de reproducir el flujo.
seo-title: Protección de contenido DRM
title: Protección de contenido DRM
uuid: 95c446f6-8304-4d70-9bef-7368b9364025
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Protección de contenido DRM {#drm-content-protection}

El reproductor Primetime admite la integración de DRM Primetime como flujos de trabajo de DRM personalizados. Esto significa que la aplicación debe implementar los flujos de trabajo de autenticación DRM antes de reproducir el flujo.

Para activarlo, TVSDK le proporciona el administrador de DRM para la autenticación. La implementación de referencia proporciona un ejemplo de los siguientes flujos de trabajo:

* Cómo cargar y reproducir flujos HLS con la protección de contenido de Access, optimizada para tasas de error bajas e inicio rápido.
* Cómo cargar y reproducir flujos HLS con protección de contenido AES128.
* Cómo cargar y reproducir flujos HLS con protección de contenido PHLS, optimizada para tasas de error bajas y rápido inicio.

Todas las bibliotecas DRM integradas en el TVSDK gestionan automáticamente el contenido protegido por DRM. Sin embargo, puede exponer la gestión de errores, la optimización de la individualización del dispositivo y la adquisición de licencias mediante las rellamadas de la API de TVSDK.

## Agregar protección de contenido al reproductor {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

Puede agregar protección de contenido al reproductor creando un administrador de reproducción o utilizando el administrador de fábrica.

Para crear un administrador de protección de contenido:

* Inicialice el sistema DRM.

   En el siguiente ejemplo de código se muestra la llamada `loadDRMServices` en la función de la aplicación `onCreate()` , para asegurarse de que se inicia la inicialización necesaria para el sistema DRM antes de iniciar la reproducción.

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* Precargue las licencias de DRM.

   El siguiente ejemplo de código muestra la carga `VideoItems` cuando la lista de contenido ha terminado de cargarse. Esto hará que las licencias DRM se adquieran del servidor de licencias y se almacenen en caché localmente, de modo que cuando se inicie la reproducción, el contenido se cargue con el mínimo retraso.

   ```java
   DrmManager.preLoadDrmLicenses(item.getUrl(),  
     new MediaPlayerItemLoader.LoaderListener() { 
   
       @Override 
       public void onLoadComplete(MediaPlayerItem item) { 
           Player.logger.w(LOG_TAG + "::DRMPreload#onLoadComplete", item.getResource().getUrl()); 
       } 
   
       @Override 
       public void onError(MediaErrorCode errorCode, String s) { 
           Player.logger.e(LOG_TAG + "::DRMPreload#onError", s); 
       } 
   } 
   ```

   >[!NOTE]
   >
   >Puede establecer las licencias DRM de Precache en ON en la interfaz de usuario de Configuración para almacenar previamente las licencias DRM al cargar contenido. Sin embargo, se recomienda cargar previamente un elemento específico en lugar de almacenar todas las licencias del catálogo en la caché previa.
   >
   >![](assets/precache-drm-licenses.jpg)

* Para utilizar `ManagerFactory` la implementación de la gestión de errores de DRM, asegúrese de que la siguiente línea de código se encuentra en el [!DNL PlayerFragment.java] archivo:

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**Documentación de API relacionada**

* [Clase DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)