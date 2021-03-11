---
title: Lista de bloqueados de los tiempos de ejecución de la aplicación restringidos para acceder a contenido protegido
description: Lista de bloqueados de los tiempos de ejecución de la aplicación restringidos para acceder a contenido protegido
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Lista de bloqueados de tiempos de ejecución de aplicaciones restringidos para acceder a contenido protegido {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

Especifica la versión de Primetime o Flash Runtime que no puede acceder al contenido. Especifique el tiempo de ejecución restringido (Flash Player, AIR o iOS), la plataforma y la versión.

Ejemplo de caso de uso: Al igual que la lista de bloqueados del cliente DRM, la versión más reciente de los tiempos de ejecución de Flash Player, AIR o iOS se puede especificar como la versión mínima necesaria para la adquisición de licencias y la reproducción de contenido.

El tiempo de ejecución de la aplicación se puede identificar mediante cualquiera de los atributos admitidos para las versiones de cliente de DRM, además de los siguientes atributos:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Aplicación | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Coincidencia exacta | Identifica el nombre del tiempo de ejecución de la aplicación. |
