---
title: Actualización de directivas DRM
description: Actualización de directivas DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Actualización de directivas DRM {#updating-drm-policies}

Si las políticas de DRM se actualizan después de empaquetar el contenido, proporcione las políticas de DRM actualizadas al servidor de licencias para que la versión actualizada se pueda utilizar al emitir una licencia. Si un servidor de licencias tiene acceso a una base de datos para almacenar directivas DRM, puede recuperar la directiva DRM actualizada de la base de datos e invocar `LicenseRequestMessage.setSelectedPolicy()` para proporcionar la nueva versión de la directiva DRM.

Para los servidores de licencias que no dependen de una base de datos central, el SDK admite Listas de actualización de directivas DRM. Una lista de actualización de directivas DRM es un fichero que incluye una lista de directivas DRM actualizadas o revocadas. Cuando se actualice una directiva DRM, genere una nueva lista de actualización de directivas DRM y, periódicamente, inserte la lista en todos los servidores de licencias. Pasar la lista al SDK mediante la configuración `HandlerConfiguration.setPolicyUpdateList()`. Si se proporciona una lista de actualización, el SDK consulta esta lista cuando analiza los metadatos de contenido. `ContentInfo.getUpdatedPolicies()` incluye las versiones actualizadas de las políticas de DRM especificadas en los metadatos.

Consulte [Uso de directivas de DRM](../../../protecting-content/working-policies-overview/working-with-policies.md) y [Listas de actualización de directivas DRM](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
