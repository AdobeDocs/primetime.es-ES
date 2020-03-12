---
seo-title: Información general
title: Información general
uuid: 7363d241-6947-4a9c-80e5-e50be71066b9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Información general {#overview}

Con Adobe® Access™, los proveedores de contenido pueden aplicar políticas a los archivos multimedia. Mediante las API de administración de políticas, los administradores pueden crear, ver detalles y actualizar políticas.

Una *política* define cómo pueden ver el contenido los usuarios; es una recopilación de información que incluye la configuración de seguridad, los requisitos de autenticación y los derechos de uso. Cuando se aplican las políticas, el cifrado y la firma permiten a los proveedores de contenido mantener el control del contenido, independientemente de la amplia difusión que se distribuya. Los archivos protegidos se pueden entregar mediante Adobe® Flash® Media Server o un servidor HTTP. Se pueden descargar y reproducir en reproductores personalizados creados con Adobe® AIR®, Adobe® Flash® Player y Adobe® Primetime SDK para iOS. La directiva es una plantilla para que el servidor de licencias la utilice cuando genere una licencia. El cliente también puede consultar la directiva antes de solicitar una licencia para determinar si debe solicitar al usuario que se autentique antes de emitir una solicitud de licencia al servidor.

Una directiva especifica uno o más derechos que se conceden al cliente. Normalmente, una política incluye, como mínimo, la opción &quot;Reproducir bien&quot;. También es posible especificar varios derechos de reproducción, cada uno con diferentes restricciones. Cuando el cliente encuentra una licencia con varios derechos de reproducción, utiliza la primera para la que cumple todas las restricciones. Por ejemplo, esta función se puede utilizar para aplicar diferentes ajustes de protección de salida en diferentes plataformas. Para obtener un código de muestra que ilustra este ejemplo, consulte `CreatePolicyWithOutputProtection.java` en el directorio Reference Implementation Command Line Tools &quot;samples&quot; (Ejemplos).

Puede realizar las siguientes tareas mediante las API de administración de directivas:

* Crear y actualizar directivas
* Ver detalles de directivas
* Administrar listas de actualización de directivas

Para obtener más información sobre la API de Java que se describe en este capítulo, consulte Referencia de la API de *Adobe Access*.

Para obtener información sobre la implementación de referencia de Policy Manager, consulte *Uso de las implementaciones* de referencia de Adobe Access.
