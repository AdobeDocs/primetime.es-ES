---
title: DRM de Primetime en el cliente
description: DRM de Primetime en el cliente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# DRM de Primetime en el cliente{#primetime-drm-on-the-client}

Una aplicación de TVSDK de Primetime que reproduce contenido protegido debe llamar primero a las API de DRM de Primetime para iniciar el flujo de trabajo de consumo de licencias y reproducción de contenido protegido. En este flujo de trabajo, Primetime DRM del cliente crea una solicitud de licencia a partir de los metadatos del contenido protegido y, a continuación, la envía al servidor de licencias DRM de Primetime.

Antes de emitir la solicitud de licencia, el cliente puede realizar opcionalmente la autenticación/autorización necesaria (según sus reglas comerciales).
