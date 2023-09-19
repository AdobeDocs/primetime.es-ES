---
description: En esta sección se describen las funciones disponibles con las distintas versiones de Flash Player y TVSDK.
title: Compatibilidad con clientes RBOP
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Compatibilidad con clientes RBOP {#rbop-client-support}

En esta sección se describen las funciones disponibles con las distintas versiones de Flash Player y TVSDK.

**Envío de error** : Las plataformas TVSDK enumeradas a continuación envían un error de tiempo de ejecución de DRM cuando la resolución del contenido que se está reproduciendo supera la resolución permitida para la configuración del dispositivo definida en la directiva DRM:

* Versiones de Flash Player 18 a 20
* Android: Versiones
* iOS: versiones

>[!NOTE]
>
>* Todas las plataformas de Flash y móviles admiten el envío de errores, pero solo los clientes TVSDK enumerados arriba procesan errores relacionados con RBOP.
>* Relacionado con RBOP [Errores del cliente DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
>    * **3371** - Resolución mal formada basada en las restricciones de protección de salida en la licencia.
>    * **3372** : la resolución del contenido es mayor que la resolución máxima especificada en la restricción de protección de salida. (Esto puede ocurrir si alguien intentó insertar contenido destinado a otro dispositivo).
>    * **3373** : la resolución del contenido es mayor que la resolución especificada por la restricción de protección de salida activa actualmente. (Esto significa que tendremos que bajar de categoría).
>

**Descenso automático** - La técnica utilizada para reducir la escala varía según la plataforma y la versión del Flash Player:

* Flash Player versión 21: admite RBOP con escalado descendente automático (conmutación inteligente de velocidad de bits)
* Firefox versión 38 y posterior en Windows (con Access CDM): Adobe reduce automáticamente un flujo de velocidad de bits más alto a uno más bajo (en lugar de descargar un flujo de calidad inferior).

>[!NOTE]
>
>Estas plataformas reducen automáticamente la escala del vídeo y muestran el contenido con una resolución inferior o igual a la especificada en la directiva DRM. Con esta función, el contenido siempre se reproduce en el cliente, siempre y cuando haya un flujo disponible que cumpla las restricciones de la directiva DRM.

**Protección de salida heredada** - Los clientes que utilicen Flashes Player anteriores a la versión 18 solo pueden gestionar restricciones de OP heredadas. Los clientes con Flash Player versión 18 o posterior pueden gestionar restricciones heredadas o RBOP. Si está estableciendo restricciones de RBOP, también debe establecer restricciones de OP heredadas para clientes más antiguos. Para los clientes que admiten RBOP, las restricciones de RBOP superan a las restricciones de OP heredadas.
