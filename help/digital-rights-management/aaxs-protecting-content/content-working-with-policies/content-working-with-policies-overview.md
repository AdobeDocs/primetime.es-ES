---
title: Información general
description: Información general
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Información general {#overview}

Con Adobe® Access™, los proveedores de contenido pueden aplicar políticas a los archivos multimedia. Mediante las API de administración de directivas, los administradores pueden crear, ver detalles y actualizar directivas.

Una *directiva* define cómo pueden ver el contenido los usuarios; es una colección de información que incluye configuración de seguridad, requisitos de autenticación y derechos de uso. Cuando se aplican políticas, el cifrado y la firma permiten a los proveedores de contenido mantener el control de su contenido independientemente de la cantidad de distribución. Los archivos protegidos se pueden entregar utilizando Adobe® Flash® Media Server o un servidor HTTP. Pueden descargarse y reproducirse en reproductores personalizados creados con Adobe® AIR®, Adobe® Flash® Player y Adobe® Primetime SDK para iOS. La directiva es una plantilla para que el servidor de licencias la utilice cuando genere una licencia. El cliente también puede consultar la directiva antes de solicitar una licencia para determinar si debe pedir al usuario que se autentique antes de emitir una solicitud de licencia al servidor.

Una directiva especifica uno o más derechos que se conceden al cliente. Normalmente, una política incluye, como mínimo, el &quot;derecho de reproducción&quot;. También es posible especificar varios derechos de reproducción, cada uno con diferentes restricciones. Cuando el cliente encuentra una licencia con varios derechos de reproducción, utiliza la primera para la que cumple todas las restricciones. Por ejemplo, esta función se puede usar para aplicar diferentes configuraciones de protección de salida en diferentes plataformas. Para ver un ejemplo de código que ilustre este ejemplo, consulte `CreatePolicyWithOutputProtection.java` en el directorio &quot;samples&quot; de las herramientas de la línea de comandos de implementación de referencia.

Puede realizar las siguientes tareas utilizando las API de administración de directivas:

* Crear y actualizar directivas
* Ver detalles de directivas
* Administrar listas de actualización de directivas

Para obtener más información sobre la API de Java que se describe en este capítulo, consulte *Referencia de la API de acceso a Adobe*.

Para obtener información sobre la implementación de referencia del Administrador de políticas, consulte *Uso de las implementaciones de referencia de acceso a Adobe*.
