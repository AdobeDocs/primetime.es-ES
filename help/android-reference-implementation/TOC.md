---
product: primetime
audience: end-user
user-guide-title: Ayuda para la implementación de referencia de Primetime
user-guide-description: Ayuda a comprender el SDK de TVSDK y a modificar los administradores de funciones para personalizar su reproductor personal.
translation-type: tm+mt
source-git-commit: 95626ebde981d1996652a67bc9e0cea05f24aa6d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 7%

---


# Implementación de referencia de PSDK 1.4 para Android {#reference-implementation}

+ [Información general sobre la implementación de referencia de Android](home.md)
+ Implementación de referencia de Primetime {#reference}
   + [Cómo utilizar la implementación de referencia de Primetime](ref-implementation/how-to-use-ref-player.md)
   + [Estructura de implementación de referencia](ref-implementation/ref-player-structure.md)
   + Cómo usar los administradores de funciones {#feature-managers}
      + [Cómo utilizar los administradores de funciones](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [Creando administradores de funciones pasando información de configuración a MediaPlayer...](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [Activar o desactivar las funciones mediante ManagerFactory](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [Gestión de eventos](ref-implementation/using-feature-managers/handling-events.md)
   + Configure el entorno de desarrollo {#setup-dev}
      + [Configuración del entorno de desarrollo](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [Descargar y configurar software de requisitos previos](set-up-dev-environment/download-prereqs-android.md)
      + [Generar la implementación de referencia de Primetime](set-up-dev-environment/install-the-ref-player-project.md)
   + Explorar el código {#explore-code}
      + [Fragmento del reproductor](set-up-dev-environment/exploring-code/player-fragment.md)
      + [Administradores de funciones](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [ConfigProvider](set-up-dev-environment/exploring-code/config-provider.md)
      + [ConfiguraciónActividad](set-up-dev-environment/exploring-code/settings-activity.md)
      + [Formato del catálogo](set-up-dev-environment/exploring-code/catalog-format.md)
      + [Objeto JSON para anuncios de Primetime](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [Objeto JSON para pausas publicitarias directas](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [Objeto JSON para marcadores de anuncios personalizados](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [Objeto JSON para el ID de recurso de derecho](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [Ejemplo de formato de fuente JSON](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + Implementación de la reproducción de vídeo {#implement-video}
      + [Operaciones esenciales de reproducción de vídeo](implement-video-playback/video-playback.md)
      + [Habilitar la reproducción de vídeo](implement-video-playback/enable-video-playback.md)
      + [Protección de contenido DRM](implement-video-playback/content-protection.md)
   + [Varias tasas de bits](implement-video-playback/mbr.md)
   + Configurar un reproductor para la reproducción de DVR con anuncios {#dvr}
      + [DVR sin inserción de anuncio](implement-video-playback/dvr/dvr-without-ad-insertion.md)
      + [DVR con inserción de anuncios](implement-video-playback/dvr/dvr-with-ad-insertion.md)
      + [Elección de un punto de partida personalizado para DVR](implement-video-playback/dvr/dvr-custom-start-point.md)
      + [Establecer una hora de inicio personalizada en la implementación de referencia](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [Mostrar las estadísticas de dispositivo y reproducción de QoS](implement-video-playback/qos-statistics.md)
   + Insertar anuncios {#insert-ads}
      + [Inserción de publicidad](insert-ads/ad-insertion.md)
      + [Tipos de inserción de publicidad](insert-ads/ad-insertion-types.md)
      + [Agregar publicidad](insert-ads/add-advertising.md)
      + [Documentación de API relacionada](insert-ads/aps-callbacks-ad-insertion.md)
   + Audio de enlace tardío {#late-binding-audio}
      + [Información general](late-binding-audio/late-binding-audio-overview.md)
      + [Integración del audio de enlace tardío](late-binding-audio/aa-enable.md)
      + [Seleccionar las pistas de audio](late-binding-audio/select-audio-tracks.md)
      + [Documentación de API relacionada](late-binding-audio/aa-api-callbacks.md)
   + Flujos de derechos de autenticación de Primetime {#primetime-authentications}
      + [Información general](paytvpass-entitlement/paytvpass-entitlement-overview.md)
      + [Información general del administrador de derechos](paytvpass-entitlement/entitlement-overvivew.md)
      + [Integración de la autenticación de Primetime](paytvpass-entitlement/integrate-pass.md)
      + [Configuración de informes de Adobe Analytics](paytvpass-entitlement/pass-analytics-setup.md)
      + [Documentación de API relacionada](paytvpass-entitlement/pass-apis-callbacks.md)
   + Video Analytics {#video-analytics}
      + [Video Analytics](video-analytics/video-analytics-overview.md)
      + [Creación del administrador de Video Analytics](video-analytics/create-video-analytics-manager.md)
      + [Configurar Video Analytics](video-analytics/configure-video-analytics-manager.md)
      + [Documentación de API relacionada](video-analytics/va-apis-callbacks.md)
   + [Creación de una interfaz de usuario personalizada](build-custom-ui.md)
   + [Resolución de problemas](troubleshooting.md)
