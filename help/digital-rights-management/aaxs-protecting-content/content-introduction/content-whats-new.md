---
description: Adobe ® Access™ es una solución avanzada de gestión de derechos digitales y protección de contenidos para contenidos audiovisuales de alto valor. Con las herramientas que crea con las API de Java, puede crear directivas, aplicar directivas a archivos que contienen contenido de audio y vídeo y cifrar esos archivos. Los pasos de alto nivel para realizar estas tareas son los siguientes
title: Información general
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Información general {#overview}

Adobe ® Access™ es una solución avanzada de gestión de derechos digitales y protección de contenidos para contenidos audiovisuales de alto valor. Con las herramientas que crea con las API de Java, puede crear directivas, aplicar directivas a archivos que contienen contenido de audio y vídeo y cifrar esos archivos. Los pasos de alto nivel para realizar estas tareas son los siguientes:

1. Utilice las API de Java para establecer las propiedades de la directiva y los parámetros de cifrado.
1. Cree una política que describa las funciones de uso del contenido. (Consulte [Uso de directivas](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)).

   Puede crear cualquier número de directivas. La mayoría de los usuarios crea un pequeño número de directivas y las aplica a muchos archivos.

1. Empaquete un archivo multimedia.

   En este contexto, *empaquetar un archivo* significa cifrarlo y aplicarle una directiva. (Consulte [Empaquetando archivos multimedia](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md).)

1. Implemente el servidor de licencias para emitir una licencia al usuario.

El contenido cifrado ya está listo para su implementación y el cliente puede solicitar la licencia al servidor.

El SDK proporciona una API de Java para realizar estas tareas e incluye implementaciones de referencia del servidor de licencias y herramientas de línea de comandos basadas en las API de Java. Para obtener más información, consulte *Uso de las implementaciones de referencia de acceso a Adobe*.

## Novedades de Adobe Access 5.2 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **CEK externo**: la capacidad de integrar un sistema de administración de claves de contenido (CKMS) en los flujos de trabajo de servicio de licencias DRM y empaquetado de contenido, en lugar de cifrar la CEK y empaquetarla en los metadatos del contenido. Consulte [Descripción general de CEK externo de DRM de acceso a Adobe](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).

* **Licencia (cupón) Devolución**: la capacidad de un cliente para devolver (o eliminar) una licencia emitida al cliente.
* **Servidor de claves Xbox**: la capacidad de proteger el contenido enviado a Xbox y Xbox 360. (Se requiere un cliente de Adobe Primetime).

## Reglas de uso personalizadas {#custom-usage-rules}

Especifica reglas de uso personalizadas. Los datos personalizados se pueden incluir en las licencias emitidas por el servidor de licencias. La interpretación/gestión de estos datos depende completamente de la implementación de la aplicación del cliente y del servidor de licencias.

Ejemplo de caso de uso: Habilita la extensibilidad de las reglas de uso al permitir que otras reglas empresariales se transmitan de forma segura como parte de la directiva o la licencia de contenido. Por motivos de seguridad, dado que estas reglas de uso se aplican en el código de aplicación cliente personalizado, esta opción debe utilizarse junto con la aplicación de AIR o las opciones de lista de permitidos del SWF de Flash Player. Para obtener más información, consulte [Restricciones de tiempo de ejecución y aplicaciones](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md).
