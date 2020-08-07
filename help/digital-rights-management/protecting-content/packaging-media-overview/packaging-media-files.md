---
seo-title: Presentación general de archivos multimedia de paquetes
title: Presentación general de archivos multimedia de paquetes
uuid: 9509bcdc-ee4d-4025-9bb6-9b8ac439b926
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# Información general {#packaging-media-files-overview}

El empaquetado se refiere al proceso de codificación y aplicación de una directiva DRM al contenido de vídeo. Puede utilizar las API de empaquetado de medios para empaquetar archivos. El SDK de Java de Primetime DRM solo puede empaquetar contenido de descarga progresiva, como MP4.

>[!NOTE]
>
>Asegúrese de ponerse en contacto con su representante de Primetime DRM para saber cómo seleccionar la opción de empaquetado más adecuada para su formato de medios y casos de uso.

El empaquetado se desenlaza del servidor de licencias. No es necesario que el empaquetador se conecte al servidor de licencias para intercambiar información sobre el contenido. Todo lo que el servidor de licencias necesita saber para emitir una licencia se incluye en los metadatos de contenido.

Cuando se cifra un archivo, su contenido no se puede analizar sin la licencia adecuada. Puede utilizar DRM de Primetime para seleccionar las partes del archivo que desea cifrar. Dado que Primetime DRM puede analizar el formato de archivo del contenido de vídeo, puede cifrar de forma inteligente partes selectivas de un archivo en lugar de todo un archivo. Los datos, como los metadatos y los puntos de referencia, pueden permanecer sin cifrar para que los motores de búsqueda puedan seguir buscando en el archivo.

Un fragmento de contenido especificado puede tener varias directivas DRM. Por ejemplo, puede otorgar licencias de contenido en distintos modelos comerciales sin tener que empaquetar el contenido varias veces. Además, puede permitir el acceso anónimo durante un breve período de tiempo y, a continuación, permitir que el cliente compre el contenido para tener acceso ilimitado. Si el contenido se empaqueta mediante varias directivas DRM, el servidor de licencias debe implementar la lógica para seleccionar qué directiva DRM debe utilizarse para emitir una licencia.

>[!NOTE]
>
>La arquitectura permite especificar las directivas DRM de uso y enlazarlas al contenido cuando se empaqueta el contenido. Para que un cliente pueda reproducir contenido, debe adquirir una licencia para un equipo especificado. La licencia especifica las reglas de uso que se aplican y proporciona la clave que debe utilizarse para descifrar el contenido. La directiva DRM representa una plantilla para generar una licencia. Sin embargo, el servidor de licencias puede anular las reglas de uso cuando emite una licencia. La licencia puede quedar invalidada por estas restricciones, como tiempos de caducidad o ventanas de reproducción.

Primetime DRM proporciona una API para pasar el CEK. Si no se especifica CEK, el SDK lo genera aleatoriamente. Normalmente necesita un CEK diferente para cada sección de contenido. Sin embargo, en Flujo dinámico, es probable que utilice el mismo CEK para todos los archivos que componen ese contenido. Por lo tanto, un usuario solo necesita una licencia para realizar transiciones sin problemas de una velocidad de bits a otra. Si desea utilizar la misma clave y licencia para varios fragmentos de contenido, debe pasar el mismo `DRMParameters` objeto a `MediaEncrypter.encryptContent()`o pasar el CEK usando `V2KeyParameters.setContentEncryptionKey()`. Si desea utilizar una clave y una licencia diferentes para cada sección de contenido, debe crear una nueva `DRMParameters` instancia para cada archivo.

Al empaquetar contenido mediante la rotación de teclas, puede controlar las teclas de rotación que se utilizan y la frecuencia con la que cambian las teclas. `F4VDRMParameters` e `FLVDRMParameters` implemente la `KeyRotationParameters` interfaz. A través de esta interfaz, puede activar la rotación de claves. También debe especificar un `RotatingContentEncryptionKeyProvider`. Para cada muestra cifrada, esta clase determina la tecla de rotación que se va a utilizar. Puede implementar su propio proveedor o utilizar el `TimeBasedKeyProvider` incluido con el SDK. Esta implementación genera aleatoriamente una nueva clave después de un número especificado de segundos.

En algunos casos, es posible que deba almacenar los metadatos de contenido como un archivo independiente y ponerlos a disposición del cliente de forma independiente del contenido. En ese caso, es necesario invocar `MediaEncrypter.encryptContent()`, que devuelve un `MediaEncrypterResult` objeto. Llama `MediaEncrypterResult.getKeyInfo()` y envía el resultado a `V2KeyStatus`. A continuación, recupere los metadatos del contenido y guárdelos en un archivo.

Todas estas tareas se pueden realizar con la API de Java.

Consulte Referencia *de API de DRM de* Adobe Primetime para obtener más información sobre la API de Java.

Consulte *Uso de las implementaciones* de referencia de DRM de Adobe Primetime para obtener información sobre la implementación de referencia de Media Packager.
