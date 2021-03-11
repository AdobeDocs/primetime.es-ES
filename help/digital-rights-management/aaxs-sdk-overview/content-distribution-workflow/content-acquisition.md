---
title: Adquisición de contenido
description: Adquisición de contenido
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# Adquisición de contenido {#content-acquisition}

Cuando un consumidor adquiere un archivo de contenido protegido desde un sitio web o CDN, el consumidor también debe adquirir una licencia que contenga una clave para descifrar el vídeo antes de que se pueda reproducir. Los siguientes pasos ilustran un flujo de trabajo común sobre cómo un equipo que ejecuta un Flash Player o Adobe AIR accede al contenido protegido:

1. El consumidor visita el sitio web del minorista y selecciona un vídeo para verlo. El consumidor intenta descargar o transmitir el vídeo protegido a su equipo mediante un Flash Player o una aplicación de Adobe AIR.

   Si es la primera vez que el consumidor intenta acceder a contenido protegido mediante este equipo específico, el tiempo de ejecución de Flash Player o Adobe AIR primero debe individualizarse como se describe en el paso 2. Si el cliente de tiempo de ejecución ya se ha individualizado, el proceso de adquisición de una licencia se produce como se describe en el paso 3.

1. El cliente en tiempo de ejecución de Flash Player o Adobe AIR adquiere un certificado digital único (denominado *certificado de equipo*) de un servidor alojado en el Adobe.

   Este proceso de asignación de un certificado único se denomina *individualización*. La individualización identifica de forma exclusiva tanto el equipo como el tiempo de ejecución de Flash Player o Adobe AIR que se utiliza para reproducir contenido.

   El proceso de individualización permite que las licencias descargadas se vinculen a un equipo específico en el que está instalado el cliente. Cada equipo recibe una credencial de equipo única (clave privada del equipo y certificado del equipo). Si un cliente específico se viera comprometido, se puede revocar y se le puede impedir adquirir licencias para contenido nuevo.

1. El cliente analiza el contenido protegido a medida que comienza a descargarse o transmitirse al equipo del consumidor y extrae la URL del servidor de licencias del minorista de los metadatos DRM incrustados en el archivo.

   Los metadatos DRM suelen estar separados del contenido, como incrustados en un archivo de manifiesto adjunto o como un blob binario, pero también se pueden incrustar en el archivo de contenido. El cliente se pone en contacto con el servidor de licencias en la dirección URL especificada y adquiere una licencia (como se describe a continuación en el paso 4).
1. El cliente adquiere una licencia del servidor de licencias del minorista.

   Durante la adquisición de licencias, el cliente envía al servidor de licencias del minorista información que identifica el contenido solicitado (los *metadatos DRM*) y el certificado del equipo (que identifica el equipo del consumidor). La solicitud de licencia enviada al servidor se cifra utilizando la clave pública de transporte, que también se incluye en los metadatos de DRM.

   El servidor de licencias (que puede integrarse en la infraestructura de facturación y autenticación del minorista) puede realizar una comprobación de reglas comerciales para comprobar que el usuario está autorizado a ver el contenido solicitado. Si las reglas comerciales lo permiten, el servidor de licencias emite una licencia que contiene la clave de cifrado de contenido para descifrar el contenido y las reglas de uso asociadas con la cuenta de ese usuario. Para procesar una solicitud de licencia, el servidor de licencias descifra la solicitud utilizando su clave privada de transporte. El CEK de los metadatos se descifra mediante la clave privada del servidor de licencias y se vuelve a cifrar para enlazar la licencia al dispositivo que realiza la solicitud. La licencia se firma con la clave privada del servidor de licencias. La respuesta de licencia se firma con la clave privada de transporte y se cifra antes de devolverse al cliente.

   Si la licencia lo permite, el cliente almacena la licencia para habilitar el *acceso sin conexión* a la licencia. El almacenamiento en caché de licencias permite al consumidor ver contenido protegido sin volver a obtener una licencia cada vez que desee ver contenido.

1. Una vez que el cliente de tiempo de ejecución de Flash Player o Adobe AIR tiene una licencia, el cliente extrae el CEK de la licencia y el consumidor puede ver el contenido al que está autorizado a acceder.

   <!--<a id="fig_s43_gc2_44"></a>-->

   ![](assets/FMRMS_fig01_web.png)

   El ejemplo anterior muestra un posible flujo de trabajo. Alternativamente, puede utilizar un flujo de trabajo con una descarga proactiva de contenido en el que la adquisición de licencia se produce mucho más tarde. Otra opción es implementar un flujo de trabajo previo al pedido en el que la adquisición de licencia se produce antes de acceder al contenido.

