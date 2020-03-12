---
seo-title: Reglas de uso
title: Reglas de uso
uuid: 361d07b9-e4c8-47ab-8c45-a1de98c9fed7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Reglas de uso{#usage-rules}

Con el servidor de Adobe Access para flujo protegido, todas las reglas de uso se especifican en el servidor a través de archivos de configuración. Se sobrescriben todas las reglas de uso especificadas en el contenido protegido, por lo que se recomienda utilizar una política anónima simple durante el empaquetado de contenido. Las reglas de uso configurables se pueden establecer por usuario.

Adobe Access Server for Protected Streaming admite las siguientes reglas de uso:

* Protección de salida
* Restricciones de aplicaciones de Adobe® AIR®, SWF, iOS y Android
* Restricciones de módulos DRM y Runtime
* Aplicación de detección de saltos de cárcel (en plataformas de Adobe Access que admiten la detección de saltos de cárcel)
* El almacenamiento en caché de licencias está deshabilitado de forma predeterminada. El almacenamiento en caché de licencias se puede habilitar especificando la fecha de finalización del almacenamiento en caché o una cantidad de tiempo que se permite el almacenamiento en caché (comenzando cuando se emite la licencia).
* Varios derechos de reproducción, que permiten especificar diferentes combinaciones de protección de salida, restricciones de aplicación y restricciones de DRM/tiempo de ejecución. Por ejemplo, es posible especificar diferentes requisitos de protección de salida para cada plataforma cliente mediante la Restricción del módulo DRM con protección de salida.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Para admitir la entrega de claves remotas a dispositivos iOS, la directiva utilizada en el momento del empaquetado debe tener habilitada la entrega de claves remotas. Esta configuración no se puede modificar mediante la configuración del inquilino en el servidor. ***Se requiere Adobe Primetime para crear aplicaciones de iOS que puedan reproducir contenido protegido con Adobe Access.***

