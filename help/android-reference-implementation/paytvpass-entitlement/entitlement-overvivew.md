---
description: El Administrador de asignación de derechos es el administrador de funciones que admite la implementación de autenticación Primetime.
seo-description: El Administrador de asignación de derechos es el administrador de funciones que admite la implementación de autenticación Primetime.
seo-title: Información general de Entitlement Manager
title: Información general de Entitlement Manager
uuid: b33dfae3-a132-4215-9992-80cbf4c87a61
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Información general de Entitlement Manager {#entitlement-manager-overview}

El Administrador de asignación de derechos es el administrador de funciones que admite la implementación de autenticación Primetime.

## Información general de características

La integración de autenticación Primetime con la implementación de referencia del SDK de Android Primetime agrega un nuevo administrador de funciones a la aplicación. Sin embargo, a diferencia de muchos otros administradores de funciones, *el administrador de asignación de derechos se utiliza en varios lugares de la aplicación*. A continuación se proporciona una descripción general de los cambios y las adiciones realizados en la implementación de referencia para admitir la autenticación Primetime:

### Clase EntitlementManager

La `EntitlementManager` clase gestiona toda la comunicación con el SDK de autenticación Primetime, además de encapsular la lógica de aplicación necesaria para los flujos de trabajo de asignación de derechos. La aplicación utiliza la API pública `EntitlementManager`de para iniciar flujos de trabajo de asignación de derechos, mientras que la `EntitlementMangerListener` interfaz proporciona un mecanismo de devolución de llamada para que la aplicación gestione `EntitlementManger` eventos.

### Devoluciones de llamada de EntitlementManager

La actividad principal de la implementación de referencia, el `CatalogActivity`, crea una instancia de `EntitlementManagerListener` y la registra con el `EntitlementManager`. De este modo, la interfaz de usuario `EntitlementManager` puede indicar las actualizaciones necesarias para el resto de la aplicación. Las rellamadas incluyen mostrar u ocultar un cuadro de diálogo de carga, mostrar cuadros de diálogo de estado, actualizar los iconos de autorización y autenticación y comenzar la reproducción de vídeo tras una autorización correcta.

### Cuadros de diálogo de asignación de derechos

La `EntitlementDialogFragment` clase genera mensajes de diálogo basados en el estado de asignación de derechos que se pasa al constructor de la clase. Esta clase se utiliza para los mensajes de éxito de autenticación, así como para todos los mensajes de error. El `CatalogActivity` muestra los cuadros de diálogo de asignación de derechos cuando recibe eventos específicos del `EntitlementManager`. Además, `CatalogActivity` implementa la `EntitlementDialogListener` interfaz, que incluye métodos de llamada de retorno para indicar cuándo se cierra un cuadro de diálogo o cuándo el usuario cierra sesión en el servicio de autenticación Primetime.

### Selección e inicio de sesión del proveedor de contenido

Durante la autenticación con autenticación Primetime, dos actividades nuevas `MvpdPickerActivity` y `MvpdLoginActivity`, permiten al usuario seleccionar su proveedor de contenido e iniciar sesión. Ambas actividades se inician desde el `CatalogActivity` sitio web a través del `EntitlementManager`. Además, los resultados `MvpdPickerActivity` y `MvpdLoginActivity` devuelven al `CatalogActivity` y, por lo tanto, el `CatalogActivity` método debe anular el `Activity.onActivityResult` .

### Botón Iniciar sesión

La actividad principal de la implementación de referencia, la `CatalogActivity`, incluye un nuevo botón &quot;Iniciar sesión&quot; en la barra de acciones. El botón Iniciar sesión permite al usuario iniciar la autenticación con la autenticación Primetime. Además, el usuario puede iniciar la autenticación seleccionando un vídeo protegido para la reproducción. El icono y el texto del botón Iniciar sesión cambian según el estado de autenticación del usuario y `CatalogActivity` contienen código para actualizar el icono y el texto del botón cuando se actualiza la página. Para ello, cuando `CatalogActivity` se inicia, llama `EntitlementManager.checkAuthentication()` a actualizar el estado de autenticación del usuario.

### Asignación de contenido

Dentro del `CatalogView`, se muestran nuevos iconos en la parte superior del icono del contenido para indicar el estado de autorización del usuario para dicho contenido. Por ejemplo, si el usuario está autorizado previamente para ver un vídeo, se muestra un icono de círculo verde sobre el contenido. Sin embargo, si el usuario no tiene autorización previa para ver el vídeo, se muestra un icono de clave. La visualización de estos iconos se gestiona en `ContentTileAdapter`, pero la actualización de su estado se inicia desde el `CatalogActivity` momento en que se llama a una llamada de retorno en el `EntitlementManagerListener` .

### Reproducción de contenido

La reproducción de vídeo ahora requiere una comprobación de autorización por parte del `EntitlementManager`. La llamada a `EntitlementManager.getAuthorization()` se produce dentro de `CatalogView`. Si el vídeo requiere autorización y el usuario está autorizado, `PlayerActivity` se inicia desde el `CatalogActivity`.

