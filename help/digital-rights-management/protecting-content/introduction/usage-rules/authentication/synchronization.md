---
title: Requisitos para la sincronización
description: Requisitos para la sincronización
copied-description: true
exl-id: 0368e363-893f-4b51-a317-00791d0ab54f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Requisitos para la sincronización {#requirements-for-synchronization}

Los requisitos para la sincronización especifican la frecuencia con la que el cliente sincroniza su estado con el servidor. Si se ha emitido una licencia fuera de banda al cliente (sin que se haya establecido contacto con un servidor de licencias), las reglas de uso pueden especificar que el cliente debe enviar mensajes de sincronización al servidor para sincronizar la hora segura del cliente e informar del estado del cliente al servidor.

El comportamiento de sincronización se define mediante los siguientes parámetros:

* **Intervalo de inicio** - Especifica cuánto tiempo se debe esperar después de la última sincronización correcta para iniciar otra solicitud de sincronización.
* **Intervalo de detención rígida** - (Opcional). No permitir la reproducción si no se ha producido una sincronización correcta en el tiempo especificado.
* **Forzar probabilidad de sincronización** - (Opcional). Probabilidad con la que el cliente debe enviar un mensaje de sincronización antes del siguiente intervalo de inicio.

>[!NOTE]
>
>Esta regla de uso es compatible con la versión 3.0 o posterior de los clientes de DRM de Primetime. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente que admita el servidor de licencias.
