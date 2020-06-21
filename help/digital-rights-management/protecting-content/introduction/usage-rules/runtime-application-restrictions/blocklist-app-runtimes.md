---
description: 'null'
seo-description: 'null'
seo-title: Bloquear lista de tiempos de ejecución de aplicaciones
title: Bloquear lista de tiempos de ejecución de aplicaciones
uuid: fc3c9bd6-b1e6-4534-b29c-cd9a35b80928
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Bloquear lista de tiempos de ejecución de aplicaciones{#blocklist-of-application-runtimes}

La lista de bloques de tiempos de ejecución de la aplicación especifica la versión del cliente Primetime o Flash Runtime que no puede acceder al contenido. Especifique el tiempo de ejecución restringido (Flash Player, AIR o iOS), la plataforma y la versión.

Ejemplo de caso de uso: De forma similar a la lista de bloques del cliente de DRM Primetime, se puede especificar la versión más reciente de los tiempos de ejecución de Flash Player, AIR o iOS como la versión mínima necesaria para la adquisición de licencias y la reproducción de contenido.

Puede identificar el tiempo de ejecución de la aplicación mediante cualquiera de los atributos admitidos para las versiones de cliente de DRM de Primetime, además de los atributos siguientes:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Aplicación | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Coincidencia exacta | Identifica el nombre del motor de ejecución de la aplicación. |

