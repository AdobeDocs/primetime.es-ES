---
seo-title: Generación de licencias
title: Generación de licencias
uuid: 242d5567-f609-4781-a8a6-2f3d78471344
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Generación de licencias {#generating-licenses}

Para emitir una licencia de hoja al usuario, el SDK debe descifrar el CEK contenido en los metadatos de contenido y volver a cifrarlo para el equipo que solicita una licencia. Para descifrar el CEK, el servidor debe proporcionar la información necesaria para descifrar la clave. Llama `ContentInfo.setKeyRetrievalInfo()` y proporciona un `AsymmetricKeyRetrieval` objeto. Si los metadatos contienen varias directivas, el servidor debe determinar qué directiva utilizar y llamar `LicenseRequestMessage.setSelectedPolicy()`. Luego llame `LicenseRequestMessage.generateLicense()` para generar la licencia. Con el `License` objeto que se devuelve, puede modificar la caducidad o los derechos de la licencia.

Si se especifica un objeto ExternalKeyRetrieval en el `ContentInfo` objeto, se espera que el servidor de licencias utilice el ID de CEK asociado para recuperar el CEK adecuado que se insertará en la licencia. Para obtener más información sobre cómo utilizar el flujo de trabajo de CEK externo, consulte Visión general de CEK externo de DRM de [Adobe Access](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
