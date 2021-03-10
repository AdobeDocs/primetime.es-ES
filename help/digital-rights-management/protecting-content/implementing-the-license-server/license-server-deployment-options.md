---
title: Opciones de implementación del servidor de licencias
description: Opciones de implementación del servidor de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Opciones de implementación del servidor de licencias{#license-server-deployment-options}

Puede implementar el servidor de licencias utilizando una de las siguientes opciones:

* Servidor DRM de Adobe Primetime para transmisión protegida: este servidor de licencias está optimizado para transmisión por secuencias. Por ejemplo, puede configurar el servidor para el HTTP Dynamic Streaming de Adobe con Primetime DRM. Este servidor se puede implementar fácilmente con muy poca configuración requerida y soporta varios inquilinos. Puede lograr un alto nivel de escalabilidad. Como esta implementación está optimizada para la transmisión por secuencias, no admite las funciones DRM de Primetime completas. Por ejemplo, no se admite la autenticación de nombre de usuario/contraseña, dominios y encadenamiento de licencias. Las reglas de uso de las licencias emitidas por este servidor se controlan a través de un archivo de configuración de servidor, que anula la directiva utilizada en el empaquetado.

   Consulte la *Guía de Adobe Primetime DRM Server para flujos protegidos* para obtener más información sobre las reglas de uso compatibles con el servidor de licencias.
* Servidor de licencias de implementación de referencia: puede utilizar esta configuración para personalizar la implementación del servidor. Este es un ejemplo de implementación de servidor de licencias, incluido el código fuente, que muestra cómo utilizar las API en el SDK de DRM de Primetime para administrar todos los tipos de solicitudes y cómo implementar la lógica empresarial personalizada respaldada por una base de datos. Las reglas de uso en las licencias emitidas por este servidor se controlan a través de la directiva asociada con el contenido en el momento del empaquetado.
* Implementación de servidor personalizada: también puede implementar su propio servidor de licencias con el SDK. La información describe cómo se utilizan las API para implementar un servidor de licencias.

