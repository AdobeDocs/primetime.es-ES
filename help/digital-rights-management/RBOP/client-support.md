---
description: En esta sección se describen las funciones disponibles con diferentes versiones de Flash Player y TVSDK.
seo-description: En esta sección se describen las funciones disponibles con diferentes versiones de Flash Player y TVSDK.
seo-title: Compatibilidad con el cliente RBOP
title: Compatibilidad con el cliente RBOP
uuid: d1d0f788-7bc1-488c-807e-be47f83725e9
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Compatibilidad con el cliente RBOP {#rbop-client-support}

En esta sección se describen las funciones disponibles con diferentes versiones de Flash Player y TVSDK.

**Envío** de errores: las plataformas TVSDK que se indican a continuación distribuyen un error de tiempo de ejecución de DRM cuando la resolución del contenido que se está reproduciendo supera la resolución permitida para la configuración del dispositivo definida en la directiva DRM:

* Versiones de Flash Player 18 a 20
* Android: versiones
* iOS: versiones

>[!NOTE]
>
>* Todas las plataformas Flash y móviles admiten el Envío de errores, aunque solo los clientes TVSDK enumerados anteriormente procesan errores relacionados con RBOP.
>* Errores [de cliente](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM relacionados con RBOP: >
   >    * **3371** - Resolución incorrecta basada en las limitaciones de protección de la producción de la licencia.
   >    * **3372** : la resolución del contenido es mayor que la resolución máxima especificada en la restricción de protección de resultados. (Esto puede ocurrir si alguien ha intentado inyectar contenido destinado a otro dispositivo).
   >    * **3373** : la resolución del contenido es mayor que la resolución especificada por la restricción de protección de salida activa. (Esto significa que tendremos que reducir la calificación).
>



**Desescalado** automático: la técnica utilizada para reducir la escala varía según la plataforma y la versión de Flash Player:

* Flash Player versión 21: Admite RBOP con Desescalado automático (conmutación inteligente de velocidad de bits)
* Firefox versión 38 y posterior en Windows (con Access CDM): Adobe reduce automáticamente un flujo de velocidad de bits más alto a uno más bajo (en lugar de descargar un flujo de menor calidad).

>[!NOTE]
>
>Estas plataformas reducen automáticamente la escala del vídeo y muestran el contenido con una resolución inferior o igual a la especificada por la directiva DRM. Con esta función, el contenido siempre se reproducirá en el cliente, siempre que haya una secuencia disponible que cumpla las restricciones de la directiva DRM.

**Protección** de salida heredada: los clientes que utilizan reproductores Flash antes de la versión 18 solo pueden gestionar restricciones de OP heredadas. Los clientes con Flash Player versión 18 y posterior pueden gestionar restricciones heredadas o RBOP. Si está estableciendo restricciones de RBOP, también debe establecer restricciones de OP heredadas para clientes más antiguos. Para los clientes que admiten RBOP, las restricciones de RBOP superan a las restricciones de OP heredadas.
