---
title: Información general sobre los archivos multimedia de paquetes
description: Información general sobre los archivos multimedia de paquetes
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# Información general {#packaging-media-files-overview}

El empaquetado hace referencia al proceso de codificación y aplicación de una directiva DRM al contenido de vídeo. Puede utilizar las API de paquetes de medios para empaquetar archivos. El SDK de Java de DRM de Primetime solo puede empaquetar contenido de descarga progresiva, como MP4.

>[!NOTE]
>
>Asegúrese de ponerse en contacto con su representante de DRM de Primetime para saber cómo seleccionar la opción de empaquetado más adecuada para su formato de medios y casos de uso.

El empaquetado se desasocia del servidor de licencias. No es necesario que el empaquetador se conecte al servidor de licencias para intercambiar información sobre el contenido. Todo lo que el servidor de licencias necesita saber para emitir una licencia se incluye en los metadatos de contenido.

Cuando se cifra un archivo, su contenido no se puede analizar sin la licencia adecuada. Puede utilizar Primetime DRM para seleccionar las partes del archivo que desea cifrar. Dado que Primetime DRM puede analizar el formato de archivo del contenido de vídeo, puede cifrar de forma inteligente partes selectivas de un archivo en lugar de todo un archivo. Los datos, como los metadatos y los puntos de referencia, pueden permanecer sin cifrar para que los motores de búsqueda puedan seguir buscando en el archivo.

Un fragmento de contenido específico puede tener varias políticas de DRM. Por ejemplo, puede obtener una licencia del contenido de diferentes modelos empresariales sin tener que empaquetar el contenido varias veces. Además, puede permitir el acceso anónimo durante un breve periodo de tiempo y permitir que el cliente compre el contenido para tener acceso ilimitado. Si el contenido se empaqueta mediante varias políticas de DRM, el servidor de licencias debe implementar la lógica para seleccionar qué directiva de DRM se debe utilizar para emitir una licencia.

>[!NOTE]
>
>La arquitectura permite especificar las políticas de DRM de uso y enlazarlas al contenido cuando se empaqueta el contenido. Para que un cliente pueda reproducir contenido, debe adquirir una licencia para un equipo especificado. La licencia especifica las reglas de uso que se aplican y proporciona la clave que debe utilizarse para descifrar contenido. La directiva DRM representa una plantilla para generar una licencia. Sin embargo, el servidor de licencias puede anular las reglas de uso cuando emite una licencia. La licencia puede no ser válida debido a estas restricciones, como tiempos de caducidad o ventanas de reproducción.

Primetime DRM proporciona una API para pasar el CEK. Si no se especifica ningún CEK, el SDK lo genera aleatoriamente. Normalmente necesita un CEK diferente para cada sección de contenido. Sin embargo, en la transmisión dinámica, es probable que utilice el mismo CEK para todos los archivos que componen ese contenido. Por lo tanto, un usuario solo necesita una licencia única para pasar sin problemas de una velocidad de bits a otra. Si desea utilizar la misma clave y licencia para varios fragmentos de contenido, debe pasar el mismo objeto `DRMParameters` a `MediaEncrypter.encryptContent()` o pasar el CEK utilizando `V2KeyParameters.setContentEncryptionKey()`. Si desea utilizar una clave y licencia diferentes para cada sección de contenido, debe crear una nueva instancia `DRMParameters` para cada archivo.

Al empaquetar contenido mediante la rotación de claves, puede controlar las claves de rotación que se utilizan y la frecuencia con la que cambian las claves. `F4VDRMParameters` e  `FLVDRMParameters` implemente la  `KeyRotationParameters` interfaz. A través de esta interfaz, puede habilitar la rotación de claves. También debe especificar un `RotatingContentEncryptionKeyProvider`. Para cada muestra cifrada, esta clase determina la clave de rotación que se utilizará. Puede implementar su propio proveedor o utilizar el `TimeBasedKeyProvider` incluido con el SDK. Esta implementación genera aleatoriamente una nueva clave después de un número específico de segundos.

En algunos casos, es posible que tenga que almacenar los metadatos de contenido como un archivo independiente y ponerlos a disposición del cliente aparte del contenido. En ese caso, es necesario invocar `MediaEncrypter.encryptContent()`, que devuelve un objeto `MediaEncrypterResult`. Llame a `MediaEncrypterResult.getKeyInfo()` y convierta el resultado en `V2KeyStatus`. A continuación, recupere los metadatos de contenido y guárdelos en un archivo.

Todas estas tareas se pueden realizar con la API de Java.

Consulte *Referencia de la API de Adobe Primetime DRM* para obtener más información sobre la API de Java.

Consulte *Uso de las implementaciones de referencia de Adobe Primetime DRM* para obtener información sobre la implementación de referencia de Media Packager.
