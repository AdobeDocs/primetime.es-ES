---
seo-title: Generar listas CRL para complementar las publicadas por Adobe
title: Generar listas CRL para complementar las publicadas por Adobe
uuid: 4e93f6d3-5a04-44e9-9e6b-e878798b68f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Generar listas CRL para complementar las publicadas por Adobe{#generate-crls-to-supplement-those-published-by-adobe}

Adobe Access permite crear listas CRL para complementar la lista CRL de equipos publicada por Adobe. El SDK de Adobe Access comprueba y aplica las CRL de Adobe, pero puede no permitir equipos cliente adicionales creando una CRL que revoque las credenciales de equipo adicionales. Para ello, debe pasar la CRL al SDK de Adobe Access y, a continuación, al emitir una licencia, el SDK comprueba tanto la CRL de Adobe como su propia CRL.

Para obtener más información sobre la generación de CRL, consulte `RevocationListFactory` en *Referencia de API de acceso a Adobe*.
