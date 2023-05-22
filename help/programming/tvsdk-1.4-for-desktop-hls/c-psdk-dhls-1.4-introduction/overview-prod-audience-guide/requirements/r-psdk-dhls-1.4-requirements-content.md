---
description: Compruebe las restricciones y requisitos para emisiones y listas de reproducción (manifiestos), incluidas las claves de cifrado DRM.
title: Requisitos de contenido y manifiesto
exl-id: 96b2b245-558b-4606-87c0-22140430c326
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Requisitos de contenido y manifiesto {#content-and-manifest-requirements}

Compruebe las restricciones y requisitos para emisiones y listas de reproducción (manifiestos), incluidas las claves de cifrado DRM.

| Incluya y configure el `RESOLUTION` para cada secuencia ABR del archivo de manifiesto. Debe utilizar el Flash Player 14 o posterior. |
|---|
| Si el flujo protegido por DRM tiene una velocidad de bits múltiple (MBR), la clave de cifrado DRM utilizada para el MBR debe ser la misma que la utilizada en todos los flujos de velocidad de bits. |
| Debe tener las mismas representaciones de velocidad de bits que las del contenido principal. |
