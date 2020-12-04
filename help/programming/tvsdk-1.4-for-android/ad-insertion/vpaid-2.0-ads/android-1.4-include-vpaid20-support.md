---
description: Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.
seo-description: Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.
seo-title: Implementación de la integración con VPAID 2.0
title: Implementación de la integración con VPAID 2.0
uuid: 7d11ffd8-240c-4a95-94e6-ff4417c8942e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---


# Implementar la integración de VPAID 2.0{#implement-vpaid-integration}

Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.

Para agregar compatibilidad con VPAID 2.0:

1. Añada la vista de publicidad personalizada en la interfaz del reproductor.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Añada un oyente para eventos de publicidad personalizados.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

