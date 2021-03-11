---
keywords: setSecure;VideoEngineView
title: Habilitar captura de pantalla
description: Habilitar captura de pantalla
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# Habilitar captura de pantalla{#enable-screen-capture}

TVSDK deshabilita la captura de pantalla de forma predeterminada. El reproductor llama a `setSecure(true)` en el objeto `com.adobe.ave.VideoEngineView` en el momento de la construcción. Tiene acceso a este objeto, ya que debe construir un objeto `VideoEngineView` y suministrarlo al objeto `VideoEngine`.

Para habilitar la captura de pantalla en la aplicación:

1. Construya el objeto `com.adobe.ave.VideoEngineView`.
1. Llame a `setSecure(false)` en el objeto `VideoEngineView`.
