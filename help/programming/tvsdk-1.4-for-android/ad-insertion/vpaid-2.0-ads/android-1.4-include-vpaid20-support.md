---
description: Para agregar compatibilidad con VPAID 2.0, agregue una vista de anuncio personalizada y oyentes adecuados.
title: Implementación de la integración con VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# Implementación de la integración de VPAID 2.0{#implement-vpaid-integration}

Para agregar compatibilidad con VPAID 2.0, agregue una vista de anuncio personalizada y oyentes adecuados.

Para añadir compatibilidad con VPAID 2.0:

1. Agregue la vista de anuncio personalizada a la interfaz del reproductor.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Añada un oyente para eventos de publicidad personalizados.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

