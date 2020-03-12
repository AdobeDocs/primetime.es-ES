---
description: 'null'
seo-description: 'null'
seo-title: Requisitos para la sincronización
title: Requisitos para la sincronización
uuid: 594a4bb2-c042-4485-9cae-73b8f9f93d82
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Requisitos para la sincronización {#requirements-for-synchronization}

Los requisitos para la sincronización especifican la frecuencia con la que el cliente sincroniza su estado con el servidor. Si al cliente se le ha emitido una licencia fuera de banda (sin que se haya establecido contacto con un servidor de licencias), las reglas de uso pueden especificar que el cliente debe enviar mensajes de sincronización al servidor para sincronizar el tiempo seguro del cliente e informar del estado del cliente al servidor.

El comportamiento de sincronización se define con los siguientes parámetros:

* **Intervalo** de inicio: especifica cuánto tiempo se debe esperar después de la última sincronización correcta para iniciar otra solicitud de sincronización.
* **Intervalo** de detención dura (opcional). No permitir la reproducción si no se ha producido una sincronización correcta en el tiempo especificado.
* **Forzar la probabilidad** de sincronización: (opcional). Probabilidad con la que el cliente debe enviar un mensaje de sincronización antes del siguiente intervalo de inicio.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Esta regla de uso es compatible con los clientes Primetime DRM versión 3.0 o posterior. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente admitida por el servidor de licencias.

