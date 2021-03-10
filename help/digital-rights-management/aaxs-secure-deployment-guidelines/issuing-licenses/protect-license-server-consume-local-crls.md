---
title: Consumir listas CRL generadas localmente
description: Consumir listas CRL generadas localmente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Utilice listas CRL generadas localmente{#consume-locally-generated-crls}

Para consumir listas de revocación de certificados (CRL) generadas localmente y listas de actualización de directivas, utilice las API de acceso a Adobe para comprobar la firma. Las API verifican que las listas no se hayan manipulado y que hayan sido firmadas por el servidor de licencias correcto.

* Llame a `RevocationList.verifySignature` para comprobar la firma antes de proporcionar RevocationList a cualquier API.

   Para obtener más información, consulte `RevocationListFactory` en la *Referencia de API de acceso al Adobe*.

* Llame a `PolicyUpdateList.verifySignature`para comprobar la firma antes de proporcionar el `PolicyUpdateList` a cualquier API.

   Para obtener más información, consulte `PolicyUpdateList` en la *Referencia de API de acceso al Adobe*.

