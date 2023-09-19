---
title: Información general
description: Información general
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Información general  {#overview}

Con Adobe ® Access™, los proveedores de contenido pueden aplicar directivas a los archivos multimedia. Mediante las API de administración de directivas, los administradores pueden crear, ver detalles y actualizar directivas.

A *directiva* define cómo los usuarios pueden ver el contenido; es una colección de información que incluye configuraciones de seguridad, requisitos de autenticación y derechos de uso. Cuando se aplican directivas, el cifrado y la firma permiten a los proveedores de contenido mantener el control de su contenido, independientemente de la amplitud de su distribución. Los archivos protegidos se pueden entregar mediante el Adobe ® el Flash ® Media Server o un servidor HTTP. Se pueden descargar y reproducir en reproductores personalizados creados con Adobe® AIR®, Adobe ® Flash ® Reproductor y Adobe ® SDK de Primetime para iOS. La directiva es una plantilla que utiliza el servidor de licencias cuando genera una licencia. El cliente también puede consultar la directiva antes de solicitar una licencia para determinar si debe pedir al usuario que se autentique antes de emitir una solicitud de licencia al servidor.

Una directiva especifica uno o varios derechos concedidos al cliente. Normalmente, una política incluye, como mínimo, el &quot;derecho de reproducción&quot;. También es posible especificar varios derechos de reproducción, cada uno con diferentes restricciones. Cuando el cliente encuentra una licencia con varios derechos de reproducción, utiliza la primera para la que cumple todas las restricciones. Por ejemplo, esta función se puede utilizar para aplicar diferentes configuraciones de protección de salida en diferentes plataformas. Para ver el código de ejemplo que ilustra este ejemplo, consulte `CreatePolicyWithOutputProtection.java` en el directorio &quot;samples&quot; de Herramientas de línea de comandos de implementación de referencia.

Puede realizar las siguientes tareas mediante las API de administración de directivas:

* Crear y actualizar directivas
* Ver detalles de la política
* Administrar listas de actualización de directivas

Para obtener más información sobre la API de Java que se analiza en este capítulo, consulte *Referencia de API de acceso de Adobe*.

Para obtener información sobre la implementación de referencia del Administrador de directivas, consulte *Uso de las implementaciones de referencia de acceso a Adobe*.
