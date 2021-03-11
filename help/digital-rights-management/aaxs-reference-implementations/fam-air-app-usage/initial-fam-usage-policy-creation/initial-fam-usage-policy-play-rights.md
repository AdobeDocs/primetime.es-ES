---
title: Derechos de reproducción
description: Derechos de reproducción
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Derechos de reproducción {#play-rights}

En la tabla siguiente se describen las preferencias de derechos de reproducción:

| Preferencia | Descripción |
|--- |--- |
| Ventana de reproducción | La duración de una licencia es válida (en minutos) después de la primera vez que el usuario reproduce el contenido protegido. |
| Protección de salida | Controla si se debe proteger la salida a dispositivos de renderización externos. Las salidas analógicas y digitales se pueden especificar de forma independiente. |
| Restricciones | Lista de bloqueados de versiones de cliente no permitidas para reproducir contenido. Todas las columnas son opcionales. |
| DRM | Especifica una lista de versiones de DRM que no pueden reproducir contenido protegido. |
| Tiempo de ejecución | Especifica una lista de versiones de tiempo de ejecución que no pueden reproducir contenido protegido. |
| Nivel mínimo de seguridad |  |
| DRM | Nivel mínimo de seguridad de DRM necesario para reproducir contenido protegido. |
| Tiempo de ejecución | Nivel mínimo de seguridad en tiempo de ejecución necesario para reproducir contenido protegido. |
| Aplicaciones permitidas | Lista de permitidos de aplicaciones cliente permitidas para reproducir contenido. Si no se especifican las aplicaciones, se permite cualquier aplicación SWF o AIR. |
| SWF | Lista de URL SWF permitidas para reproducir contenido protegido. |
| AIRE | Lista de aplicaciones de AIR permitidas para reproducir contenido protegido. El ID del editor es obligatorio, los campos restantes son opcionales. |

El Administrador de Flashes Access admite directivas que contienen varios derechos de reproducción. Para crear una política con más de un derecho de reproducción, utilice el botón &quot;Agregar derecho de reproducción adicional&quot; y rellene los atributos deseados para cada derecho de reproducción.

Al consumir una licencia, el cliente utiliza el primer derecho de reproducción para el que cumple todos los requisitos. Se pueden usar derechos de reproducción múltiple para especificar diferentes restricciones para distintos sistemas operativos. Por ejemplo, es posible especificar un derecho con Output Protection requerido para Windows (mediante la lista de bloqueados de versiones DRM en Macintosh y Linux) y especificar un segundo derecho con Output Protection &quot;Use if available&quot; en otras plataformas (mediante la lista de bloqueados de versiones DRM en Windows).
