---
title: DRM de Primetime en el cliente
description: DRM de Primetime en el cliente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# DRM de Primetime en el cliente{#primetime-drm-on-the-client}

Una aplicación de TVSDK de Primetime que reproduzca contenido protegido debe llamar primero a las API de DRM de Primetime para iniciar el flujo de trabajo para el consumo de licencias y la reproducción de contenido protegido. En este flujo de trabajo, Primetime DRM en el cliente construye una solicitud de licencia a partir de los metadatos del contenido protegido y, a continuación, la envía al servidor de licencias DRM de Primetime.

Antes de emitir la solicitud de licencia, el cliente puede opcionalmente realizar la autenticación/autorización necesaria (dependiendo de sus reglas comerciales).
