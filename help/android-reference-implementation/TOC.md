---
cloud: experience-cloud
product: primetime
audience: end-user
user-guide-title: Primetime Reference Implementation Help
translation-type: tm+mt
source-git-commit: abcbe6991d9a024f62554c3b5ec057f9b3c71c53

---


# Implementación de referencia de PSDK 1.4 para Android {#reference-implementation}

+ [Información general de implementación de referencia de Android](home.md)
+ Implementación de referencia de Primetime {#reference}
   + [Cómo utilizar la implementación de referencia de Primetime](ref-implementation/how-to-use-ref-player.md)
   + [Estructura de implementación de referencia](ref-implementation/ref-player-structure.md)
   + Cómo utilizar los administradores de funciones {#feature-managers}
      + [Cómo utilizar los administradores de funciones](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [Creando administradores de funciones pasando la información de configuración a MediaPlayer...](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [Activación o desactivación de funciones mediante ManagerFactory](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [Gestión de eventos](ref-implementation/using-feature-managers/handling-events.md)
   + Configure el entorno de desarrollo {#setup-dev}
      + [Configure el entorno de desarrollo](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [Descargar y configurar software de requisitos previos](set-up-dev-environment/download-prereqs-android.md)
      + [Genere la implementación de referencia de Primetime](set-up-dev-environment/install-the-ref-player-project.md)
   + Explorar el código {#explore-code}
      + [PlayerFragment](set-up-dev-environment/exploring-code/player-fragment.md)
      + [Administradores de funciones](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [ConfigProvider](set-up-dev-environment/exploring-code/config-provider.md)
      + [ConfiguraciónActividad](set-up-dev-environment/exploring-code/settings-activity.md)
      + [Formato del catálogo](set-up-dev-environment/exploring-code/catalog-format.md)
      + [Objeto JSON para anuncios Primetime](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [Objeto JSON para saltos de publicidad directos](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [Objeto JSON para marcadores de publicidad personalizados](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [Objeto JSON para el ID de recurso de asignación de derechos](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [Ejemplo de formato de fuente JSON](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + Implementación de la reproducción de vídeo {#implement-video}
      + [Operaciones esenciales de reproducción de vídeo](implement-video-playback/video-playback.md)
      + [Habilitar la reproducción de vídeo](implement-video-playback/enable-video-playback.md)
      + [Protección de contenido DRM](implement-video-playback/content-protection.md)
   + [Varias velocidades de bits](implement-video-playback/mbr.md)
   + Configurar un reproductor para la reproducción de DVR con anuncios {#dvr}
      + [DVR sin inserción de anuncio](implement-video-playback/dvr/dvr-without-ad-insertion.md)
      + [DVR con inserción de anuncios](implement-video-playback/dvr/dvr-with-ad-insertion.md)
      + [Elección de un punto de partida personalizado para DVR](implement-video-playback/dvr/dvr-custom-start-point.md)
      + [Establecer una hora de inicio personalizada en la implementación de referencia](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [Mostrar estadísticas de dispositivos y reproducción de QoS](implement-video-playback/qos-statistics.md)
   + Insertar publicidades {#insert-ads}
      + [Inserción de publicidad](insert-ads/ad-insertion.md)
      + [Tipos de inserción de publicidad](insert-ads/ad-insertion-types.md)
      + [Agregar publicidad](insert-ads/add-advertising.md)
      + [Documentación de API relacionada](insert-ads/aps-callbacks-ad-insertion.md)
   + Enlace tardío de audio {#late-binding-audio}
      + [Información general](late-binding-audio/late-binding-audio-overview.md)
      + [Integrar audio de enlace tardío](late-binding-audio/aa-enable.md)
      + [Seleccionar las pistas de audio](late-binding-audio/select-audio-tracks.md)
      + [Documentación de API relacionada](late-binding-audio/aa-api-callbacks.md)
   + Flujos de asignación de autenticación Primetime {#primetime-authentications}
      + [Información general](paytvpass-entitlement/paytvpass-entitlement-overview.md)
      + [Información general de Entitlement Manager](paytvpass-entitlement/entitlement-overvivew.md)
      + [Integración de la autenticación Primetime](paytvpass-entitlement/integrate-pass.md)
      + [Configurar informes de Adobe Analytics](paytvpass-entitlement/pass-analytics-setup.md)
      + [Documentación de API relacionada](paytvpass-entitlement/pass-apis-callbacks.md)
   + Análisis de vídeo {#video-analytics}
      + [Análisis de vídeo](video-analytics/video-analytics-overview.md)
      + [Creación del Administrador de análisis de vídeo](video-analytics/create-video-analytics-manager.md)
      + [Configurar Video Analytics](video-analytics/configure-video-analytics-manager.md)
      + [Documentación de API relacionada](video-analytics/va-apis-callbacks.md)
   + [Creación de una interfaz de usuario personalizada](build-custom-ui.md)
   + [Resolución de problemas](troubleshooting.md)
