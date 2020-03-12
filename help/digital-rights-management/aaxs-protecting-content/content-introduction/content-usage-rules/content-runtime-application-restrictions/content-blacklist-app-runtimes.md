---
seo-title: Lista negra de los tiempos de ejecución de la aplicación restringidos para acceder al contenido protegido
title: Lista negra de los tiempos de ejecución de la aplicación restringidos para acceder al contenido protegido
uuid: 462a2c09-b335-4768-bd0e-1359db169d69
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lista negra de los tiempos de ejecución de la aplicación restringidos para acceder al contenido protegido {#blacklist-of-application-runtimes-restricted-from-accessing-protected-content}

Especifica la versión de Primetime o Flash Runtime que no puede acceder al contenido. Especifique el tiempo de ejecución restringido (Flash Player, AIR o iOS), la plataforma y la versión.

Ejemplo de caso de uso: De forma similar a la lista negra del cliente DRM, se puede especificar la versión más reciente de los tiempos de ejecución de Flash Player, AIR o iOS como la versión mínima necesaria para la adquisición de licencias y la reproducción de contenido.

El tiempo de ejecución de la aplicación se puede identificar mediante cualquiera de los atributos admitidos para las versiones de cliente DRM, además de los atributos siguientes:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Aplicación | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Coincidencia exacta | Identifica el nombre del motor de ejecución de la aplicación. |

