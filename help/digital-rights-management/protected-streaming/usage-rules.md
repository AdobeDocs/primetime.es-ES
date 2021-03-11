---
description: Con el servidor Adobe Primetime DRM para transmisión protegida, puede especificar todas las reglas de uso en el servidor con archivos de configuración.
title: Acerca de las reglas de uso
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# Acerca de las reglas de uso{#about-usage-rules}

Con el servidor Adobe Primetime DRM para transmisión protegida, puede especificar todas las reglas de uso en el servidor con archivos de configuración.

Se anulará cualquier regla de uso especificada en la directiva DRM para el contenido protegido. Por lo tanto, Adobe recomienda utilizar una política DRM simple y anónima durante el empaquetado de contenido. Cualquier regla de uso que pueda configurar se puede configurar por cada inquilino.

El servidor de Primetime DRM para transmisión protegida es compatible con las siguientes reglas de uso:

* Protección de salida
* Restricciones de aplicaciones de Adobe® AIR®, SWF, iOS y Android
* Restricciones de módulos DRM y Runtime
* Aplicación de detección de saltos de cárcel en plataformas DRM de Primetime que admiten la detección de saltos de cárcel
* El almacenamiento en caché de licencias está deshabilitado de forma predeterminada. El almacenamiento en caché de licencias que puede habilitar especificando la fecha de finalización del almacenamiento en caché o la cantidad de tiempo que se permite el almacenamiento en caché; comienza cuando se emite la licencia.
* Varios derechos de reproducción que permiten especificar diferentes combinaciones de protección de salida, restricciones de aplicación y restricciones de DRM/tiempo de ejecución. Por ejemplo, puede especificar diferentes requisitos de protección de salida para cada plataforma cliente mediante la restricción del módulo DRM con protección de salida.

>[!NOTE]
>
>Si desea admitir la entrega de clave remota a dispositivos iOS, la directiva DRM que se aplica en el momento del empaquetado debe tener habilitada la entrega de claves remotas. Esta configuración no se puede modificar mediante la configuración de inquilino del servidor.

