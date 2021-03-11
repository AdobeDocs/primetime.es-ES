---
title: Actualización de directivas DRM
description: Actualización de directivas DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Actualización de directivas de DRM {#updating-drm-policies}

Si las directivas de DRM se actualizan después de empaquetar el contenido, proporcione las directivas de DRM actualizadas al servidor de licencias para que se pueda utilizar la versión actualizada al emitir una licencia. Si un servidor de licencias tiene acceso a una base de datos para almacenar directivas DRM, puede recuperar la directiva DRM actualizada de la base de datos y llamar a `LicenseRequestMessage.setSelectedPolicy()` para proporcionar la nueva versión de la directiva DRM.

Para los servidores de licencias que no dependen de una base de datos central, el SDK proporciona compatibilidad con las listas de actualización de directivas de DRM. Una lista de actualización de directivas DRM es un archivo que incluye una lista de directivas DRM actualizadas o revocadas. Cuando se actualiza una directiva de DRM, genere una nueva lista de actualización de directivas de DRM y coloque periódicamente la lista en todos los servidores de licencias. Pase la lista al SDK estableciendo `HandlerConfiguration.setPolicyUpdateList()`. Si se proporciona una lista de actualización, el SDK consulta esta lista cuando analiza los metadatos de contenido. `ContentInfo.getUpdatedPolicies()` incluye las versiones actualizadas de las políticas de DRM especificadas en los metadatos.

Consulte [Trabajo con directivas DRM](../../../protecting-content/working-policies-overview/working-with-policies.md) y [listas de actualización de directivas DRM](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)