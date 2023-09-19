---
keywords: setSecure;VideoEngineView
title: Habilitar captura de pantalla
description: Habilitar captura de pantalla
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Habilitar captura de pantalla{#enable-screen-capture}

TVSDK deshabilita la captura de pantalla de forma predeterminada. El reproductor llama a `setSecure(true)` en el `com.adobe.ave.VideoEngineView` objeto en tiempo de construcción. Tiene acceso a este objeto, ya que tiene que construir un `VideoEngineView` objeto y suministrarlo al `VideoEngine` objeto.

Para habilitar la captura de pantalla en la aplicación:

1. Construya el `com.adobe.ave.VideoEngineView` objeto.
1. Llamada `setSecure(false)` en su `VideoEngineView` objeto.
