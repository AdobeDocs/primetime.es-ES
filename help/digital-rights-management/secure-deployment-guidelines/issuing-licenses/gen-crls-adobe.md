---
description: Puede utilizar DRM de Adobe Primetime para crear CRL que complementen la CRL de equipos publicada por Adobe.
seo-description: Puede utilizar DRM de Adobe Primetime para crear CRL que complementen la CRL de equipos publicada por Adobe.
seo-title: Generación de CRL para complementar las publicadas por Adobe
title: Generación de CRL para complementar las publicadas por Adobe
uuid: 0cc4254d-20a0-4e05-9c5b-0b84a5c833cb
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---


# Generación de CRL para complementar las publicadas por Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Puede utilizar DRM de Adobe Primetime para crear CRL que complementen la CRL de equipos publicada por Adobe.

El SDK de DRM de Primetime comprueba y aplica las CRL de Adobe. Sin embargo, puede no permitir equipos cliente adicionales creando una CRL que revoque las credenciales de equipo adicionales pasando la CRL al SDK de DRM de Primetime. Cuando se emite una licencia, el SDK comprueba la CRL de Adobe y la CRL.

Para generar CRL, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
