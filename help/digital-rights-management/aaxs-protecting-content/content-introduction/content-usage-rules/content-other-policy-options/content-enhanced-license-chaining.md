---
title: encadenamiento de licencias mejorado
description: encadenamiento de licencias mejorado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# encadenado de licencias mejorado {#enhanced-license-chaining}

Permite actualizar una licencia utilizando una licencia raíz principal para la actualización por lotes de licencias.

Adobe Access 2.0 admite la encadenación de licencias en la que tanto las licencias de hoja como las de raíz están vinculadas a un equipo específico. Adobe Access 3.0 es compatible con la encadenación de licencias mejorada, en la que una hoja está enlazada a una licencia raíz, y solo la licencia raíz está enlazada a un equipo o dominio específico. La cadena de licencias mejorada admite la incrustación de licencias de hoja con el contenido y el cliente solo necesita adquirir la licencia raíz del servidor de licencias para consumir el contenido protegido.

Para habilitar la cadena de licencia mejorada, se asigna una clave de cifrado raíz a la directiva. La clave de cifrado raíz se utiliza para enlazar criptográficamente la licencia de hoja a la licencia raíz.

>[!NOTE]
>
>La encadenación de licencias mejorada es compatible con los clientes de acceso a Adobe versión 3.0 y posteriores. Si un cliente anterior solicita una licencia para contenido que admita la encadenación de licencias mejorada, el servidor de licencias aún puede emitir una licencia a este cliente mediante la encadenación de licencias admitida por Adobe Access 2.0.

Ejemplo de caso de uso: Utilice esta opción para actualizar las licencias vinculadas descargando una licencia raíz única. Por ejemplo, implemente modelos de suscripción en los que el contenido se pueda reproducir mientras el usuario renueve la suscripción mensualmente. La ventaja de este enfoque es que los usuarios solo tienen que realizar una adquisición de licencia única para actualizar todas sus licencias de suscripción.
