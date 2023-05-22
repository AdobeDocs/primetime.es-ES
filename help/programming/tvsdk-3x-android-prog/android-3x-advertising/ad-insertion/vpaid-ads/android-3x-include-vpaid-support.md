---
description: Para añadir compatibilidad con VPAID 2.0, agregue una vista de anuncio personalizada y los oyentes adecuados.
title: Implementación de la integración con VPAID 2.0
exl-id: a0d9a370-8fb6-4246-b59d-3b7c0b043bed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Implementación de la integración con VPAID 2.0 {#implement-vpaid-integration}

Para añadir compatibilidad con VPAID 2.0, agregue una vista de anuncio personalizada y los oyentes adecuados.

1. Añada la vista de anuncio personalizada a la interfaz del reproductor cuando el reproductor esté en el estado PREPARADO.

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
   >En un flujo de trabajo VPAID 2.0, para las vistas de anuncios personalizadas es muy importante mantener su `CustomAdView` instancia entre `AdBreak` comienza (evento) `AD_BREAK_START`) y `AdBreak` completa (evento) `AD_BREAK_COMPLETE`), desde el momento en que crea la vista de publicidad personalizada hasta el momento en que la elimina. Es decir, no cree una vista de anuncio personalizada en cada inicio de pausa publicitaria y deséchela en cada finalización.
   >
   >
   >Además, solo debe crear la vista de anuncio personalizada cuando el reproductor esté en estado PREPARADO,
   >
   >
   >Deseche únicamente la vista de anuncio personalizada cuando se invoque el restablecimiento. Por ejemplo:
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
   >Por último, antes de eliminar la vista de anuncios personalizada, debe eliminarla de `FrameLayout`. Por ejemplo:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
