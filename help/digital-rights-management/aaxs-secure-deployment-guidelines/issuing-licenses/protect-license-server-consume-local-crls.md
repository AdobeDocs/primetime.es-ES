---
title: Consumir CRL generadas localmente
description: Consumir CRL generadas localmente
copied-description: true
exl-id: d96418d0-8fd3-4f6d-8480-191fe540080a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
