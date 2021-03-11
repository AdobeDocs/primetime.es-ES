---
title: Servidor de licencias DRM de Primetime
description: Servidor de licencias DRM de Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Servidor de licencias DRM de Primetime {#primetime-drm-license-server}

El servidor de licencias DRM de Primetime se crea desde el SDK Java de DRM de Primetime. Este servidor consume solicitudes de licencia de clientes que solicitan acceso a contenido protegido. El servidor tiene la capacidad de analizar y manipular la directiva DRM desde la solicitud de licencia, para modificar o anular la directiva antes de utilizar la directiva para generar una licencia para el cliente solicitante.

Para implementar un servidor de licencias de DRM de Primetime, primero debe cumplir las **reglas de cumplimiento y solidez del Adobe** para DRM de Primetime. Adobe también ofrece un servicio de licencia DRM de Primetime alojado llamado [Primetime Cloud DRM](../cloud-quick-start/whats-included.md), que puede utilizar como alternativa al alojamiento de su propio servidor de licencias.
