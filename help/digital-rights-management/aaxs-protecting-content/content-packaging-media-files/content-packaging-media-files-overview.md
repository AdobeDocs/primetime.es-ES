---
title: Información general
description: Información general
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Información general {#overview}

*Empaquetando* hace referencia al proceso de cifrar y aplicar una directiva a archivos FLV o F4V. Utilice las API de empaquetado de medios para empaquetar archivos. El SDK de Java de Adobe Access solo puede empaquetar contenido de AIR y Flash de descarga progresiva, como FLV, F4V y MP4. Para empaquetar contenido mediante DRM de acceso al Adobe para otros formatos de contenido, como HTTP Dynamic Streaming de Adobe (HDS) o Apple HTTP Live Streaming (HLS), deberá utilizar otras herramientas, como Adobe Media Server ( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) o un codificador que implemente el SDK de Adobe Broadcast ( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)). Como alternativa, los clientes tienen la opción de utilizar el conjunto de herramientas del empaquetador Java Primetime de Adobe, que puede empaquetar contenido para una variedad de formatos de destino, como HDS, HLS y DASH.

El paquete se desacopla del servidor de licencias. No es necesario que el empaquetador se conecte al servidor de licencias para intercambiar información sobre el contenido. Todo lo que el servidor de licencias necesita saber para emitir la licencia está incluido en los metadatos de contenido.

Cuando se cifra un archivo, su contenido no se puede analizar sin la licencia adecuada. Adobe Access permite seleccionar qué partes del archivo se van a cifrar. Como Adobe® Access™ puede analizar el formato de archivo del contenido FLV y F4V, puede cifrar de forma inteligente partes selectivas del archivo en lugar de todo el archivo en su conjunto. Los datos, como los metadatos y los puntos de referencia, pueden permanecer sin cifrar para que los motores de búsqueda puedan seguir buscando en el archivo.

Es posible que un fragmento de contenido determinado tenga varias políticas. Esto podría resultar útil, por ejemplo, si desea obtener una licencia del contenido en diferentes modelos comerciales sin tener que empaquetarlo varias veces. Por ejemplo, puede permitir el acceso anónimo durante un corto periodo de tiempo y, después, permitir al cliente comprar el contenido y tener acceso ilimitado. Si el contenido se empaqueta utilizando varias directivas, el servidor de licencias debe implementar una lógica para seleccionar qué directiva utilizar para emitir una licencia.

>[!NOTE]
>
>La arquitectura permite especificar las políticas de uso y enlazarlas al contenido cuando este se empaqueta. Para que un cliente pueda reproducir contenido, debe adquirir una licencia para ese equipo. La licencia especifica las reglas de uso que se aplican y proporciona la clave utilizada para descifrar el contenido. La directiva es una plantilla para generar la licencia, pero el servidor de licencias puede optar por anular las reglas de uso al emitir la licencia. Tenga en cuenta que la licencia puede quedar invalidada por restricciones como los tiempos de caducidad o los períodos de reproducción.

Hay numerosas opciones disponibles al empaquetar contenido. Se especifican en el `DRMParameters` y las clases que implementan esa interfaz, que son las siguientes `F4VDRMParameters` y `FLVDRMParameters`. Con estas clases puede establecer parámetros de firma y clave, así como indicar si se debe cifrar contenido de audio, contenido de vídeo o datos de secuencias de comandos. Para ver cómo se implementan en la implementación de referencia, consulte las descripciones de las opciones de línea de comandos de Media Packager que se describen en *Uso de las implementaciones de referencia de acceso a Adobe*. Estas opciones se basan en la API de Java y, por lo tanto, están disponibles para su uso mediante programación.

Las opciones de empaquetado incluyen:

* Opciones de cifrado (audio, vídeo, cifrado parcial).
* URL del servidor de licencias (el cliente la usa como URL base para todas las solicitudes enviadas al servidor de licencias)
* Certificado de transporte del servidor de licencias
* Certificado del servidor de licencias, utilizado para cifrar el CEK.
* Credencial del empaquetador para firmar metadatos

Adobe Access proporciona una API para pasar el CEK. Si no se especifica ningún CEK, el SDK lo genera de forma aleatoria. Normalmente, se necesita una CEK diferente para cada parte del contenido. Sin embargo, en Dynamic Streaming, probablemente utilizaría la misma CEK para todos los archivos de ese contenido, por lo que el usuario solo necesita una licencia única y puede pasar sin problemas de una velocidad de bits a otra. Para utilizar la misma clave y licencia para varios fragmentos de contenido, pase el mismo `DRMParameters` objeto a `MediaEncrypter.encryptContent()`, o pase el CEK usando `V2KeyParameters.setContentEncryptionKey()`. Para utilizar una clave y una licencia diferentes para cada parte de contenido, cree un nuevo `DRMParameters` para cada archivo.

Al empaquetar contenido mediante la rotación de claves, puede controlar las claves de rotación utilizadas y la frecuencia con la que cambian las claves. `F4VDRMParameters` y `FLVDRMParameters` implementar el `KeyRotationParameters` interfaz. A través de esta interfaz, puede habilitar la rotación de claves. También debe especificar una `RotatingContentEncryptionKeyProvider`. Para cada ejemplo cifrado, esta clase determina la clave de rotación que se va a utilizar. Puede implementar su propio proveedor o utilizar el `TimeBasedKeyProvider` incluido con el SDK. Esta implementación genera aleatoriamente una nueva clave después de un número determinado de segundos.

En algunos casos, es posible que tenga que almacenar los metadatos de contenido como un archivo independiente y ponerlos a disposición del cliente aparte del contenido. Para ello, invoque `MediaEncrypter.encryptContent()`, que devuelve un `MediaEncrypterResult` objeto. Llamada `MediaEncrypterResult.getKeyInfo()` y convierta el resultado en `V2KeyStatus`. A continuación, recupere los metadatos de contenido y almacénelos en un archivo.

Todas estas tareas se pueden realizar mediante la API de Java. Para obtener más información sobre la API de Java que se analiza en este capítulo, consulte *Referencia de API de acceso de Adobe*.

Para obtener información sobre la implementación de referencia del empaquetador de medios, consulte *Uso de las implementaciones de referencia de acceso a Adobe*.
