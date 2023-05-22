---
title: Lista de bloqueados de los tiempos de ejecución de la aplicación restringidos para acceder al contenido protegido
description: Lista de bloqueados de los tiempos de ejecución de la aplicación restringidos para acceder al contenido protegido
copied-description: true
exl-id: 7c9d9e31-1a8d-4c76-9f2c-fcda58de1a42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Lista de bloqueados de los tiempos de ejecución de la aplicación restringidos para acceder al contenido protegido {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

Especifica la versión de Primetime o Flash Runtime que no puede acceder al contenido. Especifique el tiempo de ejecución restringido (Flash Player, AIR o iOS), la plataforma y la versión.

Ejemplo de caso de uso: de forma similar a la lista de bloqueados de cliente DRM, se puede especificar la última versión de los tiempos de ejecución de Flash Player, AIR o iOS como la versión mínima requerida para la adquisición de licencia y la reproducción de contenido.

El tiempo de ejecución de la aplicación se puede identificar mediante cualquiera de los atributos admitidos para las versiones de cliente DRM, además de los atributos siguientes:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Aplicación | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Coincidencia exacta | Identifica el nombre del tiempo de ejecución de la aplicación. |
