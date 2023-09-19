---
description: El Administrador de derechos es el administrador de funciones que admite la implementación de autenticación de Primetime.
title: Información general del administrador de derechos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# Información general del administrador de derechos {#entitlement-manager-overview}

El Administrador de derechos es el administrador de funciones que admite la implementación de autenticación de Primetime.

## Descripción general de funciones

La integración de autenticación de Primetime con la implementación de referencia del SDK de Primetime para Android agrega un nuevo administrador de funciones a la aplicación. Sin embargo, a diferencia de muchos de los otros administradores de funciones, *el Administrador de derechos se utiliza en varios lugares de la aplicación*. A continuación se ofrece una descripción general de los cambios y adiciones realizados en la Implementación de referencia para admitir la autenticación de Primetime:

### clase EntitlementManager

El `EntitlementManager` administra toda la comunicación con el SDK de autenticación de Primetime, además de encapsular la lógica de aplicación necesaria para los flujos de trabajo de asignación de derechos. El `EntitlementManager`La aplicación utiliza la API pública de para iniciar flujos de trabajo de asignación de derechos, mientras que la `EntitlementMangerListener` proporciona un mecanismo de llamada de retorno para que la aplicación lo gestione `EntitlementManger` eventos.

### Llamadas de retorno de EntityManager

La actividad principal de la Implementación de referencia, la `CatalogActivity`, crea una instancia de `EntitlementManagerListener` y lo registra en el `EntitlementManager`. De este modo, la variable `EntitlementManager` puede indicar las actualizaciones de la IU necesarias para el resto de la aplicación. Las llamadas de retorno incluyen mostrar/ocultar un cuadro de diálogo de carga, mostrar cuadros de diálogo de estado, actualizar los iconos de autorización y autenticación e iniciar la reproducción del vídeo tras la autorización correcta.

### Cuadros de diálogo de derechos

El `EntitlementDialogFragment` La clase genera mensajes de diálogo basados en el estado de derecho pasado al constructor de la clase. Esta clase se utiliza para los mensajes de éxito de autenticación así como para todos los mensajes de error. El `CatalogActivity` muestra los cuadros de diálogo de asignación de derechos cuando recibe eventos específicos del `EntitlementManager`. Además, la variable `CatalogActivity` implementa el `EntitlementDialogListener` , que incluye métodos de llamada de retorno para indicar cuándo se cierra un cuadro de diálogo o cuándo el usuario cierra la sesión del servicio de autenticación de Primetime.

### Selección de proveedor de contenido e inicio de sesión

Durante la autenticación con autenticación de Primetime, dos nuevas actividades, `MvpdPickerActivity` y `MvpdLoginActivity`, permita al usuario seleccionar su proveedor de contenido e iniciar sesión. Ambas actividades se inician desde el `CatalogActivity` a través de `EntitlementManager`. Además, tanto la variable `MvpdPickerActivity` y `MvpdLoginActivity` Devolver resultados a `CatalogActivity` y, por lo tanto, `CatalogActivity` debe anular la variable `Activity.onActivityResult` método.

### Botón Iniciar sesión

La actividad principal de la Implementación de referencia, la `CatalogActivity`, incluye un nuevo botón &quot;Iniciar sesión&quot; en la barra de acciones. El botón Iniciar sesión permite al usuario iniciar la autenticación con la autenticación de Primetime. Además, el usuario puede iniciar la autenticación seleccionando un vídeo protegido para su reproducción. El icono y el texto del botón Iniciar sesión cambian según el estado de autenticación del usuario y la variable `CatalogActivity` contiene código para actualizar el icono y el texto del botón cuando se actualiza la página. Para ello, cuando la variable `CatalogActivity` comienza, llama `EntitlementManager.checkAuthentication()` para actualizar el estado de autenticación del usuario.

### Derechos de contenido

Dentro de `CatalogView`, los nuevos iconos se muestran sobre el icono del contenido para indicar el estado de autorización del usuario para ese contenido. Por ejemplo, si el usuario está preautorizado para ver un vídeo, se muestra un icono de círculo verde sobre el contenido. Sin embargo, si el usuario no tiene autorización previa para ver el vídeo, se muestra un icono de tecla. La visualización de estos iconos se gestiona en `ContentTileAdapter`, sin embargo, la actualización de su estado se inicia desde el `CatalogActivity` cuando una llamada de retorno en `EntitlementManagerListener` se llama.

### Reproducción de contenido

La reproducción de vídeo ahora requiere una comprobación de autorización por parte del `EntitlementManager`. La llamada a `EntitlementManager.getAuthorization()` ocurre en `CatalogView`. Si el vídeo requiere autorización y el usuario está autorizado, la variable `PlayerActivity` se inicia desde el `CatalogActivity`.
