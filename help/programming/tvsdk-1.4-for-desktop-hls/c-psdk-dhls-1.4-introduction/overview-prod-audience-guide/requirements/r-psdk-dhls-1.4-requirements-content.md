---
description: Compruebe las restricciones y los requisitos de los flujos y listas de reproducción (manifiestos), incluidas las claves de cifrado DRM.
seo-description: Compruebe las restricciones y los requisitos de los flujos y listas de reproducción (manifiestos), incluidas las claves de cifrado DRM.
seo-title: Requisitos de contenido y manifiesto
title: Requisitos de contenido y manifiesto
uuid: 53cc570a-be33-4488-95e8-43f91b559b13
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Requisitos de contenido y manifiesto {#content-and-manifest-requirements}

Compruebe las restricciones y los requisitos de los flujos y listas de reproducción (manifiestos), incluidas las claves de cifrado DRM.

| Incluya y defina la propiedad para cada flujo ABR en el archivo de manifiesto. `RESOLUTION` Debe utilizar Flash Player 14 o posterior. |
|---|
| Si el flujo protegido por DRM tiene una velocidad de bits múltiple (MBR), la clave de cifrado DRM utilizada para el MBR debe ser la misma que la clave utilizada en todos los flujos de velocidad de bits. |
| Debe tener las mismas representaciones de velocidad de bits que las representaciones del contenido principal. |