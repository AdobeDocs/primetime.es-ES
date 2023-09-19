---
title: Consumir CRL generadas localmente
description: Consumir CRL generadas localmente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Consumir CRL generadas localmente{#consume-locally-generated-crls}

Para consumir listas de revocación de certificados (CRL) generadas localmente y listas de actualización de directivas, utilice las API de acceso a Adobe para comprobar la firma. Las API comprueban que las listas no se han manipulado y que el servidor de licencias correcto las ha firmado.

* Llamada `RevocationList.verifySignature` para comprobar la firma antes de proporcionar RevocationList a cualquier API.

  Para obtener más información, consulte `RevocationListFactory` en el *Referencia de API de acceso de Adobe*.

* Llamada `PolicyUpdateList.verifySignature`para comprobar la firma antes de proporcionar el `PolicyUpdateList` a cualquier API.

  Para obtener más información, consulte `PolicyUpdateList` en el *Referencia de API de acceso de Adobe*.
