---
title: Previsualización de licencia
description: Previsualización de licencia
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Previsualización de licencia {#license-preview}

Si hay alguna duda sobre si un dispositivo puede consumir y aplicar completamente una licencia DRM de Primetime, puede utilizar la función de previsualización de licencia. Una licencia de previsualización coincide completamente con todas las restricciones y restricciones definidas en la licencia final, pero no contiene la clave de cifrado de contenido (CEK) necesaria para descifrar el contenido protegido. Esta capacidad es útil para determinar si el cliente puede realmente consumir la licencia antes de que el distribuidor de contenido tome la decisión de proporcionar una licencia determinada al cliente. Por ejemplo: un cliente desea ver contenido en HD, pero el distribuidor de contenido quiere asegurarse de que el dispositivo pueda detectar y captar HDCP por completo. En esta situación, el cliente puede llamar a `DRMManager.loadPreviewVoucher()`. Si un `DRMStatusEvent` se recibe, en lugar de `DRMErrorEvent`, entonces se confirma que el cliente puede aplicar completamente las restricciones de Output Protection en la licencia, y el Distribuidor de contenido puede proporcionar libremente este tipo de licencia al cliente.

[iOS acquisitionPreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquisitionPreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
