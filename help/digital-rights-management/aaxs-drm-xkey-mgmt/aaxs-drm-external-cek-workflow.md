---
title: Flujo de trabajo CEK externo de AAXS DRM
description: Este flujo de trabajo se aleja de la mayoría de los sistemas DRM existentes, ya que no requiere el uso de ningún repositorio central o sistema de administración de claves de contenido (CKMS)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Flujo de trabajo de CEK externo AAXS DRM{#aaxs-drm-external-cek-workflow}

Este flujo de trabajo se aparta de la mayoría de los sistemas DRM existentes, ya que no requiere el uso de ningún repositorio central o sistema de administración de claves de contenido (CKMS). Sin embargo, para los clientes que desean que AAXS trabaje con su CKMS existente, AAXS proporciona una función llamada &quot;CEK externo&quot;, en la que el CEK se suministra externamente en el momento del empaquetado y la expedición de licencias.

![](assets/ECEK_Workflow.PNG)

1. (Paquete) El SDK de Java AAXS se proporciona con un CEK y un ID de CEK.
1. (Paquete) El CEK se utiliza para cifrar contenido.
1. (Paquete) El ID de CEK se inserta en los metadatos DRM del contenido.
1. El dispositivo intenta reproducir contenido solicitando una licencia del servidor AAXS.
1. (Licencias) El servidor AAXS extrae el ID de CEK de los metadatos de contenido.
1. El servidor AAXS recupera el CEK del CKMS.
1. (Licencias) El servidor AAXS emite al dispositivo una licencia que contiene el CEK.
