---
title: Actualización de directivas
description: Actualización de directivas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Actualización de directivas {#updating-policies}

Si las directivas se actualizan después de empaquetar el contenido, proporcione las directivas actualizadas al servidor de licencias para que se pueda utilizar la versión actualizada al emitir una licencia. Si el servidor de licencias tiene acceso a una base de datos para almacenar directivas, puede recuperar la directiva actualizada de la base de datos y llamar a `LicenseRequestMessage.setSelectedPolicy()` para proporcionar la nueva versión de la directiva.

Para los servidores de licencias que no dependen de una base de datos central, el SDK proporciona compatibilidad con las listas de actualización de directivas. Una lista de actualización de directivas es un archivo que contiene una lista de directivas actualizadas o revocadas. Cuando se actualiza una directiva, genere una nueva lista de actualización de directivas y extraiga periódicamente la lista a todos los servidores de licencias. Pase la lista al SDK estableciendo `HandlerConfiguration.setPolicyUpdateList()`. Si se proporciona una lista de actualización, el SDK consulta esta lista al analizar los metadatos de contenido. `ContentInfo.getUpdatedPolicies()` contiene las versiones actualizadas de las directivas especificadas en los metadatos.

Consulte [Trabajo con directivas](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) y [Listas de actualización de directivas.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
