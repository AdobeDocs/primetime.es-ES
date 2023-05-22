---
keywords: setSecure;VideoEngineView
title: Habilitar captura de pantalla
description: Habilitar captura de pantalla
copied-description: true
exl-id: 5dd1bf4e-ab50-4b57-89e4-eacc291a9fe3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Habilitar captura de pantalla{#enable-screen-capture}

TVSDK deshabilita la captura de pantalla de forma predeterminada. El reproductor llama a `setSecure(true)` en el `com.adobe.ave.VideoEngineView` objeto en tiempo de construcción. Tiene acceso a este objeto, ya que tiene que construir un `VideoEngineView` objeto y suministrarlo al `VideoEngine` objeto.

Para habilitar la captura de pantalla en la aplicación:

1. Construya el `com.adobe.ave.VideoEngineView` objeto.
1. Llamada `setSecure(false)` en su `VideoEngineView` objeto.
