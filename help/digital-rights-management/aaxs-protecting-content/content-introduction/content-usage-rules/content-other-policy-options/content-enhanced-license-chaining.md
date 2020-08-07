---
seo-title: encadenamiento de licencias mejorado
title: encadenamiento de licencias mejorado
uuid: d11b0631-5dfb-42b8-b7ba-cfeb1da488be
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# encadenamiento de licencias mejorado {#enhanced-license-chaining}

Permite actualizar una licencia mediante una licencia raíz principal para la actualización por lotes de licencias.

Adobe Access 2.0 admite la formación de licencias en la que tanto las licencias de hoja como las de raíz están enlazadas a un equipo específico. Adobe Access 3.0 es compatible con la cadena de licencias mejorada, en la que una hoja está enlazada a una licencia raíz y solo la licencia raíz está enlazada a un equipo o dominio específico. La cadena de licencias mejorada admite la incrustación de licencias de hoja con el contenido y el cliente solo necesita adquirir la licencia raíz del servidor de licencias para consumir el contenido protegido.

Para habilitar la cadena de licencia mejorada, se asigna una clave de cifrado raíz a la directiva. La clave de cifrado raíz se utiliza para enlazar criptográficamente la licencia de hoja a la licencia raíz.

>[!NOTE]
>
>La cadena de licencias mejorada es compatible con los clientes de Adobe Access versión 3.0 y posterior. Si un cliente más antiguo solicita una licencia para contenido que admita la cadena de licencias mejorada, el servidor de licencias puede seguir emitiendo una licencia para este cliente mediante la cadena de licencias admitida por Adobe Access 2.0.

Ejemplo de caso de uso: Utilice esta opción para actualizar las licencias vinculadas descargando una única licencia raíz. Por ejemplo, implemente modelos de suscripción en los que el contenido se pueda reproducir mientras el usuario renueve la suscripción mensualmente. La ventaja de este enfoque es que los usuarios solo tienen que realizar una adquisición de licencia única para actualizar todas sus licencias de suscripción.
