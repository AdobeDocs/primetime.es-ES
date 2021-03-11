---
title: Resumen del proceso de adquisición de licencias
description: Resumen del proceso de adquisición de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# Descripción general del proceso de adquisición de licencias{#license-acquisition-process-overview}

En las siguientes secciones se describe cómo permitir que la aplicación reproduzca contenido bajo la protección de Primetime DRM, utilizando muestras de código de ActionScript 3 (AS3). Las desviaciones matizadas de este flujo de trabajo para aplicaciones nativas en plataformas móviles se presentan cuando corresponde. Sin embargo, los flujos de trabajo de DRM de Primetime son muy similares en todas las plataformas, por lo que su comprensión del código AS3 hará que la extrapolación a otras plataformas sea bastante sencilla.

**Proceso de adquisición de licencias:**

1. Obtenga los metadatos DRM del contenido protegido.
1. Compruebe si una licencia está disponible localmente:

   * Si la licencia está disponible localmente, cargue la licencia y vaya al paso 6.
   * Si la licencia no está disponible localmente, continúe con el paso 3.

1. Compruebe si se requiere autenticación:

   * Si se requiere autenticación, obtenga las credenciales de autenticación del usuario y páselas al servidor de licencias.
   * Si la autenticación no es necesaria, vaya al paso 6.

1. Si es necesario registrar el dominio del dispositivo, únase al dominio del dispositivo.
1. Si la autenticación era necesaria y ya se ha completado, descargue la licencia del servidor de licencias.
1. Reproducir el contenido.

Si no se produjeron errores y el usuario recibió autorización para ver el contenido, Primetime envía un objeto `DRMStatusEvent` y la aplicación comienza la reproducción. El objeto `DRMStatusEvent` contiene la información de licencia relacionada, que identifica la política y los permisos del usuario. Por ejemplo, `DRMStatusEvent` puede contener información sobre si el contenido puede estar disponible sin conexión, cuándo caduca la licencia, etc.

La aplicación puede utilizar la información de licencia para informar al usuario del estado de su política. Por ejemplo, la aplicación puede mostrar el número de días restantes que el usuario tiene para ver el contenido en una barra de estado. Si al usuario se le permite el acceso sin conexión, la licencia se almacena en caché y el contenido cifrado se descarga en el equipo del usuario. Se puede acceder al contenido durante el tiempo definido en la duración del almacenamiento en caché de la licencia. La propiedad detail del evento contiene `DRM.voucherObtained`. La aplicación decide dónde almacenar el contenido localmente para que esté disponible sin conexión. También puede precargar licencias utilizando la clase `DRMManager` .
