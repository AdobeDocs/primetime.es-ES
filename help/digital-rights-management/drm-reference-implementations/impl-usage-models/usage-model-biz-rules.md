---
description: 'null'
seo-description: 'null'
seo-title: Modelo de uso demostración de reglas comerciales
title: Modelo de uso demostración de reglas comerciales
uuid: c55f85be-5ecb-4a78-b47d-7001ec207d3a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Modelo de uso demostración de reglas comerciales{#usage-model-demo-business-rules}

Cuando un usuario solicita una licencia, el servidor de implementación de referencia comprueba los metadatos que el cliente ha enviado para determinar si el contenido se empaquetó con la `RI_UsageModelDemo` propiedad . Si ese es el caso, el servidor aplica las siguientes reglas comerciales.

* Si una de las directivas de DRM requiere autenticación:

   * Si la solicitud contiene un token de autenticación válido, busque el nombre del usuario en la tabla Base de datos de clientes.

      Si no encuentra el nombre del usuario, complete las siguientes tareas:

      * Si la `Customer.IsSubscriber` propiedad está establecida en `true`, debe generar una licencia para el modelo de *`Subscription`* uso y enviarla al usuario.

      * Busque un registro en la tabla de la `CustomerAuthorization` base de datos para el nombre del usuario y el ID de contenido.
      Si puede localizar el registro del usuario, complete las siguientes tareas:

      * Si la `CustomerAuthorization.UsageType` propiedad está establecida en `DTO`, genere una licencia para el modelo de uso de DTO y envíela al usuario.

      * Si la `CustomerAuthorization.UsageType` propiedad está establecida en `VOD`, genere una licencia para el modelo de uso de VOD y envíela al usuario.
      Si ninguna de las directivas de DRM permite el acceso anónimo, complete las siguientes tareas:

      * Si no hay un token de autenticación válido en la solicitud, debe devolver un error de &quot;autenticación requerida&quot;.
      * De lo contrario, devuelve un error &quot;no autorizado&quot;.



* Si una de las políticas de DRM permite el acceso anónimo, genere una licencia para el modelo de uso financiado con publicidad y envíela al usuario.

