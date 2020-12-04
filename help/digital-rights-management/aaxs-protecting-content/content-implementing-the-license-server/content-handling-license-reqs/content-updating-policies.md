---
seo-title: Actualización de directivas
title: Actualización de directivas
uuid: f6686c8b-bedf-4ec5-a14e-f03326519f89
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Actualizando directivas {#updating-policies}

Si las directivas se actualizan después de empaquetar el contenido, proporcione las directivas actualizadas al servidor de licencias para que se pueda utilizar la versión actualizada al emitir una licencia. Si el servidor de licencias tiene acceso a una base de datos para almacenar directivas, puede recuperar la directiva actualizada de la base de datos y llamar a `LicenseRequestMessage.setSelectedPolicy()` para proporcionar la nueva versión de la directiva.

Para los servidores de licencias que no dependen de una base de datos central, el SDK proporciona compatibilidad con Listas de actualización de directivas. Una lista de actualización de directiva es un archivo que contiene una lista de directivas actualizadas o revocadas. Cuando se actualice una directiva, genere una nueva Lista de actualización de directiva y envíe periódicamente la lista a todos los servidores de licencias. Pase la lista al SDK estableciendo `HandlerConfiguration.setPolicyUpdateList()`. Si se proporciona una lista de actualización, el SDK consulta esta lista al analizar los metadatos del contenido. `ContentInfo.getUpdatedPolicies()` contiene las versiones actualizadas de las directivas especificadas en los metadatos.

Consulte [Trabajo con directivas](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) y [listas de actualización de políticas.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
