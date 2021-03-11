---
title: Lista de bloqueados de los tiempos de ejecución de la aplicación
description: Lista de bloqueados de los tiempos de ejecución de la aplicación
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Lista de bloqueados de los tiempos de ejecución de la aplicación {#blocklist-of-application-runtimes}

La lista de bloqueados de tiempos de ejecución de la aplicación especifica la versión del cliente Primetime o del tiempo de ejecución de Flash que no puede acceder al contenido. Especifique el tiempo de ejecución restringido (Flash Player, AIR o iOS), la plataforma y la versión.

Ejemplo de caso de uso: Al igual que la lista de bloqueados del cliente de DRM de Primetime, la versión más reciente de los tiempos de ejecución de Flash Player, AIR o iOS se puede especificar como la versión mínima necesaria para la adquisición de licencias y la reproducción de contenido.

Puede identificar el tiempo de ejecución de la aplicación mediante cualquiera de los atributos admitidos para las versiones de cliente de DRM de Primetime, además de los siguientes atributos:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Aplicación | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Coincidencia exacta | Identifica el nombre del tiempo de ejecución de la aplicación. |

