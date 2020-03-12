---
description: Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.
seo-description: Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.
seo-title: Implementación de la integración con VPAID 2.0
title: Implementación de la integración con VPAID 2.0
uuid: 7d11ffd8-240c-4a95-94e6-ff4417c8942e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implementación de la integración con VPAID 2.0{#implement-vpaid-integration}

Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.

Para agregar compatibilidad con VPAID 2.0:

1. Agregue la vista de publicidad personalizada a la interfaz del reproductor.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Agregue un detector para eventos de publicidad personalizados.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

