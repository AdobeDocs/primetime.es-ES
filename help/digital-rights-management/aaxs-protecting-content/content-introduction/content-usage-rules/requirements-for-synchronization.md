---
seo-title: Requisitos para la sincronización
title: Requisitos para la sincronización
uuid: 976a0ae1-bece-437e-b95b-6cd222525d13
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Requisitos para la sincronización{#requirements-for-synchronization}

Especifica la frecuencia con la que el cliente sincronizará su estado con el servidor. Si se ha emitido una licencia fuera de banda al cliente (sin que se haya establecido contacto con un servidor de licencias), las reglas de uso pueden especificar que el cliente debe enviar mensajes de sincronización al servidor para sincronizar el tiempo seguro del cliente y notificar el estado del cliente al servidor.

El comportamiento de sincronización se define con los siguientes parámetros:

* Intervalo de inicio — Especifica cuánto tiempo se espera después de la última sincronización correcta para realizar el inicio de otra solicitud de sincronización.
* Intervalo de parada dura — (Opcional). No permitir la reproducción si no se ha producido una sincronización correcta en el tiempo especificado.
* Forzar la probabilidad de sincronización — (Opcional). Probabilidad con la que el cliente debe enviar un mensaje de sincronización antes del siguiente intervalo de inicio.

>[!NOTE]
>
>Esta regla de uso es compatible con los clientes de Adobe Access versión 3.0 y posterior. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente admitida por el servidor de licencias. Consulte Versión [mínima del cliente](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).

