---
title: Derechos de reproducción
description: Derechos de reproducción
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Derechos de reproducción {#play-rights}

En la tabla siguiente se describen las preferencias de derechos de reproducción:

| Preferencia | Descripción |
|--- |--- |
| Ventana de reproducción | Duración de la validez de una licencia (en minutos) después de la primera vez que el usuario reproduce el contenido protegido. |
| Protección de salida | Controla si la salida a dispositivos de renderización externos debe estar protegida. Las salidas analógicas y digitales pueden especificarse de forma independiente. |
| Restricciones | Lista de bloqueados de versiones de clientes a las que no se permite reproducir contenido. Todas las columnas son opcionales. |
| DRM | Especifica una lista de versiones de DRM que no tienen permiso para reproducir contenido protegido. |
| Runtime | Especifica una lista de versiones en tiempo de ejecución a las que no se permite reproducir contenido protegido. |
| Nivel mínimo de seguridad |  |
| DRM | Nivel mínimo de seguridad DRM necesario para reproducir contenido protegido. |
| Runtime | Nivel mínimo de seguridad en tiempo de ejecución necesario para reproducir contenido protegido. |
| Aplicaciones permitidas | Lista de permitidos de aplicaciones cliente permitidas para reproducir contenido. Si no se especifican aplicaciones, se permite cualquier SWF o aplicación de AIR. |
| SWF | Lista de direcciones URL de SWF permitidas para reproducir contenido protegido. |
| AIR | Lista de aplicaciones de AIR permitidas para reproducir contenido protegido. El ID de editor es obligatorio, el resto de los campos son opcionales. |

El Administrador de Flashes Access admite directivas que contengan varios derechos de reproducción. Para crear una política con más de un derecho de reproducción, utilice el botón &quot;Añadir derecho de reproducción adicional&quot; y rellene los atributos deseados para cada derecho de reproducción.

Al consumir una licencia, el cliente utiliza el primer derecho de reproducción para el que cumple todos los requisitos. Se pueden usar varios derechos de reproducción para especificar diferentes restricciones para diferentes sistemas operativos. Por ejemplo, es posible especificar un derecho con la protección de salida necesaria para Windows (mediante el bloqueo que enumera las versiones de DRM en Macintosh y Linux) y especificar un segundo derecho con la protección de salida &quot;Usar si está disponible&quot; en otras plataformas (mediante el bloqueo que enumera las versiones de DRM en Windows).
