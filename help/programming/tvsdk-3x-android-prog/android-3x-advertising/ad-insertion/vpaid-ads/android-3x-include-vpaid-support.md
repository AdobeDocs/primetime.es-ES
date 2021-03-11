---
description: Para agregar compatibilidad con VPAID 2.0, agregue una vista de anuncio personalizada y oyentes adecuados.
title: Implementación de la integración con VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---


# Implementación de la integración de VPAID 2.0 {#implement-vpaid-integration}

Para agregar compatibilidad con VPAID 2.0, agregue una vista de anuncio personalizada y oyentes adecuados.

1. Agregue la vista de anuncio personalizada a la interfaz del reproductor cuando el reproductor esté en estado PREPARADO.

   ```java
   ... 
   private FrameLayout _playerFrame; 
       ... 
       case PREPARED: 
           ... 
           addCustomView(); 
   ... 
   private void addCustomView() { 
       ... 
       WebView view = (WebView)_mediaPlayer.getCustomAdView(); 
       ... 
       _playerFrame.addView(view);
   ```

1. Cree oyentes y procese los eventos descritos en [Events](../../../../tvsdk-3x-android-prog/android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   >[!IMPORTANT]
   >
   >En un flujo de trabajo de VPAID 2.0, para las vistas de anuncios personalizadas es muy importante mantener la instancia `CustomAdView` entre `AdBreak` inicios (evento `AD_BREAK_START`) y `AdBreak` finalizaciones (evento `AD_BREAK_COMPLETE`), desde el momento en que crea la vista de anuncios personalizada hasta el momento en que la elimina. Es decir, no cree una vista de anuncio personalizada en cada inicio de pausa publicitaria y elimínela en cada finalización de pausa publicitaria.
   >
   >
   >Además, solo debe crear la vista de anuncio personalizada cuando el reproductor esté en estado PREPARADO,
   >
   >
   >Elimine solo la vista de publicidad personalizada cuando se llama a restablecer . Por ejemplo:
   >
   >
   ```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >
   >```
   >
   >Finalmente, antes de eliminar la vista de publicidad personalizada, debe eliminarla de `FrameLayout`. Por ejemplo:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
