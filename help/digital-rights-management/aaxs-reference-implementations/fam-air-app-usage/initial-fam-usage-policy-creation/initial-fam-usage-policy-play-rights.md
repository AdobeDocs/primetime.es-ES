---
seo-title: Derechos de reproducción
title: Derechos de reproducción
uuid: 90f2a7a6-6637-4d10-9afe-6d2e77fc4185
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Derechos de reproducción {#play-rights}

En la tabla siguiente se describen las preferencias de Derechos de reproducción:

| Preferencia | Descripción |
|--- |--- |
| Ventana de reproducción | La duración de una licencia es válida (en minutos) después de la primera vez que el usuario reproduce el contenido protegido. |
| Protección de salida | Controla si se debe proteger la salida a dispositivos de procesamiento externos. Las salidas analógicas y digitales se pueden especificar de forma independiente. |
| Restricciones | Bloquear lista de versiones de cliente no permitidas para reproducir contenido. Todas las columnas son opcionales. |
| DRM | Especifica una lista de versiones DRM que no pueden reproducir contenido protegido. |
| Tiempo de ejecución | Especifica una lista de versiones en tiempo de ejecución que no pueden reproducir contenido protegido. |
| Nivel mínimo de seguridad |  |
| DRM | Nivel mínimo de seguridad de DRM necesario para reproducir contenido protegido. |
| Tiempo de ejecución | Nivel de seguridad mínimo de tiempo de ejecución necesario para reproducir contenido protegido. |
| Aplicaciones permitidas | Permitir la lista de aplicaciones cliente permitidas para reproducir contenido. Si no se especifican aplicaciones, se permite cualquier aplicación SWF o AIR. |
| SWF | Lista de URL SWF con permiso para reproducir contenido protegido. |
| AIR | Lista de aplicaciones de AIR que permiten reproducir contenido protegido. El ID de editor es obligatorio, los campos restantes son opcionales. |

Flash Access Manager admite directivas que contienen varios derechos de reproducción. Para crear una política con más de una opción Reproducir a la derecha, utilice el botón &quot;Añadir reproducción a la derecha adicional&quot; y rellene los atributos deseados para cada opción Reproducir a la derecha.

Cuando se consume una licencia, el cliente utiliza el primer derecho de reproducción para el que cumple todos los requisitos. Se pueden utilizar varios derechos de reproducción para especificar diferentes restricciones para distintos sistemas operativos. Por ejemplo, es posible especificar un derecho con Output Protection requerido para Windows (mediante la lista de bloques de versiones DRM en Macintosh y Linux) y especificar un segundo derecho con Output Protection &quot;Use if available&quot; en otras plataformas (mediante la lista de bloques de versiones DRM en Windows).
