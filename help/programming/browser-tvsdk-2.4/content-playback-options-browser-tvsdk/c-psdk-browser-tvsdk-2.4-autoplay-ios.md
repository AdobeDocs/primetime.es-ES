---
title: Reproducción automática en iOS
description: Reproducción automática en iOS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---


# Reproducción automática en iOS{#autoplay-on-ios}

La implementación de la API de volumen de AdobePSDK.MediaPlayer permite la reproducción automática de contenido en dispositivos que ejecutan iOS versión 10 o superior. iOS permite la reproducción automática solo cuando el volumen se silencia. Cuando el volumen se establece en cero, la API establece la propiedad `muted` de la etiqueta de vídeo en `true`; de lo contrario, la propiedad `muted` se establece en `false`. La API `play` inicia la reproducción sin ninguna interacción del usuario ni ningún gesto del usuario.

Para la reproducción automática en iPhone, también debe establecerse la propiedad `playsInline` de la etiqueta `video` en `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>El uso de la propiedad `playsInline` inicia la reproducción sin el modo de pantalla completa.

