---
title: Información general sobre empaquetado de archivos multimedia
description: Información general sobre empaquetado de archivos multimedia
copied-description: true
exl-id: 88c593a7-33b5-4773-b283-2ab16f9e8c3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# Información general {#packaging-media-files-overview}

El empaquetado hace referencia al proceso de cifrar y aplicar una directiva DRM al contenido de vídeo. Puede utilizar las API de empaquetado de medios para empaquetar archivos. El SDK de Java de Primetime DRM solo puede empaquetar contenido de descarga progresiva, como MP4.

>[!NOTE]
>
>Asegúrese de ponerse en contacto con su representante de DRM de Primetime para seleccionar la opción de empaquetado más adecuada para su formato de medios y casos de uso.

El paquete se desacopla del servidor de licencias. No es necesario que el empaquetador se conecte al servidor de licencias para intercambiar información sobre el contenido. Todo lo que el servidor de licencias necesita saber para emitir una licencia está incluido en los metadatos de contenido.

Cuando se cifra un archivo, su contenido no se puede analizar sin la licencia adecuada. Puede utilizar Primetime DRM para seleccionar las partes del archivo que desea cifrar. Dado que Primetime DRM puede analizar el formato de archivo del contenido de vídeo, puede cifrar de forma inteligente partes selectivas de un archivo en lugar de un archivo completo. Los datos, como los metadatos y los puntos de referencia, pueden permanecer sin cifrar para que los motores de búsqueda puedan seguir buscando en el archivo.

Un fragmento de contenido especificado puede tener varias políticas DRM. Por ejemplo, puede obtener una licencia del contenido en diferentes modelos comerciales sin tener que empaquetarlo varias veces. Además, puede permitir el acceso anónimo durante un corto periodo de tiempo y, a continuación, permitir que el cliente compre el contenido para tener acceso ilimitado. Si el contenido se empaqueta utilizando varias directivas DRM, el servidor de licencias debe implementar una lógica para seleccionar qué directiva DRM debe utilizarse para emitir una licencia.

>[!NOTE]
>
>La arquitectura permite especificar las políticas de DRM de uso y enlazarlas al contenido cuando este se empaqueta. Para que un cliente pueda reproducir contenido, debe adquirir una licencia para un equipo especificado. La licencia especifica las reglas de uso que se aplican y proporciona la clave que debe utilizarse para descifrar contenido. La directiva DRM representa una plantilla para generar una licencia. Sin embargo, el servidor de licencias puede anular las reglas de uso cuando emite una licencia. Estas restricciones, como los tiempos de caducidad o los períodos de reproducción, pueden invalidar la licencia.

Primetime DRM proporciona una API para pasar el CEK. Si no se especifica ningún CEK, el SDK lo genera de forma aleatoria. Normalmente, se necesita una CEK diferente para cada sección del contenido. Sin embargo, en el flujo dinámico, es probable que utilice la misma CEK para todos los archivos que componen ese contenido. Por lo tanto, un usuario solo necesita una licencia para realizar la transición sin problemas de una velocidad de bits a otra. Si desea utilizar la misma clave y licencia para varios fragmentos de contenido, debe pasar lo mismo `DRMParameters` objeto a `MediaEncrypter.encryptContent()`, o pase el CEK usando `V2KeyParameters.setContentEncryptionKey()`. Si desea utilizar una clave y una licencia diferentes para cada sección de contenido, debe crear una nueva `DRMParameters` para cada archivo.

Al empaquetar contenido mediante la rotación de claves, puede controlar las claves de rotación que se utilizan y la frecuencia con la que cambian las claves. `F4VDRMParameters` y `FLVDRMParameters` implementar el `KeyRotationParameters` interfaz. A través de esta interfaz, puede habilitar la rotación de claves. También debe especificar una `RotatingContentEncryptionKeyProvider`. Para cada ejemplo cifrado, esta clase determina la clave de rotación que se va a utilizar. Puede implementar su propio proveedor o utilizar el `TimeBasedKeyProvider` incluido con el SDK. Esta implementación genera aleatoriamente una nueva clave después de un número determinado de segundos.

En algunos casos, es posible que tenga que almacenar los metadatos de contenido como un archivo independiente y ponerlos a disposición del cliente aparte del contenido. En ese caso, debe invocar a `MediaEncrypter.encryptContent()`, que devuelve un `MediaEncrypterResult` objeto. Llamada `MediaEncrypterResult.getKeyInfo()` y convierta el resultado en `V2KeyStatus`. A continuación, recupere los metadatos de contenido y almacénelos en un archivo.

Todas estas tareas se pueden realizar con la API de Java.

Consulte *Referencia de API de DRM de Adobe Primetime* para obtener más información sobre la API de Java.

Consulte *Uso de las implementaciones de referencia de DRM de Adobe Primetime* para obtener información sobre la implementación de referencia del empaquetador de medios.
