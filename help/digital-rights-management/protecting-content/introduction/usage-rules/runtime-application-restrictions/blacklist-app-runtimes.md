---
description: 'null'
seo-description: 'null'
seo-title: Lista negra de los tiempos de ejecución de la aplicación
title: Lista negra de los tiempos de ejecución de la aplicación
uuid: fc3c9bd6-b1e6-4534-b29c-cd9a35b80928
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lista negra de los tiempos de ejecución de la aplicación{#blacklist-of-application-runtimes}

La lista negra de los tiempos de ejecución de la aplicación especifica la versión del cliente Primetime o Flash Runtime que no puede acceder al contenido. Especifique el tiempo de ejecución restringido (Flash Player, AIR o iOS), la plataforma y la versión.

Ejemplo de caso de uso: De forma similar a la lista negra de Primetime DRM Client, se puede especificar la versión más reciente de los tiempos de ejecución de Flash Player, AIR o iOS como la versión mínima necesaria para la adquisición de licencias y la reproducción de contenido.

Puede identificar el tiempo de ejecución de la aplicación mediante cualquiera de los atributos admitidos para las versiones de cliente de DRM de Primetime, además de los atributos siguientes:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Aplicación | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Coincidencia exacta | Identifica el nombre del motor de ejecución de la aplicación. |

