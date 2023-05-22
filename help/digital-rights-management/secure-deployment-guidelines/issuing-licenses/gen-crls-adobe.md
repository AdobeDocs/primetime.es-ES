---
description: Puede utilizar Adobe Primetime DRM para crear listas CRL que complementen la lista CRL de la máquina publicada por Adobe.
title: Generación de listas CRL para complementar las publicadas por Adobe
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Generación de listas CRL para complementar las publicadas por Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Puede utilizar Adobe Primetime DRM para crear listas CRL que complementen la lista CRL de la máquina publicada por Adobe.

El SDK de DRM de Primetime comprueba y aplica las CRL de Adobe. Sin embargo, puede no permitir equipos cliente adicionales creando una CRL que revoque las credenciales de equipo adicionales pasando la CRL al SDK de DRM de Primetime. Al emitir una licencia, el SDK comprueba la CRL de Adobe y su CRL.

Para generar CRL, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
