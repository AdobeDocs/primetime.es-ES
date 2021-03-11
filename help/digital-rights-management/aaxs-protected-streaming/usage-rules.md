---
title: Reglas de uso
description: Reglas de uso
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Reglas de uso{#usage-rules}

Con Adobe Access Server para la transmisión protegida, todas las reglas de uso se especifican en el servidor a través de archivos de configuración. Se sobrescriben todas las reglas de uso especificadas en el contenido protegido, por lo que se recomienda utilizar una política anónima simple durante el empaquetado de contenido. Las reglas de uso que se pueden configurar se pueden configurar por cada inquilino.

Adobe Access Server para la transmisión protegida es compatible con las siguientes reglas de uso:

* Protección de salida
* Restricciones de aplicaciones de Adobe® AIR®, SWF, iOS y Android
* Restricciones de módulos DRM y Runtime
* Aplicación de detección de fuga (en plataformas de acceso al Adobe que admiten la detección de fuga)
* El almacenamiento en caché de licencias está deshabilitado de forma predeterminada. Se puede habilitar el almacenamiento en caché de licencias especificando la fecha de finalización del almacenamiento en caché o una cantidad de tiempo que se permite el almacenamiento en caché (a partir de la emisión de la licencia).
* Varios derechos de reproducción, que le permiten especificar diferentes combinaciones de protección de salida, restricciones de aplicación y restricciones de DRM/tiempo de ejecución. Por ejemplo, es posible especificar diferentes requisitos de protección de salida para cada plataforma cliente utilizando la restricción del módulo DRM con protección de salida.

>[!NOTE]
>
>Para admitir la entrega de claves remotas a dispositivos iOS, la directiva utilizada en el momento del empaquetado debe tener habilitada la entrega de claves remotas. Esta configuración no se puede modificar mediante la configuración de inquilino del servidor. ***Adobe Primetime es necesario para crear aplicaciones de iOS que puedan reproducir contenido protegido por Adobe.***

