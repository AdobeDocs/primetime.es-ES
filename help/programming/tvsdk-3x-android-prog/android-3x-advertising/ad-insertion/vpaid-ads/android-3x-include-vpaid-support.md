---
description: Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.
seo-description: Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.
seo-title: Implementación de la integración con VPAID 2.0
title: Implementación de la integración con VPAID 2.0
uuid: d512fb5b-001c-4a7a-a553-d5962002bb30
translation-type: tm+mt
source-git-commit: 83df68905f74931355264661aed6cff43b802d3f

---


# Implementación de la integración con VPAID 2.0 {#implement-vpaid-integration}

Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.

1. Añada la vista de publicidad personalizada en la interfaz del reproductor cuando éste se encuentre en el estado PREPARADO.

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

1. Cree oyentes y procese los eventos descritos en [Eventos](../../../../tvsdk-3x-android-prog/android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   >[!IMPORTANT]
   >
   >En un flujo de trabajo de VPAID 2.0, para las vistas de publicidad personalizadas es muy importante mantener la `CustomAdView` instancia entre `AdBreak` inicios (evento `AD_BREAK_START`) y `AdBreak` finalizaciones (evento `AD_BREAK_COMPLETE`), desde el momento en que crea la vista de publicidad personalizada hasta el momento en que la elimina. Es decir, no cree una vista de publicidad personalizada en cada inicio de pausa publicitaria y elimínelo en cada pausa publicitaria completada.
   >
   >
   >Además, solo debe crear la vista de publicidad personalizada cuando el reproductor esté en el estado PREPARADO,
   >
   >
   >Solo debe deshacerse de la vista de publicidad personalizada cuando se llame a reset. Por ejemplo:
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
   >Por último, antes de eliminar la vista de publicidad personalizada, debe eliminarla del `FrameLayout`. Por ejemplo:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
