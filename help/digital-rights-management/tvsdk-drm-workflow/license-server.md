---
title: Servidor de licencias DRM de Primetime
description: Servidor de licencias DRM de Primetime
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Servidor de licencias DRM de Primetime {#primetime-drm-license-server}

El servidor de licencias DRM de Primetime se crea a partir del SDK de Java DRM de Primetime. Este servidor consume solicitudes de licencia de clientes que solicitan acceso a contenido protegido. El servidor tiene la capacidad de analizar y manipular la directiva DRM desde la solicitud de licencia, con el fin de modificar o anular la directiva antes de utilizarla para generar una licencia para el cliente solicitante.

Para poder implementar un servidor de licencias DRM de Primetime, primero debe cumplir con **Reglas de cumplimiento y solidez de Adobe** para DRM de Primetime. Adobe también ofrece un servicio de licencias DRM de Primetime alojado llamado [DRM de Primetime Cloud](../cloud-quick-start/whats-included.md), que puede utilizar como alternativa al alojamiento de su propio servidor de licencias.
