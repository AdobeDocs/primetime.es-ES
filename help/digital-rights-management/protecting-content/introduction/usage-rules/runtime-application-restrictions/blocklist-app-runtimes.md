---
title: Lista de bloqueados de tiempos de ejecución de aplicaciones
description: Lista de bloqueados de tiempos de ejecución de aplicaciones
copied-description: true
exl-id: f8d1d385-41d4-4361-82c1-417b2ff421c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Lista de bloqueados de tiempos de ejecución de aplicaciones {#blocklist-of-application-runtimes}

La lista de bloqueados de los tiempos de ejecución de la aplicación especifica la versión del cliente de Primetime o del tiempo de ejecución de Flash que no puede acceder al contenido. Especifique el tiempo de ejecución restringido (Flash Player, AIR o iOS), la plataforma y la versión.

Ejemplo de caso de uso: de forma similar a la lista de bloqueados de cliente DRM de Primetime, se puede especificar la última versión de los tiempos de ejecución de Flash Player, AIR o iOS como la versión mínima requerida para la adquisición de licencia y la reproducción de contenido.

Puede identificar el tiempo de ejecución de la aplicación mediante cualquiera de los atributos admitidos para las versiones de cliente DRM de Primetime, además de los atributos siguientes:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Aplicación | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Coincidencia exacta | Identifica el nombre del tiempo de ejecución de la aplicación. |
