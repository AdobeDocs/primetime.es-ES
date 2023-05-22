---
title: Requisitos para la sincronización
description: Requisitos para la sincronización
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Requisitos para la sincronización{#requirements-for-synchronization}

Especifica la frecuencia con la que el cliente sincronizará su estado con el servidor. Si se ha emitido una licencia fuera de banda al cliente (sin que se haya establecido contacto con un servidor de licencias), las reglas de uso pueden especificar que el cliente debe enviar mensajes de sincronización al servidor para sincronizar la hora segura del cliente y notificar el estado del cliente al servidor.

El comportamiento de sincronización se define mediante los siguientes parámetros:

* Intervalo de inicio: especifica el tiempo de espera después de la última sincronización correcta para iniciar otra solicitud de sincronización.
* Intervalo de detención rígida (opcional). No permitir la reproducción si no se ha producido una sincronización correcta en el tiempo especificado.
* Forzar probabilidad de sincronización (opcional). Probabilidad con la que el cliente debe enviar un mensaje de sincronización antes del siguiente intervalo de inicio.

>[!NOTE]
>
>Esta regla de uso es compatible con la versión 3.0 y posteriores de los clientes de Adobe Access. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente que admita el servidor de licencias. Consulte. [Versión mínima del cliente](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).

