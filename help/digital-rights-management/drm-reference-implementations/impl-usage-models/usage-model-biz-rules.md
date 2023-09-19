---
title: Modelo de uso de reglas empresariales de demostración
description: Modelo de uso de reglas empresariales de demostración
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Modelo de uso de reglas empresariales de demostración{#usage-model-demo-business-rules}

Cuando un usuario solicita una licencia, el servidor de implementación de referencia comprueba los metadatos que ha enviado el cliente para determinar si el contenido se empaquetó utilizando `RI_UsageModelDemo` propiedad. En ese caso, el servidor aplica las siguientes reglas empresariales.

* Si una de las políticas de DRM requiere autenticación:

   * Si la solicitud contiene un token de autenticación válido, busque el nombre del usuario en la tabla de la base de datos de clientes.

     Si no encuentra el nombre del usuario, complete las siguientes tareas:

      * Si la variable `Customer.IsSubscriber` La propiedad se establece en `true`, debe generar una licencia para el *`Subscription`* modelo de uso y enviarlo al usuario.

      * Busque un registro en la `CustomerAuthorization` tabla de base de datos para el nombre del usuario y el ID de contenido.

     Si puede localizar el registro del usuario, complete las siguientes tareas:

      * Si la variable `CustomerAuthorization.UsageType` La propiedad se establece en `DTO`, genere una licencia para el modelo de uso de DTO y envíela al usuario.

      * Si la variable `CustomerAuthorization.UsageType` La propiedad se establece en `VOD`, genere una licencia para el modelo de uso de VOD y envíela al usuario.

     Si ninguna de las políticas de DRM permite el acceso anónimo, complete las siguientes tareas:

      * Si no hay un token de autenticación válido en la solicitud, debe devolver el error &quot;se requiere autenticación&quot;.
      * De lo contrario, devuelve el error &quot;no autorizado&quot;.

* Si una de las políticas de DRM permite el acceso anónimo, genere una licencia para el modelo de uso financiado con publicidad y envíela al usuario.
