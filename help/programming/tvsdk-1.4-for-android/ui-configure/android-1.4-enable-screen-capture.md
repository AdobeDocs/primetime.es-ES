---
description: 'null'
keywords: setSecure;VideoEngineView
seo-description: 'null'
seo-title: Activar captura de pantalla
title: Activar captura de pantalla
uuid: f3d18729-e13e-47f9-b4b8-f93a2874ef16
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# Habilitar captura de pantalla{#enable-screen-capture}

TVSDK no permite la captura de pantalla de forma predeterminada. El reproductor llama a `setSecure(true)` en el objeto `com.adobe.ave.VideoEngineView` en tiempo de construcción. Tiene acceso a este objeto, ya que tiene que construir un objeto `VideoEngineView` y suministrarlo al objeto `VideoEngine`.

Para activar la captura de pantalla en la aplicación:

1. Construya el objeto `com.adobe.ave.VideoEngineView`.
1. Llame a `setSecure(false)` en el objeto `VideoEngineView`.
