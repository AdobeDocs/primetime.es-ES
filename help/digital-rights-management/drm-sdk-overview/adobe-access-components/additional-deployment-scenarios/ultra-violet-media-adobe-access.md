---
seo-title: Medios UltraViolet y Adobe Primetime DRM
title: Medios UltraViolet y Adobe Primetime DRM
uuid: 7076c0f9-e092-48e4-9118-8a414bd03c7a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Medios UltraViolet y Adobe Primetime DRM {#ultraviolet-media-and-adobe-primetime-drm}

Adobe Primetime DRM puede utilizarse con otras soluciones de flujo de contenido de terceros para configurar un ecosistema de distribución de medios completo y seguro basado en DRM.

UltraViolet ( [https://www.myuv.com/](https://www.uvvu.com/)) es un sistema de autenticación de derechos digitales y distribución basada en la nube que permite a los consumidores de contenido de entretenimiento doméstico digital transmitir y descargar contenido adquirido a través de múltiples plataformas y dispositivos. El contenido UltraViolet se descargará (o transmitirá) en un formato de archivo común (CFF) usando el cifrado común (CENC).

Es fácil configurar un sistema UltraViolet junto con Adobe Primetime DRM. El siguiente caso de uso describe el comportamiento del flujo de contenido:

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. El propietario del contenido codifica y empaqueta el contenido en CFF. El contenido empaquetado tiene una licencia otorgada a un minorista para su distribución.
1. El minorista carga el contenido en un proveedor de servicios digitales, como CDN. El contenido ya está disponible para su descarga. Tenga en cuenta que algunas de estas funciones pueden ser desempeñadas por una o varias empresas.

   El usuario final tiene un dispositivo compatible con Adobe AIR. Además, el usuario necesita instalar una aplicación compatible con UltraViolet. La aplicación incluye el código necesario para analizar el CFF y presentarlo para su consumo durante el tiempo de ejecución. Todas las operaciones criptográficas sensibles se gestionan en tiempo de ejecución seguro.
1. La aplicación puede activar una unión de dominio para el dispositivo, que interactúa con el coordinador. El coordinador mantiene un bloqueador de derechos, una base de datos de usuarios y dominios. El administrador de dominios del coordinador se crea mediante el SDK de DRM de Primetime para implementar las operaciones de unión/abandono de dominio específicas de Primetime DRM.
1. A continuación, el usuario puede utilizar la aplicación para seleccionar un vídeo que desee adquirir del minorista. El minorista normalmente proporciona un portal web y gestiona toda la lógica comercial.
1. A continuación, el minorista interactúa con el coordinador para agregar un token de derechos. A continuación, el minorista redirige la solicitud al proveedor de servicios para la descarga de contenido real.
1. Si el dispositivo aún no tiene una licencia para el contenido, activa una solicitud de licencia mediante el CFF. La solicitud suele incluir un certificado de dominio, credenciales de usuario e información sobre la aplicación. El proveedor de servicios opera un servidor de licencias DRM Primetime (desarrollado con el SDK de DRM Primetime) que sigue las especificaciones de UltraViolet.
1. La lógica empresarial UltraViolet del proveedor de servicios interactúa con el coordinador según sea necesario para recuperar el token de derechos adecuado para determinar si se debe emitir una licencia de contenido.

   La licencia de contenido está enlazada al dominio. La aplicación cliente puede insertar la licencia en el archivo CFF. Ahora, el contenido se puede reproducir en la aplicación, con toda la aplicación de reglas de uso y protección gestionada por el componente DRM Primetime en tiempo de ejecución.
1. Otros dispositivos y aplicaciones propiedad del mismo usuario final pueden registrarse en el coordinador. El contenido ahora se puede cargar en otros dispositivos DRM Primetime sin necesidad de realizar ninguna transacción externa.