---
description: 'null'
seo-description: 'null'
seo-title: Lista de bloqueados de los tiempos de ejecución de la aplicación
title: Lista de bloqueados de los tiempos de ejecución de la aplicación
uuid: fc3c9bd6-b1e6-4534-b29c-cd9a35b80928
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Lista de bloqueados de los tiempos de ejecución de la aplicación {#blocklist-of-application-runtimes}

La lista de bloqueados de los tiempos de ejecución de la aplicación especifica la versión del cliente Primetime o Flash Runtime que no puede acceder al contenido. Especifique el tiempo de ejecución restringido (Flash Player, AIR o iOS), la plataforma y la versión.

Ejemplo de caso de uso: De forma similar a la lista de bloqueados del cliente Primetime DRM, se puede especificar la versión más reciente de los tiempos de ejecución de Flash Player, AIR o iOS como la versión mínima necesaria para la adquisición de licencias y la reproducción de contenido.

Puede identificar el tiempo de ejecución de la aplicación mediante cualquiera de los atributos admitidos para las versiones de cliente de DRM de Primetime, además de los atributos siguientes:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Aplicación | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Coincidencia exacta | Identifica el nombre del motor de ejecución de la aplicación. |

