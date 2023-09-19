---
title: Actualización de directivas
description: Actualización de directivas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Actualización de directivas {#updating-policies}

Si las directivas se actualizan después de empaquetar el contenido, proporcione las directivas actualizadas al servidor de licencias para que la versión actualizada se pueda utilizar al emitir una licencia. Si el servidor de licencias tiene acceso a una base de datos para almacenar directivas, puede recuperar la directiva actualizada de la base de datos y llamar a `LicenseRequestMessage.setSelectedPolicy()` para proporcionar la nueva versión de la directiva.

Para los servidores de licencias que no dependen de una base de datos central, el SDK admite Listas de actualización de directivas. Una lista de actualización de directivas es un archivo que contiene una lista de directivas actualizadas o revocadas. Cuando se actualice una directiva, genere una nueva lista de actualización de directivas y, periódicamente, extraiga la lista a todos los servidores de licencias. Pasar la lista al SDK mediante la configuración `HandlerConfiguration.setPolicyUpdateList()`. Si se proporciona una lista de actualización, el SDK consulta esta lista al analizar los metadatos de contenido. `ContentInfo.getUpdatedPolicies()` contiene las versiones actualizadas de las directivas especificadas en los metadatos.

Consulte [Trabajar Con Directivas](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) y [Listas de actualización de directivas.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
