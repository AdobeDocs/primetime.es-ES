---
description: Compruebe las restricciones y los requisitos para las transmisiones y listas de reproducción (manifiestos), incluidas las claves de cifrado DRM.
title: Requisitos de contenido y manifiesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# Requisitos de contenido y manifiesto {#content-and-manifest-requirements}

Compruebe las restricciones y los requisitos para las transmisiones y listas de reproducción (manifiestos), incluidas las claves de cifrado DRM.

| Incluya y establezca la propiedad `RESOLUTION` para cada flujo ABR en el archivo de manifiesto. Debe usar el Flash Player 14 o posterior. |
|---|
| Si el flujo protegido por DRM es de tasa de bits múltiple (MBR), la clave de cifrado DRM utilizada para el MBR debe ser la misma que la clave utilizada en todos los flujos de velocidad de bits. |
| Debe tener las mismas representaciones de velocidad de bits que las representaciones del contenido principal. |