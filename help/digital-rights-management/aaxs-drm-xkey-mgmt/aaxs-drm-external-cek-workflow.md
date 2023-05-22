---
title: Flujo de trabajo de CEK externo de AXS DRM
description: Este flujo de trabajo se aleja de la mayoría de los sistemas DRM existentes, ya que no requiere el uso de ningún repositorio central ni de un sistema de administración de claves de contenido (CKMS)
exl-id: f084aa57-8bef-40a0-b52d-4d23dfdf36c4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Flujo de trabajo de CEK externo de AXS DRM{#aaxs-drm-external-cek-workflow}

Este flujo de trabajo se aleja de la mayoría de los sistemas DRM existentes, ya que no requiere el uso de ningún repositorio central ni de un sistema de administración de claves de contenido (CKMS). Sin embargo, para los clientes que desean que AAXS funcione con sus CKMS existentes, AAXS proporciona una función llamada &quot;CEK externo&quot;, en la que el CEK se suministra externamente en el momento del empaquetado y la emisión de la licencia.

![](assets/ECEK_Workflow.PNG)

1. (Paquete) El SDK de Java de AXS incluye un CEK y un ID de CEK.
1. (Paquete) El CEK se utiliza para cifrar contenido.
1. (Paquete) El ID de CEK se inserta en los metadatos DRM del contenido.
1. El dispositivo intenta reproducir contenido solicitando una licencia al servidor AXS.
1. (Licencias) El servidor AXS extrae el ID de CEK de los metadatos de contenido.
1. El servidor AXS recupera el CEK del CKMS.
1. (Licencias) El servidor AXS emite al dispositivo una licencia que contiene el CEK.
