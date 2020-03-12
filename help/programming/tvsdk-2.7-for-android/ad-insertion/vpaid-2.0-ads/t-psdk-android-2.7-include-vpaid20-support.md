---
description: Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.
seo-description: Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.
seo-title: Implementación de la integración con VPAID 2.0
title: Implementación de la integración con VPAID 2.0
uuid: fa5b9cdd-e684-4656-91b7-50781dc59e23
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Implementación de la integración con VPAID 2.0 {#implement-vpaid-integration}

Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.

Para agregar compatibilidad con VPAID 2.0:

1. Agregue la vista de publicidad personalizada a la interfaz del reproductor cuando el reproductor esté en el estado PREPARADO.

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

1. Cree oyentes y procese los eventos descritos en los oyentes de eventos.

   >[!IMPORTANT]
   >
   >En un flujo de trabajo de VPAID 2.0, para las vistas de publicidad personalizadas es muy importante mantener la `CustomAdView` instancia entre `AdBreak` inicios (evento `AD_BREAK_START`) y `AdBreak` finalizaciones (evento `AD_BREAK_COMPLETE`), desde el momento en que se crea la vista de publicidad personalizada hasta el momento en que se elimina. Es decir, no cree una vista de publicidad personalizada en cada inicio de pausa publicitaria y elimínelo en cada desglose de publicidad completado.
   >
   >
   >Además, solo debe crear la vista de publicidad personalizada cuando el reproductor esté en estado PREPARADO,
   >
   >
   >Solo debe deshacerse de la vista de publicidad personalizada cuando se llame a reset. Por ejemplo:    >
   >
   >
   ```>
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >
   >
   ```   >
   >



   >Por último, antes de eliminar la vista de publicidad personalizada, debe eliminarla de la `FrameLayout`. Por ejemplo:    >
   >
   >
   ```>
   if (_playerFrame != null) 
      _playerFrame.removeAllViews(); 
   ```
