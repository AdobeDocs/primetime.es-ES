---
title: Opciones de implementación del servidor de licencias
description: Opciones de implementación del servidor de licencias
copied-description: true
exl-id: c7422a8f-2cd1-4ace-8706-eb3e5a55eac6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Opciones de implementación del servidor de licencias{#license-server-deployment-options}

El servidor de licencias se puede implementar mediante una de las siguientes opciones:

* **Adobe Access Server para flujo protegido** — Este servidor de licencias está optimizado para la transmisión. Por ejemplo, puede configurar el servidor para el HTTP Dynamic Streaming de Adobe con acceso de Adobe. Este servidor se puede implementar fácilmente con muy poca configuración requerida y admitirá varios inquilinos, y puede lograr un alto nivel de escalabilidad. Sin embargo, dado que esta implementación está optimizada para la transmisión, no admite las funciones completas de Acceso al Adobe. Por ejemplo, no se admite la autenticación de nombre de usuario/contraseña, dominios y encadenamiento de licencias. Las reglas de uso en licencias emitidas por este servidor se controlan a través de un archivo de configuración del servidor, que anula la directiva utilizada en el momento del empaquetado. Consulte la *Guía de Adobe Access Server para flujo protegido* para obtener más información sobre las reglas de uso admitidas por este servidor.
* **Servidor de licencias de implementación de referencia** — Utilice esta configuración como punto de partida para una implementación de servidor personalizada. Este es un ejemplo de implementación del servidor de licencias, incluido el código fuente, que muestra cómo utilizar las API en el SDK de acceso a Adobe para controlar todos los tipos de solicitudes y cómo implementar lógica empresarial personalizada respaldada por una base de datos. Las reglas de uso en licencias emitidas por este servidor se controlan a través de la directiva asociada al contenido en el momento del empaquetado.
* **Implementación de servidor personalizada** — También puede implementar su propio servidor de licencias mediante el SDK. La información de este capítulo describe las API utilizadas para implementar un servidor de licencias.
