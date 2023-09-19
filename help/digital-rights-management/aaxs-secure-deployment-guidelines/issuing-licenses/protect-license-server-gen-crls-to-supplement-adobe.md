---
title: Generar CRL para complementar las publicadas por Adobe
description: Generar CRL para complementar las publicadas por Adobe
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Generar CRL para complementar las publicadas por Adobe{#generate-crls-to-supplement-those-published-by-adobe}

Adobe El acceso permite crear listas CRL para complementar la lista CRL de la máquina publicada por Adobe. El SDK de acceso a Adobe comprueba y aplica las CRL de Adobe; sin embargo, puede no permitir equipos cliente adicionales creando una CRL que revoque las credenciales de equipo adicionales. Para ello, debe pasar la CRL al SDK de acceso a Adobe y, a continuación, al emitir una licencia, el SDK comprueba tanto la CRL de Adobe como su propia CRL.

Para obtener más información sobre la generación de CRL, consulte `RevocationListFactory` in *Referencia de API de acceso de Adobe*.
