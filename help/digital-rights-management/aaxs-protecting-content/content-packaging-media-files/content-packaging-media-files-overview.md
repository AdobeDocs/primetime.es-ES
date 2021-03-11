---
title: Información general
description: Información general
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---


# Información general {#overview}

** El empaquetado hace referencia al proceso de codificación y aplicación de una política a los archivos FLV o F4V. Utilice las API de empaquetado de medios para empaquetar archivos. El SDK de Java de Acceso a Adobe solo puede empaquetar contenido de Flash y AIR de descarga progresiva, como FLV, F4V y MP4. Para empaquetar contenido utilizando DRM de acceso al Adobe para otros formatos de contenido, como HTTP Dynamic Streaming de Adobe (HDS) o transmisión en directo HTTP (HLS) de Apple, tendrá que utilizar otras herramientas, como el Servidor de Adobes Medium ( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) o un codificador que implemente el SDK de difusión de Adobe ( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)). Como alternativa, los clientes tienen la opción de utilizar el conjunto de herramientas de Adobe Java Primetime Packager, que puede empaquetar contenido para una variedad de formatos de destino, como HDS, HLS y DASH.

El empaquetado se desasocia del servidor de licencias. No es necesario que el empaquetador se conecte al servidor de licencias para intercambiar información sobre el contenido. Todo lo que el servidor de licencias necesita saber para emitir la licencia se incluye en los metadatos de contenido.

Cuando se cifra un archivo, su contenido no se puede analizar sin la licencia adecuada. Adobe Access permite seleccionar qué partes del archivo se van a cifrar. Como Adobe® Access™ puede analizar el formato de archivo del contenido FLV y F4V, puede cifrar de forma inteligente partes selectivas del archivo en lugar de todo el archivo. Los datos, como los metadatos y los puntos de referencia, pueden permanecer sin encriptar para que los motores de búsqueda puedan seguir buscando en el archivo.

Es posible que un determinado fragmento de contenido tenga varias políticas. Esto podría resultar útil, por ejemplo, si desea obtener una licencia del contenido en distintos modelos de negocio sin tener que empaquetar el contenido varias veces. Por ejemplo, puede permitir el acceso anónimo durante un breve periodo de tiempo, y después de eso, permitir al cliente comprar el contenido y tener acceso ilimitado. Si el contenido se empaqueta con varias directivas, el servidor de licencias debe implementar la lógica para seleccionar qué directiva utilizar para emitir una licencia.

>[!NOTE]
>
>La arquitectura permite especificar políticas de uso y enlazarlas al contenido cuando se empaqueta el contenido. Para que un cliente pueda reproducir contenido, debe adquirir una licencia para ese equipo. La licencia especifica las reglas de uso que se aplican y proporciona la clave utilizada para descifrar el contenido. La directiva es una plantilla para generar la licencia, pero el servidor de licencias puede optar por anular las reglas de uso al emitir la licencia. Tenga en cuenta que la licencia puede no ser válida debido a restricciones como tiempos de caducidad o ventanas de reproducción.

Hay numerosas opciones disponibles al empaquetar contenido. Se especifican en la interfaz `DRMParameters` y en las clases que implementan esa interfaz, que son `F4VDRMParameters` y `FLVDRMParameters`. Con estas clases puede definir parámetros de firma y clave, así como indicar si desea cifrar contenido de audio, contenido de vídeo o datos de secuencias de comandos. Para ver cómo se implementan en la implementación de referencia, consulte las descripciones de las opciones de línea de comandos de Media Packager que se tratan en *Uso de las implementaciones de referencia de acceso a Adobe*. Estas opciones se basan en la API de Java y, por lo tanto, están disponibles para uso programático.

Las opciones de empaquetado incluyen:

* Opciones de codificación (audio, vídeo, cifrado parcial).
* URL del servidor de licencias (el cliente utiliza esta URL como URL base para todas las solicitudes enviadas al servidor de licencias)
* Certificado de transporte del servidor de licencias
* Certificado del servidor de licencias, utilizado para cifrar el CEK.
* Credenciales del paquete para firmar metadatos

Adobe Access proporciona una API para pasar el CEK. Si no se especifica ningún CEK, el SDK lo genera aleatoriamente. Normalmente necesita un CEK diferente para cada parte de contenido. Sin embargo, en la transmisión dinámica, es probable que utilice el mismo CEK para todos los archivos de ese contenido, por lo que el usuario solo necesita una licencia única y puede pasar sin problemas de una velocidad de bits a otra. Para utilizar la misma clave y licencia para varios fragmentos de contenido, pase el mismo objeto `DRMParameters` a `MediaEncrypter.encryptContent()` o pase el CEK utilizando `V2KeyParameters.setContentEncryptionKey()`. Para utilizar una clave y licencia diferentes para cada fragmento de contenido, cree una nueva instancia `DRMParameters` para cada archivo.

Al empaquetar contenido mediante la rotación de claves, puede controlar las claves de rotación utilizadas y la frecuencia con la que cambian las claves. `F4VDRMParameters` e  `FLVDRMParameters` implemente la  `KeyRotationParameters` interfaz. A través de esta interfaz, puede habilitar la rotación de claves. También debe especificar un `RotatingContentEncryptionKeyProvider`. Para cada muestra cifrada, esta clase determina la clave de rotación que se utilizará. Puede implementar su propio proveedor o utilizar el `TimeBasedKeyProvider` incluido con el SDK. Esta implementación genera aleatoriamente una nueva clave después de un número específico de segundos.

En algunos casos, es posible que tenga que almacenar los metadatos de contenido como un archivo independiente y ponerlos a disposición del cliente aparte del contenido. Para ello, invoque `MediaEncrypter.encryptContent()`, que devuelve un objeto `MediaEncrypterResult`. Llame a `MediaEncrypterResult.getKeyInfo()` y convierta el resultado en `V2KeyStatus`. A continuación, recupere los metadatos de contenido y guárdelos en un archivo.

Todas estas tareas se pueden realizar mediante la API de Java. Para obtener más información sobre la API de Java que se describe en este capítulo, consulte *Referencia de la API de acceso a Adobe*.

Para obtener información sobre la implementación de referencia de Media Packager, consulte *Uso de las implementaciones de referencia de acceso a Adobe*.
