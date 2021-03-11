---
title: Generar listas CRL para complementar las publicadas por Adobe
description: Generar listas CRL para complementar las publicadas por Adobe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Generar listas CRL para complementar las publicadas por Adobe{#generate-crls-to-supplement-those-published-by-adobe}

Adobe Access permite crear listas CRL para complementar la CRL de máquinas publicada por Adobe. El SDK de acceso a Adobe comprueba y aplica las listas CRL de Adobe; sin embargo, puede no permitir equipos cliente adicionales creando una CRL que revoque credenciales de equipo adicionales. Para ello, debe pasar la CRL al SDK de acceso a Adobe y, a continuación, al emitir una licencia, el SDK comprueba la CRL de Adobe y su propia CRL.

Para obtener más información sobre la generación de CRL, consulte `RevocationListFactory` en *Referencia de API de acceso a Adobe*.
