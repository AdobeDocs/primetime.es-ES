---
description: 'null'
keywords: setSecure;VideoEngineView
seo-description: 'null'
seo-title: Activar captura de pantalla
title: Activar captura de pantalla
uuid: f3d18729-e13e-47f9-b4b8-f93a2874ef16
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Activar captura de pantalla{#enable-screen-capture}

TVSDK no permite la captura de pantalla de forma predeterminada. El reproductor llama `setSecure(true)` al `com.adobe.ave.VideoEngineView` objeto en tiempo de construcción. Tiene acceso a este objeto, ya que tiene que construir un `VideoEngineView` objeto y suministrarlo al `VideoEngine` objeto.

Para activar la captura de pantalla en la aplicación:

1. Construya el `com.adobe.ave.VideoEngineView` objeto.
1. Llama `setSecure(false)` al `VideoEngineView` objeto.
