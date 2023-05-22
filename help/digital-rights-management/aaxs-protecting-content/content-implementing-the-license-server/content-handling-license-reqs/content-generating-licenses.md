---
title: Generación de licencias
description: Generación de licencias
copied-description: true
exl-id: 65c5677d-5a69-46f8-bc14-7af6d14d4dff
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Generación de licencias {#generating-licenses}

Para emitir una licencia hoja para el usuario, el SDK debe descifrar la CEK contenida en los metadatos de contenido y volver a cifrarla para el equipo que solicita una licencia. Para descifrar el CEK, el servidor debe proporcionar la información necesaria para descifrar la clave. Llamada `ContentInfo.setKeyRetrievalInfo()` y proporcionar un `AsymmetricKeyRetrieval` objeto. Si los metadatos contienen varias directivas, el servidor debe determinar a qué directiva utilizar y llamar `LicenseRequestMessage.setSelectedPolicy()`. Entonces llama a `LicenseRequestMessage.generateLicense()` para generar la licencia. Uso del `License` objeto que se devuelve, puede modificar la caducidad o los derechos de la licencia.

Si se especifica un objeto ExternalKeyRetrieval en la variable `ContentInfo` , se espera que el servidor de licencias use el ID de CEK asociado para recuperar el CEK apropiado que se insertará en la licencia. Para obtener más información sobre cómo utilizar el flujo de trabajo de CEK externo, consulte [Descripción general de CEK externo de DRM de acceso a Adobe](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
