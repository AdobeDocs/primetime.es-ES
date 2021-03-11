---
description: Adobe Access se puede utilizar con otras soluciones de transmisión de contenido de terceros para configurar un ecosistema de distribución de medios basado en DRM completo y seguro.
title: Acceso a medios y Adobes UltraViolet
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---


# Acceso a medios y Adobes UltraViolet {#ultraviolet-media-and-adobe-access}

Adobe Access se puede utilizar con otras soluciones de transmisión de contenido de terceros para configurar un ecosistema de distribución de medios basado en DRM completo y seguro.

UltraViolet ( [](https://www.uvvu.com/)) es un sistema de autenticación de derechos digitales y distribución basada en la nube que puede permitir a los consumidores de contenido de entretenimiento digital doméstico transmitir y descargar contenido comprado a través de múltiples plataformas y dispositivos. El contenido UltraViolet se descargará (o transmitirá) en un formato de archivo común (CFF) usando un cifrado común (CENC).

Es fácil configurar un sistema UltraViolet junto con el acceso al Adobe. El siguiente caso de uso muestra el comportamiento del flujo de contenido:

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. El propietario del contenido codifica y empaqueta el contenido en CFF. El contenido empaquetado tiene licencia para su distribución a un minorista.
1. El minorista carga el contenido en un proveedor de servicios digitales, como CDN. El contenido ya está disponible para su descarga. Tenga en cuenta que algunas de estas funciones pueden ser desempeñadas por una o más empresas.

   El usuario final tiene un dispositivo compatible con Adobe AIR. Además, el usuario debe instalar una aplicación compatible con UltraViolet. La aplicación incluye el código necesario para analizar la CFF y presentarla para su consumo durante la ejecución. Todas las operaciones criptográficas confidenciales se gestionan en tiempo de ejecución seguro.
1. La aplicación puede almacenar en déclencheur una unión de dominio para el dispositivo, que interactúa con el coordinador. El coordinador mantiene un bloqueador de derechos, una base de datos de usuarios y dominios. El administrador de dominios del coordinador se crea empleando el SDK de acceso a Adobe para implementar operaciones de unión/baja de dominios específicas de acceso a Adobe.
1. El usuario puede utilizar la aplicación para seleccionar un vídeo que desee adquirir en el minorista. Normalmente, el minorista proporciona un portal web y gestiona toda la lógica empresarial.
1. A continuación, el minorista interactúa con el coordinador para añadir un token de derechos. A continuación, el minorista redirige la solicitud al proveedor de servicios para la descarga real de contenido.
1. Si el dispositivo aún no tiene una licencia para el contenido, se déclencheur una solicitud de licencia mediante CFF. La solicitud suele incluir un certificado de dominio, credenciales de usuario e información sobre la aplicación. El proveedor de servicios opera un servidor de licencias de acceso a Adobe (desarrollado con el SDK de acceso a Adobe) que sigue las especificaciones de UltraViolet.
1. La lógica empresarial UltraViolet del proveedor de servicios interactúa con el coordinador según sea necesario para recuperar el token de derechos adecuado para determinar si se debe emitir una licencia de contenido.

   La licencia de contenido está enlazada al dominio . La aplicación cliente puede insertar la licencia en el archivo CFF. El contenido ahora se puede reproducir en la aplicación, con toda la protección y la aplicación de reglas de uso gestionadas por el componente Acceso a Adobe en tiempo de ejecución.
1. Otros dispositivos y aplicaciones propiedad del mismo usuario final pueden registrarse en el coordinador. El contenido ahora se puede cargar en otros dispositivos de acceso a Adobe sin necesidad de realizar ninguna transacción externa.

