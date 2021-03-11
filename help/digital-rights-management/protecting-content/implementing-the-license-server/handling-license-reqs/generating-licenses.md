---
title: Generación de licencias
description: Generación de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Generación de licencias{#generating-licenses}

Si desea emitir una licencia de hoja a un usuario, el SDK debe descifrar el CEK contenido en los metadatos de contenido y volver a cifrarlo para el equipo que solicita una licencia. Para descifrar el CEK, el servidor debe proporcionar la información necesaria para descifrar la clave. Llame a `ContentInfo.setKeyRetrievalInfo()` y proporcione un objeto `AsymmetricKeyRetrieval`. Si los metadatos incluyen varias directivas, el servidor debe determinar qué directiva utilizar e invocar a `LicenseRequestMessage.setSelectedPolicy()`. A continuación, llame a `LicenseRequestMessage.generateLicense()` para generar la licencia. Con el objeto `License` que se devuelve, puede modificar la caducidad o los derechos de la licencia.

Si se especifica un objeto `ExternalKeyRetrieval` en el objeto `ContentInfo`, se espera que el servidor de licencias utilice el ID de CEK asociado para recuperar el CEK adecuado que se inserta en la licencia.

Consulte [Descripción general del CEK externo de Adobe Primetime DRM](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) para obtener más información sobre cómo utilizar el flujo de trabajo de CEK externo.
