---
title: DRM de Primetime en el cliente
description: DRM de Primetime en el cliente
copied-description: true
exl-id: 157d558f-3014-4d05-bba1-e73134cedc23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# DRM de Primetime en el cliente{#primetime-drm-on-the-client}

Una aplicación de TVSDK de Primetime que reproduce contenido protegido debe llamar primero a las API de DRM de Primetime para iniciar el flujo de trabajo de consumo de licencias y reproducción de contenido protegido. En este flujo de trabajo, Primetime DRM del cliente crea una solicitud de licencia a partir de los metadatos del contenido protegido y, a continuación, la envía al servidor de licencias DRM de Primetime.

Antes de emitir la solicitud de licencia, el cliente puede realizar opcionalmente la autenticación/autorización necesaria (según sus reglas comerciales).
