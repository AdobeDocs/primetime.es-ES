---
title: Requisitos para la sincronización
description: Requisitos para la sincronización
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Requisitos para la sincronización {#requirements-for-synchronization}

Los requisitos para la sincronización especifican la frecuencia con la que el cliente sincroniza su estado con el servidor. Si se ha emitido una licencia fuera de banda al cliente (sin ponerse en contacto con un servidor de licencias), las reglas de uso pueden especificar que el cliente debe enviar mensajes de sincronización al servidor para sincronizar el tiempo seguro del cliente e informar del estado del cliente al servidor.

El comportamiento de sincronización se define mediante los siguientes parámetros:

* **Intervalo de inicio** : especifica cuánto tiempo se debe esperar después de la última sincronización correcta para iniciar otra solicitud de sincronización.
* **Intervalo de detención**  grave (opcional). No permitir la reproducción si no se ha producido una sincronización correcta en el tiempo especificado.
* **Forzar Probabilidad**  De Sincronización (Opcional). Probabilidad con la que el cliente debe enviar un mensaje de sincronización antes del siguiente intervalo de inicio.

>[!NOTE]
>
>Esta regla de uso es compatible con los clientes de Primetime DRM versión 3.0 o posterior. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente admitida por el servidor de licencias.

