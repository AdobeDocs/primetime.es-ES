---
description: Adobe Access se puede utilizar con otras soluciones de transmisión de contenido de terceros para configurar un ecosistema de distribución de medios completo y seguro basado en DRM.
title: Acceso a medios y Adobe UltraViolet
exl-id: cca476a4-1961-46d8-aad4-bc7c996d7b02
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Acceso a medios y Adobe UltraViolet {#ultraviolet-media-and-adobe-access}

Adobe Access se puede utilizar con otras soluciones de transmisión de contenido de terceros para configurar un ecosistema de distribución de medios completo y seguro basado en DRM.

UltraVioleta ( [](https://www.uvvu.com/)) es un sistema de autenticación de derechos digitales y distribución basado en la nube que puede permitir a los consumidores de contenido de entretenimiento doméstico digital transmitir y descargar contenido comprado a través de múltiples plataformas y dispositivos. El contenido ultravioleta se descargará (o transmitirá) en un formato de archivo común (CFF) con cifrado común (CENC).

Es fácil configurar un sistema UltraViolet junto con el acceso al Adobe. El siguiente caso de uso muestra el comportamiento del flujo de contenido:

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. El propietario del contenido codifica y empaqueta el contenido en CFF. El contenido empaquetado se distribuye bajo licencia a un minorista.
1. El minorista carga el contenido en un proveedor de servicios digitales, como CDN. El contenido ya está disponible para descargar. Tenga en cuenta que una o más compañías pueden desempeñar algunos de estos roles.

   El usuario final tiene un dispositivo que es compatible con Adobe AIR. Además, el usuario debe instalar una aplicación compatible con UltraViolet. La aplicación incluye el código necesario para analizar el CFF y presentarlo para que el motor en tiempo de ejecución lo consuma. Todas las operaciones criptográficas confidenciales se gestionan en el tiempo de ejecución seguro.
1. La aplicación puede almacenar en déclencheur una unión de dominio para el dispositivo, que interactúa con el coordinador. El coordinador mantiene un bloqueador de derechos, una base de datos de usuarios y dominios. El administrador de dominios del coordinador se crea mediante el SDK de acceso a Adobe para implementar operaciones de unión o salida de dominio específicas del acceso a Adobe.
1. El usuario puede utilizar la aplicación para seleccionar el vídeo que desea adquirir en el establecimiento. El minorista suele proporcionar un portal web y gestiona toda la lógica empresarial.
1. A continuación, el comerciante interactúa con el coordinador para añadir un token de derechos. A continuación, el minorista redirige la solicitud al proveedor de servicios para la descarga de contenido real.
1. Si el dispositivo aún no tiene una licencia para el contenido, déclencheur una solicitud de licencia utilizando el CFF. La solicitud suele incluir un certificado de dominio, credenciales de usuario e información sobre la aplicación. El proveedor de servicios gestiona un servidor de licencias de acceso a Adobe (desarrollado mediante el SDK de acceso a Adobe) que sigue las especificaciones UltraViolet.
1. La lógica empresarial UltraViolet del proveedor de servicios interactúa con el coordinador según sea necesario para recuperar el token de derechos adecuado para determinar si se debe emitir una licencia de contenido.

   La licencia de contenido está enlazada al dominio. La aplicación cliente puede insertar la licencia en el archivo CFF. Ahora el contenido se puede reproducir en la aplicación, con toda la protección y la aplicación de reglas de uso gestionadas por el componente Acceso a Adobe en tiempo de ejecución.
1. Otros dispositivos y aplicaciones propiedad del mismo usuario final se pueden registrar con el coordinador. El contenido ahora se puede cargar en otros dispositivos de acceso a Adobe sin requerir ninguna transacción externa.
