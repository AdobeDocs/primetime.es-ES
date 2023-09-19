---
title: Opciones de implementación del servidor de licencias
description: Opciones de implementación del servidor de licencias
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Opciones de implementación del servidor de licencias{#license-server-deployment-options}

Puede implementar el servidor de licencias mediante una de las siguientes opciones:

* Servidor DRM de Adobe Primetime para flujo protegido: Este servidor de licencias está optimizado para flujo continuo. Por ejemplo, puede configurar el servidor para el HTTP Dynamic Streaming de Adobe con Primetime DRM. Este servidor se puede implementar fácilmente con muy poca configuración requerida y admite varios inquilinos. Puede lograr un alto nivel de escalabilidad. Debido a que esta implementación está optimizada para streaming, no admite las funciones completas de DRM de Primetime. Por ejemplo, no se admite la autenticación de nombre de usuario/contraseña, dominios y encadenamiento de licencias. Las reglas de uso en licencias emitidas por este servidor se controlan a través de un archivo de configuración del servidor, que anula la directiva utilizada en el momento del empaquetado.

  Consulte la *Guía del servidor DRM de Adobe Primetime para flujo protegido* para obtener más información sobre las reglas de uso admitidas por el servidor de licencias.
* Servidor de licencias de implementación de referencia: puede utilizar esta configuración para personalizar la implementación del servidor. Este es un ejemplo de implementación del servidor de licencias, incluido el código fuente, que muestra cómo utilizar las API en el SDK de DRM de Primetime para administrar todos los tipos de solicitudes y cómo implementar lógica empresarial personalizada respaldada por una base de datos. Las reglas de uso en licencias emitidas por este servidor se controlan a través de la directiva asociada al contenido en el momento del empaquetado.
* Implementación de servidor personalizada: también puede implementar su propio servidor de licencias con el SDK. La información describe cómo se utilizan las API para implementar un servidor de licencias.
