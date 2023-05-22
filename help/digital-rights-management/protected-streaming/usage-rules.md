---
description: Con Adobe Primetime DRM Server for Protected Streaming, puede especificar todas las reglas de uso del servidor con archivos de configuración.
title: Acerca de las reglas de uso
exl-id: 55af3a18-8fdb-4285-bd9f-ca479475e34f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# Acerca de las reglas de uso{#about-usage-rules}

Con Adobe Primetime DRM Server for Protected Streaming, puede especificar todas las reglas de uso del servidor con archivos de configuración.

Se anularán todas las reglas de uso especificadas en la directiva DRM para el contenido protegido. Por lo tanto, Adobe recomienda utilizar una directiva DRM simple y anónima durante el empaquetado de contenido. Cualquier regla de uso que pueda configurar se puede configurar por inquilino.

El servidor DRM de Primetime para flujo protegido admite las siguientes reglas de uso:

* Protección de salida
* Restricciones de aplicaciones de Adobe® AIR®, SWF, iOS y Android
* Restricciones del módulo DRM y Runtime
* Aplicación de la detección de jailbreak en plataformas DRM de Primetime que admiten la detección de jailbreak
* El almacenamiento en caché de licencias está deshabilitado de forma predeterminada. El almacenamiento en caché de licencias que se puede habilitar especificando la fecha de finalización del almacenamiento en caché o una cantidad de tiempo que se permite; se inicia cuando se emite la licencia.
* Derechos de reproducción múltiple que permiten especificar diferentes combinaciones de Protección de salida, Restricciones de aplicación y Restricciones de DRM/tiempo de ejecución. Por ejemplo, se pueden especificar distintos requisitos de protección de salida para cada plataforma cliente mediante la restricción del módulo DRM con protección de salida.

>[!NOTE]
>
>Si desea admitir la entrega de claves remotas a dispositivos iOS, la directiva DRM aplicada en el momento del empaquetado debe tener activada la entrega de claves remotas. Esta configuración no se puede modificar a través de la configuración del inquilino en el servidor.
