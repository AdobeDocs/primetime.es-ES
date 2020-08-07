---
description: Con el servidor DRM de Adobe Primetime para flujo protegido, puede especificar todas las reglas de uso en el servidor con archivos de configuración.
seo-description: Con el servidor DRM de Adobe Primetime para flujo protegido, puede especificar todas las reglas de uso en el servidor con archivos de configuración.
seo-title: Acerca de las reglas de uso
title: Acerca de las reglas de uso
uuid: 4a794712-db58-43f5-b867-8871e58e12ae
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Acerca de las reglas de uso{#about-usage-rules}

Con el servidor DRM de Adobe Primetime para flujo protegido, puede especificar todas las reglas de uso en el servidor con archivos de configuración.

Se sobrescriben todas las reglas de uso especificadas en la directiva DRM para el contenido protegido. Por lo tanto, Adobe recomienda utilizar una política de DRM sencilla y anónima durante el empaquetado de contenido. Cualquier regla de uso que pueda configurar se puede configurar por usuario.

El servidor Primetime DRM para flujo protegido admite las siguientes reglas de uso:

* Protección de salida
* Restricciones de aplicaciones de Adobe® AIR®, SWF, iOS y Android
* Restricciones de módulos DRM y Runtime
* Aplicación de detección de saltos de cárcel en plataformas DRM Primetime que admiten la detección de saltos de cárcel
* El almacenamiento en caché de licencias está deshabilitado de forma predeterminada. El almacenamiento en caché de licencias que se puede habilitar especificando la fecha de finalización del almacenamiento en caché o una cantidad de tiempo que se permite el almacenamiento en caché; inicio cuando se expide la licencia.
* Varios derechos de reproducción que permiten especificar diferentes combinaciones de protección de salida, restricciones de aplicación y restricciones de DRM/tiempo de ejecución. Por ejemplo, puede especificar diferentes requisitos de protección de salida para cada plataforma cliente mediante la Restricción del módulo DRM con protección de salida.

>[!NOTE]
>
>Si desea admitir el envío de claves remotas en dispositivos iOS, la directiva DRM que se aplica en el momento del empaquetado debe tener activado el envío de claves remotas. Esta configuración no se puede modificar mediante la configuración del inquilino en el servidor.

