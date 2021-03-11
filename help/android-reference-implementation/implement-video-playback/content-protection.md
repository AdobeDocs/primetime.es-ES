---
description: El reproductor Primetime es compatible con la integración de Primetime DRM como flujos de trabajo personalizados de DRM. Esto significa que la aplicación debe implementar los flujos de trabajo de autenticación DRM antes de reproducir el flujo.
title: Protección de contenido DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Protección de contenido DRM {#drm-content-protection}

El reproductor Primetime es compatible con la integración de Primetime DRM como flujos de trabajo personalizados de DRM. Esto significa que la aplicación debe implementar los flujos de trabajo de autenticación DRM antes de reproducir el flujo.

Para habilitarlo, TVSDK le proporciona el administrador de DRM para la autenticación. La implementación de referencia proporciona un ejemplo de los siguientes flujos de trabajo:

* Cómo cargar y reproducir flujos HLS con protección de contenido de Access, optimizado para tasas de error bajas e inicio rápido.
* Cómo cargar y reproducir flujos HLS con protección de contenido AES128.
* Cómo cargar y reproducir flujos HLS con protección de contenido PHLS, optimizado para tasas de error bajas y inicio rápido.

Todas las bibliotecas DRM integradas en TVSDK gestionan automáticamente el contenido protegido por DRM. Sin embargo, puede exponer la gestión de errores, la optimización de la individualización del dispositivo y la adquisición de licencias mediante llamadas de retorno de API de TVSDK.

## Agregar protección de contenido al reproductor {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

Puede añadir protección de contenido al reproductor creando un administrador de reproducción o utilizando el administrador de fábrica.

Para crear un administrador de protección de contenido:

* Inicialice el sistema DRM.

   El siguiente ejemplo de código muestra la llamada `loadDRMServices` en la función `onCreate()` de la aplicación para asegurarse de que se inicia cualquier inicialización necesaria para el sistema DRM antes de iniciar la reproducción.

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* Precargue las licencias de DRM.

   El siguiente ejemplo de código muestra la carga de `VideoItems` cuando la lista de contenido ha terminado de cargarse. Esto hará que las licencias de DRM se adquieran del servidor de licencias y se almacenen en caché localmente, de modo que cuando se inicie la reproducción, el contenido se cargue con el mínimo retraso.

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
   >Puede establecer las licencias de Precache DRM en ON en la interfaz de usuario de Configuración para almacenar en caché previamente las licencias de DRM al cargar contenido. Sin embargo, se recomienda cargar previamente un elemento específico en lugar de almacenar en caché previamente todas las licencias del catálogo.
   >
   >![](assets/precache-drm-licenses.jpg)

* Para utilizar `ManagerFactory` para implementar la gestión de errores de DRM, asegúrese de que la siguiente línea de código se encuentra en el archivo [!DNL PlayerFragment.java]:

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**Documentación de API relacionada**

* [Clase DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)