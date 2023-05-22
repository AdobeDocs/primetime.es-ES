---
title: Encadenamiento de licencias mejorado
description: Encadenamiento de licencias mejorado
copied-description: true
exl-id: 5553f055-903f-4140-a425-08f21e8bce87
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Encadenamiento de licencias mejorado {#enhanced-license-chaining}

Permite actualizar una licencia mediante una licencia raíz principal para la actualización por lotes de licencias.

Adobe Access 2.0 admite el encadenamiento de licencias en el que las licencias hoja y raíz están enlazadas a un equipo específico. Adobe Access 3.0 es compatible con el encadenamiento de licencias mejorado, en el que una hoja está enlazada a una licencia raíz y sólo la licencia raíz está enlazada a un equipo o dominio específico. La cadena de licencias mejorada admite la incrustación de una licencia hoja con el contenido y el cliente solo necesita adquirir la licencia raíz del servidor de licencias para consumir el contenido protegido.

Para habilitar el encadenamiento de licencias mejorado, se asigna una clave de cifrado raíz a la directiva. La clave de cifrado raíz se utiliza para enlazar criptográficamente la licencia hoja a la licencia raíz.

>[!NOTE]
>
>La encadenamiento de licencias mejorado es compatible con la versión 3.0 y posteriores de los clientes de Adobe Access. Si un cliente antiguo solicita una licencia para un contenido compatible con el encadenamiento de licencias mejorado, el servidor de licencias aún puede emitir una licencia para este cliente mediante el encadenamiento de licencias compatible con Adobe Access 2.0.

Ejemplo de caso de uso: utilice esta opción para actualizar cualquier licencia vinculada descargando una sola licencia raíz. Por ejemplo, implemente modelos de suscripción en los que el contenido se pueda reproducir siempre y cuando el usuario renueve la suscripción mensualmente. La ventaja de este enfoque es que los usuarios solo tienen que realizar una única adquisición de licencia para actualizar todas las licencias de suscripción.
