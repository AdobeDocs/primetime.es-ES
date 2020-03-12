---
seo-title: Información general sobre el trabajo con directivas DRM
title: Información general sobre el trabajo con directivas DRM
uuid: 32423448-013c-4183-bea8-e14b6690abdb
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Información general {#working-with-drm-policies-overview}

Los proveedores de contenido pueden aplicar políticas de DRM a los archivos de medios mediante el SDK de DRM de Primetime. A continuación, los administradores pueden crear, ver detalles y actualizar políticas de DRM mediante API de administración de políticas.

Una *`DRM policy`* es una colección de información que incluye la configuración de seguridad, los requisitos de autenticación y los derechos de uso. La política define cómo pueden ver el contenido los usuarios. Las políticas de DRM, el cifrado y la firma permiten a los proveedores de contenido mantener el control de su contenido independientemente de la amplia distribución del mismo.

Una directiva DRM sirve como plantilla que el servidor de licencias utiliza cuando genera una licencia. Un cliente también puede hacer referencia a la directiva DRM antes de solicitar una licencia para determinar si el cliente debe solicitar la autenticación al usuario antes de enviar una solicitud de licencia al servidor.

Puede entregar contenido protegido mediante Adobe Flash Media Server o un servidor HTTP. Los usuarios pueden descargar y reproducir contenido protegido en reproductores personalizados creados con el SDK de DRM de Primetime.

Una directiva DRM especifica uno o más derechos que se conceden al cliente. Normalmente, una directiva DRM incluye, como mínimo, el *`Play Right`*. También puede especificar varios derechos de reproducción, cada uno con diferentes restricciones. Cuando el cliente recibe una licencia con varios derechos de reproducción, utiliza la primera licencia que cumple todas las restricciones. Por ejemplo, puede aplicar diferentes ajustes de protección de salida en diferentes plataformas.

Consulte `CreatePolicyWithOutputProtection.java` en el directorio Reference Implementation Command Line Tools (Herramientas de línea de comandos de implementación de referencia) [!DNL samples] para obtener un código de muestra que ilustra este ejemplo.

Puede completar las siguientes tareas con las API de administración de directivas DRM Primetime:

* Crear y actualizar directivas
* Ver detalles de directiva DRM
* Administrar listas de actualización de directivas DRM

Consulte la Referencia *de API de DRM de* Primetime para obtener más información sobre la API de Java.

Consulte la guía *Uso de las implementaciones* de referencia de DRM de Primetime para obtener información sobre el Administrador de directivas de DRM de Primetime.
