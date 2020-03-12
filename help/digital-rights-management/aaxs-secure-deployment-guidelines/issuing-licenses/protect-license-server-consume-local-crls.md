---
seo-title: Consumir CRL generadas localmente
title: Consumir CRL generadas localmente
uuid: 5a4519b8-6dbd-4921-9048-6c9f67aae18d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Consumir CRL generadas localmente{#consume-locally-generated-crls}

Para consumir listas de revocación de certificados (CRL) generadas localmente y listas de actualización de políticas, utilice las API de Adobe Access para verificar la firma. Las API comprueban que las listas no se han manipulado y que están firmadas por el servidor de licencias correcto.

* Llame `RevocationList.verifySignature` para comprobar la firma antes de proporcionar RevocationList a cualquier API.

   Para obtener más información, consulte `RevocationListFactory` la Referencia *de la API de* Adobe Access.

* Llame `PolicyUpdateList.verifySignature`para comprobar la firma antes de proporcionar el `PolicyUpdateList` a cualquier API.

   Para obtener más información, consulte `PolicyUpdateList` la Referencia *de la API de* Adobe Access.

