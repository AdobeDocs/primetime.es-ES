---
description: En esta sección se describen las funciones disponibles con diferentes versiones de Flash Player y TVSDK.
title: Compatibilidad con clientes RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Soporte de cliente RBOP {#rbop-client-support}

En esta sección se describen las funciones disponibles con diferentes versiones de Flash Player y TVSDK.

**Error Dispatch** : Las plataformas TVSDK enumeradas a continuación envían un error de tiempo de ejecución de DRM cuando la resolución del contenido que se está reproduciendo supera la resolución permitida para la configuración del dispositivo definida en la política de DRM:

* Flash Player de las versiones 18 a 20
* Android: versiones
* iOS: versiones

>[!NOTE]
>
>* Todas las plataformas de Flash y móviles admiten la entrega de errores, aunque solo los clientes de TVSDK enumerados anteriormente procesan los errores relacionados con RBOP.
>* [Errores de cliente de DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages) relacionados con RBOP:
   >    * **3371** - Resolución mal formada basada en restricciones de protección de salida en la licencia.
   >    * **3372** : la resolución del contenido es mayor que la resolución máxima especificada en la restricción de protección de salida. (Esto puede ocurrir si alguien intenta insertar contenido destinado a otro dispositivo).
   >    * **3373**  - La resolución del contenido es mayor que la resolución especificada por la restricción de protección de salida activa actualmente. (Esto significa que tendremos que bajar de categoría).

>



**Desescalado automático** : la técnica utilizada para reducir la escala varía según la plataforma y la versión de Flash Player:

* Flash Player versión 21: Admite RBOP con Desescalado automático (conmutación inteligente de velocidad de bits)
* Firefox versión 38 y posteriores en Windows (con Access CDM): El Adobe descarga automáticamente un flujo de velocidad de bits mayor a uno más bajo (en lugar de descargar un flujo de nivel inferior).

>[!NOTE]
>
>Estas plataformas reducen la escala de vídeo automáticamente y muestran el contenido a una resolución inferior o igual a la especificada por la directiva DRM. Con esta función, el contenido siempre se reproducirá en el cliente, siempre que haya un flujo disponible que cumpla las restricciones de la política de DRM.

**Protección de salida heredada** : los clientes que utilizan Flashes Player anteriores a la versión 18 solo pueden gestionar restricciones de OP heredadas. Los clientes con Flash Player versión 18 y posteriores pueden gestionar restricciones heredadas o RBOP. Si está estableciendo restricciones de RBOP, también debe establecer restricciones de OP heredadas para clientes más antiguos. Para los clientes que admiten RBOP, las restricciones de RBOP prevalecen sobre las restricciones de OP heredadas.
