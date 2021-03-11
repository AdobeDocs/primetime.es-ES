---
title: encadenamiento de licencias mejorado
description: encadenamiento de licencias mejorado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# encadenado de licencias mejorado {#enhanced-license-chaining}

Puede utilizar la encadenación de licencias mejorada para actualizar una licencia utilizando una licencia raíz principal para la actualización por lotes de licencias.

Primetime DRM 2.0 admite la encadenación de licencias en la que tanto las licencias de hoja como las de raíz están vinculadas a un equipo específico. Primetime DRM 3.0 y posteriores son compatibles con la encadenación de licencias mejorada, en la que una hoja está enlazada a una licencia raíz, y solo la licencia raíz está enlazada a un equipo o dominio específico. La cadena de licencias mejorada admite la incrustación de una licencia de hoja con el contenido, y el cliente solo necesita adquirir la licencia raíz del servidor de licencias para consumir el contenido protegido.

Si desea habilitar la encadenación de licencias mejorada, debe asignar una clave de cifrado raíz a una directiva de DRM de Primetime. La clave de cifrado raíz se utiliza para enlazar criptográficamente la licencia de hoja a la licencia raíz.

>[!NOTE]
>
>La encadenación de licencias mejorada es compatible con los clientes de Primetime DRM versión 3.0 o posterior. Si un cliente anterior solicita una licencia para contenido que admita la encadenación de licencias mejorada, el servidor de licencias aún puede emitir una licencia a este cliente utilizando la encadenación de licencias admitida por Primetime DRM 2.0.

Ejemplo de caso de uso: Utilice esta opción para actualizar las licencias vinculadas descargando una licencia raíz única. Por ejemplo, implemente modelos de suscripción en los que el contenido se pueda reproducir mientras el usuario renueve la suscripción mensualmente. La ventaja de este enfoque es que los usuarios solo tienen que adquirir una licencia única para actualizar todas sus licencias de suscripción.
