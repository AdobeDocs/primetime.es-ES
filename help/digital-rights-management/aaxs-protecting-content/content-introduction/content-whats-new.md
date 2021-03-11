---
description: 'Adobe® Access™ es una avanzada solución de protección de contenidos y gestión de derechos digitales para contenido audiovisual de alto valor. Con las herramientas que crea mediante las API de Java, puede crear políticas, aplicar políticas a archivos que contengan contenido de audio y vídeo y cifrar esos archivos. Los pasos de alto nivel para realizar estas tareas son los siguientes '
title: Información general
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Información general {#overview}

Adobe® Access™ es una avanzada solución de protección de contenidos y gestión de derechos digitales para contenido audiovisual de alto valor. Con las herramientas que crea mediante las API de Java, puede crear políticas, aplicar políticas a archivos que contengan contenido de audio y vídeo y cifrar esos archivos. Los pasos de alto nivel para realizar estas tareas son los siguientes:

1. Utilice las API de Java para establecer las propiedades de la directiva y los parámetros de codificación.
1. Cree una directiva que describa las funciones de uso del contenido. (Consulte [Trabajo con directivas](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)).

   Puede crear cualquier número de directivas. La mayoría de los usuarios crean un pequeño número de directivas y las aplican a muchos archivos.

1. Empaquete un archivo multimedia.

   En este contexto, *empaquetar un archivo* significa cifrarlo y aplicarle una política. (Consulte [Empaquetado de archivos multimedia](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md)).

1. Implemente el servidor de licencias para emitir una licencia al usuario.

El contenido cifrado ya está listo para su implementación y el cliente puede solicitar la licencia al servidor.

El SDK proporciona una API de Java para realizar estas tareas e incluye implementaciones de referencia del servidor de licencias y herramientas de línea de comandos basadas en las API de Java. Para obtener más información, consulte *Uso de las implementaciones de referencia de acceso a Adobe*.

## Novedades de Adobe Access 5.2 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **CEK** externo: La capacidad de integrar un sistema de administración de claves de contenido (CKMS) en los flujos de trabajo de servicio de licencias DRM y paquetes de contenido, en lugar de cifrar el CEK y agregarlo a los metadatos del contenido. Consulte [Información general del CEK externo DRM de acceso al Adobe](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).

* **Regreso** de licencia (cupón): Capacidad de un cliente para devolver (o eliminar) una licencia emitida al cliente.
* **Servidor** de claves Xbox: La capacidad de proteger el contenido enviado a Xbox y Xbox 360. (Se requiere un cliente de Adobe Primetime).

## Reglas de uso personalizadas {#custom-usage-rules}

Especifica reglas de uso personalizadas. Los datos personalizados se pueden incluir en las licencias emitidas por el servidor de licencias. La interpretación/gestión de estos datos depende completamente de la implementación de la aplicación cliente y del servidor de licencias.

Ejemplo de caso de uso: Permite la extensibilidad de las reglas de uso al permitir que otras reglas comerciales se transmitan de forma segura como parte de la directiva o la licencia de contenido. Por motivos de seguridad, dado que estas reglas de uso se aplican en el código personalizado de la aplicación cliente, esta opción debe utilizarse junto con las opciones de lista de permitidos SWF de la aplicación de AIR o del Flash Player. Para obtener más información, consulte [Restricciones de tiempo de ejecución y aplicación](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md).
