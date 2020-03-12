---
seo-title: encadenamiento de licencias mejorado
title: encadenamiento de licencias mejorado
uuid: 5e4e825a-de84-4ab2-a652-02cc03153957
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# encadenamiento de licencias mejorado {#enhanced-license-chaining}

Puede utilizar la encadenación de licencias mejorada para actualizar una licencia mediante una licencia raíz principal para la actualización por lotes de licencias.

Primetime DRM 2.0 admite encadenamiento de licencias en el que tanto las licencias de hoja como las de raíz están enlazadas a un equipo específico. Primetime DRM 3.0 y posterior es compatible con la encadenación de licencias mejorada, en la que una hoja está enlazada a una licencia raíz y solo la licencia raíz está enlazada a un equipo o dominio específico. La cadena de licencias mejorada admite la incrustación de una licencia de hoja con el contenido y el cliente solo necesita adquirir la licencia raíz del servidor de licencias para consumir el contenido protegido.

Si desea habilitar la encadenación de licencias mejorada, debe asignar una clave de cifrado raíz a una directiva DRM Primetime. La clave de cifrado raíz se utiliza para enlazar criptográficamente la licencia de hoja a la licencia raíz.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Los clientes Primetime DRM versión 3.0 o posterior admiten la encadenado de licencias mejorada. Si un cliente anterior solicita una licencia para contenido que admita la encadenación de licencias mejorada, el servidor de licencias puede seguir emitiendo una licencia para este cliente mediante la cadena de licencias admitida por Primetime DRM 2.0.

Ejemplo de caso de uso: Utilice esta opción para actualizar las licencias vinculadas descargando una única licencia raíz. Por ejemplo, implemente modelos de suscripción en los que el contenido se pueda reproducir mientras el usuario renueve la suscripción mensualmente. La ventaja de este método es que los usuarios solo tienen que adquirir una licencia única para actualizar todas sus licencias de suscripción.
