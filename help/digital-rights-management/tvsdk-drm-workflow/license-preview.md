---
seo-title: Vista previa de licencia
title: Vista previa de licencia
uuid: 61ff171f-b977-40ef-8e8d-2900316fa89a
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Vista previa de licencia {#license-preview}

Si hay alguna pregunta sobre si un dispositivo puede consumir o no una licencia de DRM Primetime y aplicarla por completo, puede utilizar la función Vista previa de licencia. Una licencia de vista previa coincide completamente con todas las restricciones y restricciones definidas en la licencia final, pero no contiene la clave de codificación de contenido (CEK) necesaria para descifrar el contenido protegido. Esta capacidad es útil para determinar si el cliente puede realmente consumir la licencia antes de que el distribuidor de contenido tome la decisión de proporcionar una licencia específica al cliente. Por ejemplo: un cliente desea ver el contenido HD, pero el distribuidor de contenido desea asegurarse de que el dispositivo pueda detectar y captar el HDCP por completo. En este caso, el cliente puede llamar `DRMManager.loadPreviewVoucher()`. Si `DRMStatusEvent` se recibe una licencia, en lugar de una `DRMErrorEvent`, se confirma que el cliente puede aplicar completamente las restricciones de Output Protection en la licencia y que el distribuidor de contenido puede proporcionar libremente este tipo de licencia al cliente.

[iOS acquisitionPreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquisitionPreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
