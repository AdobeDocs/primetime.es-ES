---
seo-title: Adquisición de contenido
title: Adquisición de contenido
uuid: f3d8b4ef-bc45-4c2d-962b-638512ca0ef3
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Adquisición de contenido {#content-acquisition}

Cuando un consumidor adquiere un archivo de contenido protegido de un sitio web o CDN, también debe adquirir una licencia que contenga una clave para descifrar el vídeo antes de poder reproducirlo. Los siguientes pasos ilustran un flujo de trabajo común para el acceso al contenido protegido por un equipo que ejecuta Flash Player o Adobe AIR:

1. El consumidor visita el sitio web del minorista y selecciona un vídeo para verlo. El consumidor intenta descargar o transmitir el vídeo protegido a su equipo mediante Flash Player o una aplicación de Adobe AIR.

   Si es la primera vez que el consumidor intenta acceder al contenido protegido mediante este equipo específico, el tiempo de ejecución de Flash Player o Adobe AIR debe individualizarse primero como se describe en el paso 2. Si el cliente en tiempo de ejecución ya se ha individualizado, el proceso de adquisición de una licencia se produce como se describe en el paso 3.

1. El cliente en tiempo de ejecución de Flash Player o Adobe AIR adquiere un certificado digital único (denominado certificado *de* equipo) de un servidor alojado por Adobe.

   Este proceso de asignar un certificado único se denomina *individualización*. La individualización identifica de forma exclusiva tanto el equipo como el tiempo de ejecución de Flash Player o Adobe AIR utilizado para reproducir contenido.

   El proceso de individualización permite que las licencias descargadas se enlacen a un equipo específico en el que está instalado el cliente. Cada equipo recibe una credencial de equipo única (clave privada del equipo y certificado del equipo). Si un cliente específico se viera comprometido, se le puede revocar y prohibir la adquisición de licencias para contenido nuevo.

1. El cliente analiza el contenido protegido cuando comienza a descargarse o transmitirse al equipo del consumidor y extrae la dirección URL del servidor de licencias del minorista de los metadatos DRM incrustados en el archivo.

   Los metadatos DRM suelen estar separados del contenido, como incrustados en un archivo de manifiesto adjunto o como un blob binario, pero también pueden incrustarse en el archivo de contenido. El cliente se pone en contacto con el servidor de licencias en la dirección URL especificada y adquiere una licencia (como se describe a continuación en el paso 4).
1. El cliente adquiere una licencia del servidor de licencias del minorista.

   Durante la adquisición de la licencia, el cliente envía al servidor de licencias del minorista información que identifica el contenido solicitado (los metadatos *de* DRM) y el certificado del equipo (que identifica el equipo del consumidor). La solicitud de licencia enviada al servidor se cifra mediante la clave pública de transporte, que también se incluye en los metadatos de DRM.

   El servidor de licencias — que puedan integrarse en la infraestructura de facturación y autenticación del minorista — Puede realizar una comprobación de reglas comerciales para comprobar que el usuario está autorizado a ver el contenido solicitado. Si las reglas comerciales lo permiten, el servidor de licencias emite una licencia que contiene la clave de cifrado de contenido para descifrar el contenido y las reglas de uso asociadas con la cuenta de ese usuario. Para procesar una solicitud de licencia, el servidor de licencias descifra la solicitud utilizando su clave privada de transporte. El CEK de los metadatos se descifra mediante la clave privada del servidor de licencias y se vuelve a cifrar para enlazar la licencia al dispositivo que realiza la solicitud. La licencia se firma con la clave privada del servidor de licencias. La respuesta de licencia se firma con la clave privada Transporte y se cifra antes de devolverse al cliente.

   Si la licencia lo permite, el cliente almacena la licencia para habilitar el acceso ** sin conexión a la licencia. El almacenamiento en caché de licencias permite al consumidor ver el contenido protegido sin tener que volver a adquirir una licencia cada vez que desee ver el contenido.

1. Una vez que el cliente en tiempo de ejecución de Flash Player o Adobe AIR tiene una licencia, el cliente extrae el CEK de la licencia y el consumidor puede ver el contenido al que está autorizado a acceder.

   <!--<a id="fig_s43_gc2_44"></a>-->

   ![](assets/FMRMS_fig01_web.png)

   El ejemplo anterior muestra un flujo de trabajo posible. También puede utilizar un flujo de trabajo con una descarga proactiva de contenido en el que la adquisición de licencias se produce mucho más tarde. Otra opción es implementar un flujo de trabajo previo al pedido en el que la adquisición de licencias tiene lugar antes de acceder al contenido.

