---
title: Opciones de implementación del servidor de licencias
description: Opciones de implementación del servidor de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Opciones de implementación del servidor de licencias{#license-server-deployment-options}

El servidor de licencias se puede implementar mediante una de las siguientes opciones:

* **Adobe Access Server para transmisión protegida** : este servidor de licencias está optimizado para la transmisión por secuencias. Por ejemplo, puede configurar el servidor para el HTTP Dynamic Streaming de Adobe con acceso a Adobe. Este servidor se puede implementar fácilmente con muy poca configuración requerida y soportará varios inquilinos, y puede lograr un alto nivel de escalabilidad. Sin embargo, dado que esta implementación está optimizada para la transmisión por secuencias, no admite todas las funciones de acceso al Adobe. Por ejemplo, no se admite la autenticación de nombre de usuario/contraseña, dominios y encadenamiento de licencias. Las reglas de uso de las licencias emitidas por este servidor se controlan a través de un archivo de configuración de servidor, que anula la directiva utilizada en el empaquetado. Consulte la *Guía de Adobe Access Server para transmisión protegida* para obtener más información sobre las reglas de uso admitidas por este servidor.
* **Servidor de licencias de implementación de referencia** : utilice esta configuración como punto de partida para una implementación de servidor personalizada. Este es un ejemplo de implementación de servidor de licencias, incluido código fuente, que muestra cómo utilizar las API en el SDK de acceso a Adobe para gestionar todos los tipos de solicitudes y cómo implementar la lógica empresarial personalizada respaldada por una base de datos. Las reglas de uso en las licencias emitidas por este servidor se controlan a través de la directiva asociada con el contenido en el momento del empaquetado.
* **Implementación de servidor personalizada** : también puede implementar su propio servidor de licencias mediante el SDK. La información de este capítulo describe las API utilizadas para implementar un servidor de licencias.

