---
title: Vista previa de licencia
description: Vista previa de licencia
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Vista previa de licencia {#license-preview}

Si hay alguna pregunta sobre si un dispositivo puede consumir o no y aplicar completamente una licencia de DRM de Primetime, puede utilizar la función Vista previa de licencia. Una licencia de Vista previa coincide completamente con todas las restricciones y restricciones definidas en la licencia final, pero no contiene la clave de codificación de contenido (CEK) necesaria para descifrar el contenido protegido. Esta capacidad es útil para determinar si el cliente puede consumir la licencia antes de que el Distribuidor de Contenido tome la decisión de proporcionar una licencia particular al cliente. Por ejemplo: un cliente desea ver contenido HD, pero el Distribuidor de contenido desea asegurarse de que el dispositivo pueda detectar y captar el HDCP por completo. En este caso, el cliente puede llamar a `DRMManager.loadPreviewVoucher()`. Si se recibe un `DRMStatusEvent`, en lugar de un `DRMErrorEvent`, se confirma que el cliente puede aplicar completamente las restricciones de Output Protection en la licencia y que el Distribuidor de Contenido puede proporcionar libremente este tipo de licencia al cliente.

[iOS acquisitionPreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquisitionPreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
