---
description: Para añadir compatibilidad con VPAID 2.0, agregue una vista de anuncio personalizada y los oyentes adecuados.
title: Implementación de la integración con VPAID 2.0
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# Implementación de la integración con VPAID 2.0{#implement-vpaid-integration}

Para añadir compatibilidad con VPAID 2.0, agregue una vista de anuncio personalizada y los oyentes adecuados.

Para agregar compatibilidad con VPAID 2.0:

1. Añada la vista de anuncio personalizada a la interfaz del reproductor.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Agregue un oyente para los eventos de publicidad personalizados.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

