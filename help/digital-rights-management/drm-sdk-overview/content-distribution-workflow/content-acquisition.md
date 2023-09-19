---
description: Cuando un consumidor adquiere un archivo de contenido protegido de un sitio web o CDN, también debe adquirir una licencia que contenga una clave para descifrar el vídeo antes de poder reproducirlo. Los siguientes pasos ilustran un flujo de trabajo común sobre cómo un equipo que ejecuta Flash Player o Adobe AIR accede al contenido protegido
title: Adquisición de contenido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Adquisición de contenido{#content-acquisition}

Cuando un consumidor adquiere un archivo de contenido protegido de un sitio web o CDN, también debe adquirir una licencia que contenga una clave para descifrar el vídeo antes de poder reproducirlo. Los siguientes pasos ilustran un flujo de trabajo común sobre cómo un equipo que ejecuta Flash Player o Adobe AIR accede al contenido protegido:

1. El consumidor visita el sitio web del minorista y selecciona el vídeo que desea ver. El consumidor intenta descargar o transmitir el vídeo protegido a su equipo mediante un Flash Player o una aplicación de Adobe AIR.

   Si es la primera vez que el consumidor intenta acceder al contenido protegido mediante este equipo específico, el tiempo de ejecución de Flash Player o Adobe AIR debe individualizarse primero como se describe en el paso 2. Si el cliente de tiempo de ejecución ya se ha individualizado, el proceso de adquisición de una licencia se produce tal como se describe en el paso 3.

1. El cliente de tiempo de ejecución de Flash Player o Adobe AIR adquiere un certificado digital único (denominado *certificado automático*) desde un servidor alojado en el Adobe.

   Se llama a este proceso de asignación de un certificado único *individualización*. La individualización identifica de forma exclusiva el equipo y el tiempo de ejecución de Flash Player o Adobe AIR utilizados para reproducir contenido.

   El proceso de individualización permite enlazar las licencias descargadas a un equipo específico en el que está instalado el cliente. Cada equipo recibe una credencial de equipo única (clave privada del equipo y certificado del equipo). Si un cliente específico se viera comprometido, se le puede revocar y prohibir la adquisición de licencias para nuevo contenido.

1. El cliente analiza el contenido protegido a medida que comienza a descargarse o transmitirse al equipo del consumidor y extrae la URL del servidor de licencias del comerciante de los metadatos DRM de Primetime incrustados en el archivo.

   Los metadatos DRM de Primetime suelen ser independientes del contenido, como están incrustados en un archivo de manifiesto complementario o como un blob binario, pero también se pueden incrustar en el archivo de contenido. El cliente se pone en contacto con el servidor de licencias en la dirección URL especificada y adquiere una licencia (como se describe en el paso 4).
1. El cliente adquiere una licencia del servidor de licencias del minorista.

   Durante la adquisición de la licencia, el cliente envía información que identifica el contenido solicitado (la *Metadatos de DRM de Primetime*) y el certificado del equipo (que identifica el equipo del consumidor) al servidor de licencias del comerciante. La solicitud de licencia enviada al servidor se cifra mediante la clave pública Transport, que también se incluye en los metadatos DRM de Primetime.

   El servidor de licencias (que puede integrarse en la infraestructura de facturación y autenticación del minorista) puede realizar una comprobación de reglas empresariales para comprobar que el usuario está autorizado a ver el contenido solicitado. Si las reglas empresariales lo permiten, el servidor de licencias emite una licencia que contiene la clave de cifrado de contenido para descifrar el contenido y las reglas de uso asociadas con la cuenta de ese usuario. Para procesar una solicitud de licencia, el servidor de licencias descifra la solicitud utilizando su clave privada de transporte. El CEK de los metadatos se descifra mediante la clave privada del servidor de licencias y se vuelve a cifrar para enlazar la licencia al dispositivo que realiza la solicitud. La licencia se firma con la clave privada del servidor de licencias. La respuesta de licencia se firma con la clave privada Transport y se cifra antes de devolverse al cliente.

   Si la licencia lo permite, el cliente almacena la licencia para habilitar *acceso sin conexión* a la licencia. El almacenamiento en caché de licencias permite al consumidor ver contenido protegido sin volver a adquirir una licencia cada vez que desee ver contenido.

1. Una vez que el cliente de tiempo de ejecución de Flash Player o Adobe AIR tiene una licencia, el cliente extrae la CEK de la licencia y el consumidor puede ver el contenido al que tiene autorización para acceder.

   <!--<a id="fig_s43_gc2_44"></a>-->

   ![](assets/FMRMS_fig01_web.png)

   El ejemplo anterior muestra solo un posible flujo de trabajo. También puede utilizar un flujo de trabajo con una descarga proactiva de contenido donde la adquisición de licencia se produzca mucho más tarde. Otra opción es implementar un flujo de trabajo de solicitud previa en el que la adquisición de licencia se produce antes de acceder al contenido.
