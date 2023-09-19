---
description: Compruebe las restricciones y requisitos para emisiones y listas de reproducción (manifiestos), incluidas las claves de cifrado DRM.
title: Requisitos de contenido y manifiesto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
