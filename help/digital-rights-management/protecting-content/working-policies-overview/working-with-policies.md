---
title: Información general sobre el trabajo con las políticas de DRM
description: Información general sobre el trabajo con las políticas de DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Información general {#working-with-drm-policies-overview}

Los proveedores de contenido pueden aplicar políticas de DRM a archivos multimedia mediante el SDK de Primetime DRM. A continuación, los administradores pueden crear, ver los detalles y actualizar las políticas de DRM mediante las API de administración de directivas.

Una *`DRM policy`* es una colección de información que incluye configuración de seguridad, requisitos de autenticación y derechos de uso. La directiva define cómo pueden ver el contenido los usuarios. Las políticas de DRM, el cifrado y la firma permiten a los proveedores de contenido mantener el control de su contenido independientemente de la amplia distribución de este.

Una directiva DRM sirve como plantilla que el servidor de licencias utiliza cuando genera una licencia. Un cliente también puede hacer referencia a la directiva DRM antes de solicitar una licencia para determinar si el cliente necesita solicitar la autenticación del usuario antes de enviar una solicitud de licencia al servidor.

Puede enviar contenido protegido mediante el Flash Media Server de Adobe o un servidor HTTP. Los usuarios pueden descargar y reproducir contenido protegido en reproductores personalizados creados con el SDK de DRM de Primetime.

Una directiva DRM especifica uno o más derechos que se conceden al cliente. Normalmente, una directiva DRM incluye, como mínimo, el *`Play Right`*. También puede especificar varios derechos de reproducción, cada uno con diferentes restricciones. Cuando el cliente recibe una licencia con varios derechos de reproducción, utiliza la primera licencia que cumple todas las restricciones. Por ejemplo, puede aplicar diferentes configuraciones de protección de salida en diferentes plataformas.

Consulte `CreatePolicyWithOutputProtection.java` en el directorio Herramientas de la línea de comandos de implementación de referencia [!DNL samples] para obtener un código de ejemplo que ilustra este ejemplo.

Puede completar las siguientes tareas con las API de administración de directivas de DRM de Primetime:

* Crear y actualizar directivas
* Ver detalles de la directiva DRM
* Administrar listas de actualización de directivas DRM

Consulte la *Referencia de la API de DRM de Primetime* para obtener más información sobre la API de Java.

Consulte la guía *Using the Primetime DRM Reference Implementations* para obtener información sobre el Administrador de políticas de DRM de Primetime.
