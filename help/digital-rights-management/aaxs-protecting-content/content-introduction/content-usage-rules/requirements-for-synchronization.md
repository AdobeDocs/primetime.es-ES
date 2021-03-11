---
title: Requisitos para la sincronización
description: Requisitos para la sincronización
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Requisitos para la sincronización{#requirements-for-synchronization}

Especifica la frecuencia con la que el cliente sincronizará su estado con el servidor. Si se ha emitido una licencia fuera de banda al cliente (sin ponerse en contacto con un servidor de licencias), las reglas de uso pueden especificar que el cliente debe enviar mensajes de sincronización al servidor para sincronizar la hora segura del cliente y el estado del cliente de informes con el servidor.

El comportamiento de sincronización se define mediante los siguientes parámetros:

* Intervalo de inicio: especifica cuánto tiempo se debe esperar después de la última sincronización correcta para iniciar otra solicitud de sincronización.
* Intervalo de detención de disco duro (opcional). No permitir la reproducción si no se ha producido una sincronización correcta en el tiempo especificado.
* Forzar Probabilidad De Sincronización — (Opcional). Probabilidad con la que el cliente debe enviar un mensaje de sincronización antes del siguiente intervalo de inicio.

>[!NOTE]
>
>Esta regla de uso es compatible con los clientes de acceso a Adobe versión 3.0 y posteriores. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente admitida por el servidor de licencias. Consulte [Versión mínima del cliente](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).

