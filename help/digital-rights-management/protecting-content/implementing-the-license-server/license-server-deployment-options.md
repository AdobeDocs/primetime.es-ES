---
seo-title: Opciones de implementación del servidor de licencias
title: Opciones de implementación del servidor de licencias
uuid: 732b948f-8037-423e-9f85-770d6316cbae
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Opciones de implementación del servidor de licencias{#license-server-deployment-options}

Puede implementar el servidor de licencias mediante una de las siguientes opciones:

* Servidor de Adobe Primetime DRM para flujo protegido: este servidor de licencias está optimizado para flujo continuo. Por ejemplo, puede configurar el servidor para el flujo dinámico HTTP de Adobe con Primetime DRM. Este servidor se puede implementar fácilmente con muy poca configuración necesaria y admite varios inquilinos. Puede lograr un alto nivel de escalabilidad. Debido a que esta implementación está optimizada para la transmisión de flujo continuo, no admite las funciones DRM de Primetime completas. Por ejemplo, no se admiten la autenticación de nombre de usuario/contraseña, dominios y encadenamiento de licencias. Las reglas de uso de las licencias emitidas por este servidor se controlan mediante un archivo de configuración de servidor, que anula la directiva utilizada en el empaquetado.

   Consulte la Guía *de flujo protegido de* Adobe Primetime DRM Server para obtener más información sobre las reglas de uso que admite el servidor de licencias.
* Servidor de licencias de implementación de referencia: puede utilizar esta configuración para personalizar la implementación del servidor. Se trata de un ejemplo de implementación de servidor de licencias, incluido el código fuente, que muestra cómo utilizar las API en el SDK de DRM de Primetime para administrar todos los tipos de solicitudes y cómo implementar la lógica empresarial personalizada respaldada por una base de datos. Las reglas de uso de las licencias emitidas por este servidor se controlan mediante la directiva asociada al contenido en el momento del empaquetado.
* Implementación de servidor personalizada: también puede implementar su propio servidor de licencias con el SDK. La información describe cómo se utilizan las API para implementar un servidor de licencias.

