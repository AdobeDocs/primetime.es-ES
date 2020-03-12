---
seo-title: Flujo de trabajo de CEK externo de AAXS DRM
title: Flujo de trabajo de CEK externo de AAXS DRM
description: Este flujo de trabajo se aparta de la mayoría de los sistemas DRM existentes, ya que no requiere el uso de ningún repositorio central ni de un sistema de administración de claves de contenido (CKMS)
seo-description: Este flujo de trabajo se aparta de la mayoría de los sistemas DRM existentes, ya que no requiere el uso de ningún repositorio central ni de un sistema de administración de claves de contenido (CKMS)
uuid: b313594b-0feb-4f27-bf02-f04b955e2140
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc

---


# Flujo de trabajo de CEK externo de AAXS DRM{#aaxs-drm-external-cek-workflow}

Este flujo de trabajo se aparta de la mayoría de los sistemas DRM existentes, ya que no requiere el uso de ningún repositorio central ni de un sistema de administración de claves de contenido (CKMS). Sin embargo, para los clientes que desean que AAXS funcione con su CKMS existente, AAXS proporciona una función llamada &quot;CEK externo&quot;, en la que el CEK se suministra externamente en el momento de la emisión de paquetes y licencias.

![](assets/ECEK_Workflow.PNG)

1. (Paquete) El SDK de Java AAXS se proporciona con un CEK y un ID de CEK.
1. (Paquete) El CEK se utiliza para cifrar contenido.
1. (Paquete) El ID CEK se inserta en los metadatos DRM del contenido.
1. El dispositivo intenta reproducir contenido solicitando una licencia del servidor AAXS.
1. (Licencias) El servidor AAXS extrae el ID de CEK de los metadatos de contenido.
1. El servidor AAXS recupera el CEK del CKMS.
1. (Licencias) El servidor AAXS emite al dispositivo una licencia que contiene el CEK.
