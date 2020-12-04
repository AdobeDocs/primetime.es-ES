---
description: Para consumir listas de revocación de certificados (CRL) generadas localmente y listas de actualización de políticas, utilice las API de Adobe Primetime DRM para comprobar la firma.
seo-description: Para consumir listas de revocación de certificados (CRL) generadas localmente y listas de actualización de políticas, utilice las API de Adobe Primetime DRM para comprobar la firma.
seo-title: Consumo de CRL generadas localmente
title: Consumo de CRL generadas localmente
uuid: 2e20b8ca-8606-4c27-b585-2f020b93be32
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Consumo de CRL generadas localmente {#consuming-locally-generated-crls}

Para consumir listas de revocación de certificados (CRL) generadas localmente y listas de actualización de políticas, utilice las API de Adobe Primetime DRM para comprobar la firma.

Las siguientes API comprueban que las listas no se han manipulado y que el servidor de licencias correcto ha firmado las listas:

* Llame a [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) para comprobar la firma antes de proporcionar el [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a cualquier API.

   Para obtener más información, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Llame a [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) para comprobar la firma antes de proporcionar el `PolicyUpdateList` a cualquier API.

   Para obtener más información, consulte [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

