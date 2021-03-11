---
description: Puede utilizar Adobe Primetime DRM para crear listas CRL que complementen la CRL del equipo que publica el Adobe.
title: Generación de listas CRL para complementar las publicadas por Adobe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Generación de listas CRL para complementar las publicadas por Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Puede utilizar Adobe Primetime DRM para crear listas CRL que complementen la CRL del equipo que publica el Adobe.

El SDK de DRM de Primetime comprueba y aplica las CRL de Adobe. Sin embargo, puede no permitir equipos cliente adicionales creando una CRL que revoque credenciales de equipo adicionales pasando la CRL al SDK de DRM de Primetime. Cuando emite una licencia, el SDK comprueba la CRL de Adobe y la CRL.

Para generar listas CRL, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
