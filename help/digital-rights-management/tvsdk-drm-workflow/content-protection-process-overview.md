---
title: Resumen del proceso de adquisición de licencia
description: Resumen del proceso de adquisición de licencia
copied-description: true
exl-id: 0e1c43a5-9a7d-4534-acd6-7feff94f4670
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Resumen del proceso de adquisición de licencia{#license-acquisition-process-overview}

En las siguientes secciones se describe cómo permitir que la aplicación reproduzca contenido con la protección de Primetime DRM, mediante ejemplos de código de ActionScript 3 (AS3). Las diferencias matizadas de este flujo de trabajo para aplicaciones nativas en plataformas móviles se presentan cuando corresponde. Sin embargo, los flujos de trabajo de DRM de Primetime son muy similares en todas las plataformas, por lo que su comprensión del código AS3 hará que la extrapolación a otras plataformas sea bastante sencilla.

**Proceso de adquisición de licencia:**

1. Obtenga los metadatos DRM del contenido protegido.
1. Compruebe si una licencia está disponible localmente:

   * Si la licencia está disponible localmente, cargue la licencia y vaya al paso 6.
   * Si la licencia no está disponible localmente, continúe con el paso 3.

1. Compruebe si se requiere autenticación:

   * Si se requiere autenticación, obtenga las credenciales de autenticación del usuario y páselas al servidor de licencias.
   * Si no se requiere autenticación, vaya al paso 6.

1. Si se requiere el registro del dominio del dispositivo, únase al dominio del dispositivo.
1. Si se necesitaba la autenticación y ahora está completa, descargue la licencia del servidor de licencias.
1. Reproduzca el contenido.

Si no se producen errores y se autoriza correctamente al usuario a ver el contenido, Primetime envía un `DRMStatusEvent` y la aplicación inicia la reproducción. El `DRMStatusEvent` contiene la información de licencia relacionada, que identifica la directiva y los permisos del usuario. Por ejemplo, `DRMStatusEvent` puede contener información sobre si el contenido puede estar disponible sin conexión, cuándo caduca la licencia, etc.

La aplicación puede utilizar la información de la licencia para informar al usuario del estado de su política. Por ejemplo, la aplicación puede mostrar el número de días restantes que el usuario tiene para ver el contenido en una barra de estado. Si se permite al usuario el acceso sin conexión, la licencia se almacena en caché y el contenido cifrado se descarga en el equipo del usuario. El contenido se hace accesible durante la duración definida en la duración del almacenamiento en caché de la licencia. La propiedad detail del evento contiene `DRM.voucherObtained`. La aplicación decide dónde almacenar el contenido localmente para que esté disponible sin conexión. También puede precargar licencias utilizando el `DRMManager` clase.
