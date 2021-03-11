---
title: Modelo de uso de demostración de reglas de negocio
description: Modelo de uso de demostración de reglas de negocio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Modelo de uso de reglas comerciales de demostración{#usage-model-demo-business-rules}

Cuando un usuario solicita una licencia, el servidor de implementación de referencia comprueba los metadatos que ha enviado el cliente para determinar si el contenido se empaquetó con la propiedad `RI_UsageModelDemo` . Si ese es el caso, el servidor aplica las siguientes reglas comerciales.

* Si una de las directivas de DRM requiere autenticación:

   * Si la solicitud contiene un token de autenticación válido, busque el nombre del usuario en la tabla de la base de datos del cliente.

      Si no encuentra el nombre del usuario, complete las siguientes tareas:

      * Si la propiedad `Customer.IsSubscriber` está establecida en `true`, debe generar una licencia para el modelo de uso *`Subscription`* y enviarla al usuario.

      * Busque un registro en la tabla de la base de datos `CustomerAuthorization` para el nombre del usuario y el ID de contenido.

      Si puede localizar el registro del usuario, complete las siguientes tareas:

      * Si la propiedad `CustomerAuthorization.UsageType` está establecida en `DTO`, genere una licencia para el modelo de uso de DTO y envíela al usuario.

      * Si la propiedad `CustomerAuthorization.UsageType` está establecida en `VOD`, genere una licencia para el modelo de uso de VOD y envíela al usuario.

      Si ninguna de las directivas de DRM permite el acceso anónimo, complete las siguientes tareas:

      * Si no hay un token de autenticación válido en la solicitud, debe devolver un error de &quot;autenticación requerida&quot;.
      * De lo contrario, devuelve un error &quot;no autorizado&quot;.



* Si una de las políticas de DRM permite el acceso anónimo, genere una licencia para el modelo de uso financiado por Ad y envíelo al usuario.

