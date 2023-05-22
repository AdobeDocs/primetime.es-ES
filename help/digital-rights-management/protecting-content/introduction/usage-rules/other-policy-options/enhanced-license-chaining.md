---
title: Encadenamiento de licencias mejorado
description: Encadenamiento de licencias mejorado
copied-description: true
exl-id: 269e7866-fe43-45a8-84d8-c51e4fc95f77
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Encadenamiento de licencias mejorado {#enhanced-license-chaining}

Puede utilizar el encadenamiento de licencias mejorado para actualizar una licencia mediante una licencia raíz principal para la actualización por lotes de licencias.

Primetime DRM 2.0 admite el encadenamiento de licencias, en el que las licencias hoja y raíz están enlazadas a un equipo específico. Primetime DRM 3.0 y versiones posteriores admiten el encadenamiento de licencias mejorado, en el que una hoja está enlazada a una licencia raíz y solo la licencia raíz está enlazada a un equipo o dominio específico. La cadena de licencias mejorada admite la incrustación de una licencia hoja con el contenido y el cliente solo necesita adquirir la licencia raíz del servidor de licencias para consumir el contenido protegido.

Si desea habilitar el encadenamiento de licencias mejorado, debe asignar una clave de cifrado raíz a una directiva DRM de Primetime. La clave de cifrado raíz se utiliza para enlazar criptográficamente la licencia hoja a la licencia raíz.

>[!NOTE]
>
>La versión 3.0 o posterior de los clientes de Primetime DRM admite el encadenamiento mejorado de licencias. Si un cliente más antiguo solicita una licencia para contenido que admita el encadenamiento de licencias mejorado, el servidor de licencias aún puede emitir una licencia para este cliente utilizando el encadenamiento de licencias compatible con Primetime DRM 2.0.

Ejemplo de caso de uso: utilice esta opción para actualizar cualquier licencia vinculada descargando una sola licencia raíz. Por ejemplo, implemente modelos de suscripción en los que el contenido se pueda reproducir siempre y cuando el usuario renueve la suscripción mensualmente. La ventaja de este enfoque es que los usuarios solo tienen que adquirir una única licencia para actualizar todas sus licencias de suscripción.
