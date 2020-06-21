---
description: 'Adobe® Access™ es una solución avanzada de administración de derechos digitales y protección de contenido para contenido audiovisual de alto valor. Mediante las herramientas que cree con las API de Java, puede crear políticas, aplicar políticas a los archivos que contengan contenido de audio y vídeo y cifrar dichos archivos. Los pasos de alto nivel para realizar estas tareas son los siguientes '
seo-description: 'Adobe® Access™ es una solución avanzada de administración de derechos digitales y protección de contenido para contenido audiovisual de alto valor. Mediante las herramientas que cree con las API de Java, puede crear políticas, aplicar políticas a los archivos que contengan contenido de audio y vídeo y cifrar dichos archivos. Los pasos de alto nivel para realizar estas tareas son los siguientes '
seo-title: Información general
title: Información general
uuid: 874c175b-8207-49fa-aad4-204ccbee9c2c
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Información general {#overview}

Adobe® Access™ es una solución avanzada de administración de derechos digitales y protección de contenido para contenido audiovisual de alto valor. Mediante las herramientas que cree con las API de Java, puede crear políticas, aplicar políticas a los archivos que contengan contenido de audio y vídeo y cifrar dichos archivos. Los pasos de alto nivel para realizar estas tareas son los siguientes:

1. Utilice las API de Java para establecer las propiedades de directiva y los parámetros de codificación.
1. Cree una directiva que describa las funciones de uso del contenido. (Consulte [Uso de políticas](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)).

   Puede crear cualquier número de directivas. La mayoría de los usuarios crea un pequeño número de directivas y las aplica a muchos archivos.

1. Empaquete un archivo multimedia.

   En este contexto, *empaquetar un archivo* significa cifrarlo y aplicarle una política. (Consulte [Empaquetado de archivos](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md)multimedia).

1. Implemente el servidor de licencias para emitir una licencia al usuario.

El contenido cifrado ya está listo para la implementación y el cliente puede solicitar la licencia al servidor.

El SDK proporciona una API de Java para realizar estas tareas e incluye implementaciones de referencia del servidor de licencias y herramientas de línea de comandos basadas en las API de Java. Para obtener más información, consulte *Uso de las implementaciones* de referencia de Adobe Access.

## Novedades de Adobe Access 5.2 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **CEK** externo: La capacidad de integrar un sistema de administración de claves de contenido (CKMS) al servicio de licencias DRM y a los flujos de trabajo de empaquetado de contenido, en lugar de cifrar el CEK y agregarlo a los metadatos del contenido. Consulte [Información general](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)de CEK externo de DRM de Adobe Access.

* **Devolución** de licencia (vale): Capacidad de un cliente para devolver (o eliminar) una licencia emitida al cliente.
* **Servidor** de claves Xbox: La capacidad de proteger el contenido enviado a la Xbox y a la Xbox 360. (Se requiere un cliente Adobe Primetime).

## Reglas de uso personalizadas {#custom-usage-rules}

Especifica reglas de uso personalizadas. Los datos personalizados pueden incluirse en las licencias emitidas por el servidor de licencias. La interpretación y el manejo de estos datos depende completamente de la implementación de la aplicación cliente y del servidor de licencias.

Ejemplo de caso de uso: Permite la extensibilidad de las reglas de uso al permitir que otras reglas comerciales se transmitan de forma segura como parte de la política o licencia de contenido. Por motivos de seguridad, como estas reglas de uso se aplican en el código de la aplicación cliente personalizada, esta opción debe usarse junto con la aplicación de AIR o con las opciones de lista de permitidas por Flash Player SWF. Para obtener más información, consulte &quot;Restricciones[de](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md)tiempo de ejecución y aplicación&quot;.
