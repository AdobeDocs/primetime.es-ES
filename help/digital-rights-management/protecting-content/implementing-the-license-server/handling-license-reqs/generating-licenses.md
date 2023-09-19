---
title: Generación de licencias
description: Generación de licencias
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Generación de licencias{#generating-licenses}

Si desea emitir una licencia hoja para un usuario, el SDK debe descifrar la CEK contenida en los metadatos de contenido y volver a cifrarla para el equipo que solicita una licencia. Para descifrar el CEK, el servidor debe proporcionar la información necesaria para descifrar la clave. Llamada `ContentInfo.setKeyRetrievalInfo()` y proporcionar un `AsymmetricKeyRetrieval` objeto. Si los metadatos incluyen varias directivas, el servidor debe determinar a qué directiva utilizar y llamar `LicenseRequestMessage.setSelectedPolicy()`. Entonces llama a `LicenseRequestMessage.generateLicense()` para generar la licencia. Uso del `License` objeto que se devuelve, puede modificar la caducidad o los derechos de la licencia.

Si un `ExternalKeyRetrieval` se especifica en la variable `ContentInfo` , se espera que el servidor de licencias utilice el ID de CEK asociado para recuperar el CEK apropiado que se ha insertado en la licencia.

Consulte la [Descripción general de CEK externo de Adobe Primetime DRM](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) para obtener más información sobre cómo utilizar el flujo de trabajo de CEK externo.
