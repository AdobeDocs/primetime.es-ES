---
title: Reglas de uso
description: Reglas de uso
copied-description: true
exl-id: 0f6df09f-47fd-4a05-bcb0-786beaba325a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Reglas de uso{#usage-rules}

Con Adobe Access Server para flujo protegido, todas las reglas de uso se especifican en el servidor a través de archivos de configuración. Se anulan todas las reglas de uso especificadas en el contenido protegido, por lo que se recomienda utilizar una directiva anónima simple durante el empaquetado de contenido. Las reglas de uso que se pueden configurar se pueden establecer por inquilino.

Adobe Access Server para flujo protegido admite las siguientes reglas de uso:

* Protección de salida
* Restricciones de aplicaciones de Adobe® AIR®, SWF, iOS y Android
* Restricciones del módulo DRM y Runtime
* Aplicación de detección de jailbreak (en plataformas de acceso a Adobe que admiten la detección de jailbreak)
* El almacenamiento en caché de licencias está deshabilitado de forma predeterminada. El almacenamiento en caché de licencias se puede habilitar especificando la fecha de finalización del almacenamiento en caché o permitiendo una cantidad de tiempo de almacenamiento en caché (a partir del momento en que se emite la licencia).
* Varios derechos de reproducción, que le permite especificar diferentes combinaciones de protección de salida, restricciones de aplicación y restricciones de DRM/tiempo de ejecución. Por ejemplo, es posible especificar diferentes requisitos de protección de salida para cada plataforma de cliente mediante la restricción del módulo DRM con protección de salida.

>[!NOTE]
>
>Para admitir la entrega de claves remotas a dispositivos iOS, la directiva utilizada al empaquetar debe tener habilitada la entrega de claves remotas. Esta configuración no se puede modificar a través de la configuración del inquilino en el servidor. ***Adobe Primetime es necesario para crear aplicaciones de iOS que puedan reproducir contenido protegido por el acceso a Adobe.***
