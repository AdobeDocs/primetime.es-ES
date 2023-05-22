---
title: Información general sobre el trabajo con políticas DRM
description: Información general sobre el trabajo con políticas DRM
copied-description: true
exl-id: 734d0be3-2abe-400c-bc34-00046ec52f4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Información general {#working-with-drm-policies-overview}

Los proveedores de contenido pueden aplicar directivas DRM a archivos multimedia mediante el SDK de DRM de Primetime. Los administradores pueden crear, ver detalles y actualizar directivas de DRM mediante las API de administración de directivas.

A *`DRM policy`* es una recopilación de información que incluye configuraciones de seguridad, requisitos de autenticación y derechos de uso. La directiva define cómo los usuarios pueden ver el contenido. Las políticas, el cifrado y la firma de DRM permiten a los proveedores de contenido mantener el control de su contenido, independientemente de la amplitud con la que se distribuya.

Una directiva DRM sirve como plantilla que el servidor de licencias utiliza cuando genera una licencia. Un cliente también puede hacer referencia a la directiva DRM antes de solicitar una licencia, para determinar si el cliente necesita solicitar la autenticación al usuario antes de emitir una solicitud de licencia al servidor.

Puede enviar contenido protegido mediante el Flash Media Server de Adobe o un servidor HTTP. Los usuarios pueden descargar y reproducir contenido protegido en reproductores personalizados creados con el SDK de DRM de Primetime.

Una directiva DRM especifica uno o varios derechos que se conceden al cliente. Normalmente, una política de DRM incluye, como mínimo, la *`Play Right`*. También puede especificar varios derechos de reproducción, cada uno con diferentes restricciones. Cuando el cliente recibe una licencia con varios derechos de reproducción, utiliza la primera licencia que cumple todas las restricciones. Por ejemplo, puede aplicar diferentes configuraciones de protección de salida en diferentes plataformas.

Consulte `CreatePolicyWithOutputProtection.java` en las herramientas de línea de comandos de implementación de referencia [!DNL samples] directorio para el código de ejemplo que ilustra este ejemplo.

Puede completar las siguientes tareas con las API de administración de directivas DRM de Primetime:

* Crear y actualizar directivas
* Ver detalles de la política de DRM
* Administrar listas de actualización de directivas DRM

Consulte la *Referencia de API de DRM de Primetime* para obtener más información sobre la API de Java.

Consulte la *Uso de las implementaciones de referencia de DRM de Primetime* para obtener información sobre el Administrador de políticas de DRM de Primetime.
