---
description: El administrador de derechos es el administrador de funciones que admite la implementación de autenticación de Primetime.
title: Información general del administrador de derechos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# Información general del Administrador de derechos {#entitlement-manager-overview}

El administrador de derechos es el administrador de funciones que admite la implementación de autenticación de Primetime.

## Descripción general de características

La integración de autenticación de Primetime con la implementación de referencia del SDK de Android Primetime agrega un nuevo administrador de funciones a la aplicación. Sin embargo, a diferencia de muchos de los demás administradores de funciones, *el administrador de derechos se utiliza en varios lugares de la aplicación*. A continuación se proporciona una descripción general de los cambios y adiciones realizados en la Implementación de referencia para admitir la autenticación de Primetime:

### Clase EntitlementManager

La clase `EntitlementManager` gestiona toda la comunicación con el SDK de autenticación de Primetime, además de encapsula la lógica de aplicación necesaria para los flujos de trabajo de asignación de derechos. La API pública de `EntitlementManager` la utiliza la aplicación para iniciar flujos de trabajo de derechos, mientras que la interfaz `EntitlementMangerListener` proporciona un mecanismo de devolución de llamada para que la aplicación gestione eventos `EntitlementManger`.

### Rellamadas de retorno de EntitlementManager

La actividad principal de la Implementación de referencia, `CatalogActivity`, crea una instancia de `EntitlementManagerListener` y la registra con `EntitlementManager`. De este modo, `EntitlementManager` puede indicar las actualizaciones de UI necesarias para el resto de la aplicación. Las llamadas de retorno incluyen mostrar u ocultar un cuadro de diálogo de carga, mostrar los cuadros de diálogo de estado, actualizar los iconos de autorización y autenticación e iniciar la reproducción de vídeo tras una autorización correcta.

### Cuadros de diálogo de derechos

La clase `EntitlementDialogFragment` genera mensajes de diálogo basados en el estado de la asignación de derechos pasado al constructor de clases. Esta clase se utiliza para los mensajes de éxito de autenticación, así como para todos los mensajes de error. El `CatalogActivity` muestra los cuadros de diálogo de asignación de derechos cuando recibe eventos específicos del `EntitlementManager`. Además, `CatalogActivity` implementa la interfaz `EntitlementDialogListener` , que incluye métodos de rellamada para indicar cuándo se cierra un cuadro de diálogo o cuándo el usuario cierra la sesión del servicio de autenticación de Primetime.

### Selección e inicio de sesión del proveedor de contenido

Durante la autenticación con autenticación de Primetime, dos nuevas actividades, `MvpdPickerActivity` y `MvpdLoginActivity`, permiten al usuario seleccionar su proveedor de contenido e iniciar sesión. Ambas actividades se inician desde `CatalogActivity` a través de `EntitlementManager`. Además, tanto `MvpdPickerActivity` como `MvpdLoginActivity` devuelven los resultados a `CatalogActivity` y, por lo tanto, el `CatalogActivity` debe anular el método `Activity.onActivityResult`.

### Botón Iniciar sesión

La actividad principal de Implementación de referencia, `CatalogActivity`, incluye un nuevo botón &quot;Iniciar sesión&quot; en su barra de acciones. El botón Iniciar sesión permite al usuario iniciar la autenticación con autenticación de Primetime. Además, el usuario puede iniciar la autenticación seleccionando un vídeo protegido para la reproducción. El icono y el texto del botón Iniciar sesión cambian según el estado de autenticación del usuario, y `CatalogActivity` contiene código para actualizar el icono y el texto del botón cuando se actualiza la página. Para ello, cuando se inicia el `CatalogActivity`, llama a `EntitlementManager.checkAuthentication()` para actualizar el estado de autenticación del usuario.

### Asignación de contenido

Dentro de `CatalogView`, se muestran nuevos iconos sobre el icono del contenido para indicar el estado de autorización del usuario para dicho contenido. Por ejemplo, si el usuario tiene autorización previa para ver un vídeo, se muestra un icono de círculo verde sobre el contenido. Sin embargo, si el usuario no tiene autorización previa para ver el vídeo, se muestra un icono de clave. La visualización de estos iconos se gestiona en `ContentTileAdapter`, pero la actualización de su estado se inicia desde `CatalogActivity` cuando se llama a una llamada de retorno en `EntitlementManagerListener`.

### Reproducción de contenido

La reproducción de vídeo ahora requiere una comprobación de autorización por parte de `EntitlementManager`. La llamada a `EntitlementManager.getAuthorization()` se produce dentro de `CatalogView`. Si el vídeo requiere autorización y el usuario está autorizado, el `PlayerActivity` se inicia desde el `CatalogActivity`.

