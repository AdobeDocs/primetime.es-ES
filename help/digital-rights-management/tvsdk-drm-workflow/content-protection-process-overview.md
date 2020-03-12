---
seo-title: Información general sobre el proceso de adquisición de licencias
title: Información general sobre el proceso de adquisición de licencias
uuid: c2eedd0a-3e3a-4c2f-a781-855f0ba65b15
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Información general sobre el proceso de adquisición de licencias{#license-acquisition-process-overview}

La habilitación de la aplicación para reproducir contenido bajo la protección de Primetime DRM se describe en las siguientes secciones, utilizando ejemplos de código de ActionScript 3 (AS3). Las desviaciones matizadas de este flujo de trabajo para las aplicaciones nativas en plataformas móviles se presentan cuando corresponde. Sin embargo, los flujos de trabajo de DRM Primetime son muy similares en todas las plataformas, por lo que su comprensión del código AS3 hará que la extrapolación a otras plataformas sea bastante sencilla.

**Proceso de adquisición de licencias:**

1. Obtenga los metadatos DRM del contenido protegido.
1. Compruebe si hay una licencia disponible localmente:

   * Si la licencia está disponible localmente, cargue la licencia y vaya al paso 6.
   * Si la licencia no está disponible localmente, continúe con el paso 3.

1. Compruebe si se requiere autenticación:

   * Si se requiere autenticación, obtenga las credenciales de autenticación del usuario y páselas al servidor de licencias.
   * Si no se requiere autenticación, vaya al paso 6.

1. Si es necesario registrarse en el dominio del dispositivo, únase al dominio del dispositivo.
1. Si la autenticación era necesaria y se ha completado, descargue la licencia del servidor de licencias.
1. Reproduzca el contenido.

Si no se producen errores y el usuario ha recibido la autorización necesaria para ver el contenido, Primetime distribuye un `DRMStatusEvent` objeto y la aplicación inicia la reproducción. El `DRMStatusEvent` objeto contiene la información de licencia relacionada, que identifica la política y los permisos del usuario. Por ejemplo, `DRMStatusEvent` puede contener información sobre si el contenido puede estar disponible sin conexión, cuándo caduca la licencia, etc.

La aplicación puede utilizar la información de la licencia para informar al usuario del estado de su política. Por ejemplo, la aplicación puede mostrar el número de días restantes que el usuario tiene para ver el contenido en una barra de estado. Si se permite al usuario el acceso sin conexión, la licencia se almacena en caché y el contenido cifrado se descarga en el equipo del usuario. El contenido se hace accesible durante el tiempo definido en la duración del almacenamiento en caché de la licencia. La propiedad detail del evento contiene `DRM.voucherObtained`. La aplicación decide dónde almacenar el contenido localmente para que esté disponible sin conexión. También puede precargar licencias mediante la `DRMManager` clase.
