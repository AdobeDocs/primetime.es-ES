---
seo-title: Generación de licencias
title: Generación de licencias
uuid: f91b0cc8-e0ed-4722-947b-22eb2bfba916
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Generación de licencias{#generating-licenses}

Si desea emitir una licencia de hoja a un usuario, el SDK debe descifrar el CEK contenido en los metadatos de contenido y volver a cifrarlo para el equipo que solicita una licencia. Para descifrar el CEK, el servidor debe proporcionar la información necesaria para descifrar la clave. Llama `ContentInfo.setKeyRetrievalInfo()` y proporciona un `AsymmetricKeyRetrieval` objeto. Si los metadatos incluyen varias directivas, el servidor debe determinar qué directiva utilizar y llamar `LicenseRequestMessage.setSelectedPolicy()`. Luego llame `LicenseRequestMessage.generateLicense()` para generar la licencia. Con el `License` objeto que se devuelve, puede modificar la caducidad o los derechos de la licencia.

Si se especifica un `ExternalKeyRetrieval` objeto en el `ContentInfo` objeto, se espera que el servidor de licencias utilice el ID de CEK asociado para recuperar el CEK adecuado que se inserta en la licencia.

Consulte [Adobe Primetime DRM External CEK Overview](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) para obtener más información sobre cómo utilizar el flujo de trabajo de CEK externo.
