---
seo-title: Actualización de directivas DRM
title: Actualización de directivas DRM
uuid: 6f7a1432-88e4-499b-a008-6c8cf0e9c09b
translation-type: tm+mt
source-git-commit: d5986e9bc8689bf37abdf242a41aea5e768df754
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Actualizando directivas de DRM {#updating-drm-policies}

Si las directivas de DRM se actualizan después de empaquetar el contenido, proporcione las directivas de DRM actualizadas al servidor de licencias para que la versión actualizada pueda utilizarse al emitir una licencia. Si un servidor de licencias tiene acceso a una base de datos para almacenar directivas DRM, puede recuperar la directiva DRM actualizada de la base de datos y llamar a `LicenseRequestMessage.setSelectedPolicy()` para proporcionar la nueva versión de la directiva DRM.

Para los servidores de licencias que no dependen de una base de datos central, el SDK proporciona compatibilidad con las Listas de actualización de directivas DRM. Una lista de actualización de directiva DRM es un archivo que incluye una lista de directivas DRM actualizadas o revocadas. Cuando se actualice una directiva DRM, genere una nueva Lista de actualización de directiva DRM y envíe periódicamente la lista a todos los servidores de licencias. Pase la lista al SDK estableciendo `HandlerConfiguration.setPolicyUpdateList()`. Si se proporciona una lista de actualización, el SDK consulta esta lista cuando analiza los metadatos del contenido. `ContentInfo.getUpdatedPolicies()` incluye las versiones actualizadas de las directivas DRM especificadas en los metadatos.

Consulte [Uso de políticas de DRM](../../../protecting-content/working-policies-overview/working-with-policies.md) y [listas de actualización de directivas de DRM](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)