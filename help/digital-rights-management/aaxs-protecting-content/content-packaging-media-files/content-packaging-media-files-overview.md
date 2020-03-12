---
seo-title: Información general
title: Información general
uuid: 11cf1f1f-a4b2-4ac2-aae7-e925d96729d2
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Información general {#overview}

*El empaquetado* se refiere al proceso de codificación y aplicación de una política a los archivos FLV o F4V. Utilice las API de empaquetado de medios para empaquetar archivos. El SDK de Java de Adobe Access solo puede empaquetar contenido Flash y AIR de descarga progresiva, como FLV, F4V y MP4. Para empaquetar contenido mediante Adobe Access DRM para otros formatos de contenido, como Adobe HTTP Dynamic Streaming (HDS) o Apple HTTP Live Streaming (HLS), tendrá que utilizar otras herramientas, como Adobe Media Server ( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) o un codificador que implemente el SDK de difusión de Adobe ( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)). De forma alternativa, los clientes pueden elegir utilizar el conjunto de herramientas de Java Primetime Packager de Adobe, que puede empaquetar contenido para diversos formatos de destino, como HDS, HLS y DASH.

El empaquetado se desenlaza del servidor de licencias. No es necesario que el empaquetador se conecte al servidor de licencias para intercambiar información sobre el contenido. Todo lo que el servidor de licencias necesita saber para emitir la licencia se incluye en los metadatos de contenido.

Cuando se cifra un archivo, su contenido no se puede analizar sin la licencia adecuada. Adobe Access permite seleccionar qué partes del archivo se van a cifrar. Dado que Adobe® Access™ puede analizar el formato de archivo del contenido FLV y F4V, puede cifrar de forma inteligente partes selectivas del archivo en lugar de todo el archivo. Los datos como metadatos y puntos de referencia pueden permanecer sin cifrar para que los motores de búsqueda puedan seguir buscando en el archivo.

Es posible que un determinado contenido tenga varias políticas. Esto podría resultar útil, por ejemplo, si desea obtener licencias de contenido en diferentes modelos comerciales sin tener que empaquetar el contenido varias veces. Por ejemplo, puede permitir el acceso anónimo durante un breve período de tiempo y, después de eso, permitir al cliente comprar el contenido y tener acceso ilimitado. Si el contenido se empaqueta con varias directivas, el servidor de licencias debe implementar la lógica para seleccionar la directiva que se debe utilizar para emitir una licencia.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>La arquitectura permite que las políticas de uso se especifiquen y enlazen al contenido cuando se empaqueta el contenido. Para que un cliente pueda reproducir contenido, debe adquirir una licencia para ese equipo. La licencia especifica las reglas de uso que se aplican y proporciona la clave utilizada para descifrar el contenido. La directiva es una plantilla para generar la licencia, pero el servidor de licencias puede elegir anular las reglas de uso al emitir la licencia. Tenga en cuenta que la licencia puede no ser válida debido a restricciones como tiempos de caducidad o ventanas de reproducción.

Existen numerosas opciones disponibles al empaquetar contenido. Estos se especifican en la interfaz y en las clases que implementan dicha interfaz, que son los `DRMParameters` y `F4VDRMParameters` `FLVDRMParameters`. Con estas clases puede definir parámetros de firma y clave, así como también indicar si desea cifrar contenido de audio, vídeo o datos de secuencias de comandos. Para ver cómo se implementan en la implementación de referencia, consulte las descripciones de las opciones de línea de comandos de Media Packager que se describen en *Uso de las implementaciones* de referencia de Adobe Access. Estas opciones se basan en la API de Java y, por lo tanto, están disponibles para el uso programático.

Las opciones de empaquetado incluyen:

* Opciones de codificación (audio, vídeo, cifrado parcial).
* URL del servidor de licencias (el cliente utiliza esta URL como la URL base para todas las solicitudes enviadas al servidor de licencias)
* Certificado de transporte del servidor de licencias
* Certificado de servidor de licencias, utilizado para cifrar el CEK.
* Credenciales de Packager para firmar metadatos

Adobe Access proporciona una API para pasar el CEK. Si no se especifica CEK, el SDK lo genera aleatoriamente. Normalmente necesita un CEK diferente para cada fragmento de contenido. Sin embargo, en el flujo dinámico, es probable que utilice el mismo CEK para todos los archivos de ese contenido, por lo que el usuario solo necesita una licencia única y puede realizar una transición sin problemas de una velocidad de bits a otra. Para utilizar la misma clave y licencia para varios fragmentos de contenido, pase el mismo `DRMParameters` objeto a `MediaEncrypter.encryptContent()`o pase el CEK usando `V2KeyParameters.setContentEncryptionKey()`. Para utilizar una clave y una licencia diferentes para cada fragmento de contenido, cree una nueva `DRMParameters` instancia para cada archivo.

Al empaquetar contenido mediante rotación de claves, puede controlar las teclas de rotación utilizadas y la frecuencia con la que cambian las teclas. `F4VDRMParameters` e `FLVDRMParameters` implemente la `KeyRotationParameters` interfaz. A través de esta interfaz, puede activar la rotación de claves. También debe especificar un `RotatingContentEncryptionKeyProvider`. Para cada muestra cifrada, esta clase determina la tecla de rotación que se va a utilizar. Puede implementar su propio proveedor o utilizar el `TimeBasedKeyProvider` incluido con el SDK. Esta implementación genera aleatoriamente una nueva clave después de un número especificado de segundos.

En algunos casos, es posible que deba almacenar los metadatos de contenido como un archivo independiente y ponerlos a disposición del cliente de forma independiente del contenido. Para ello, invoque `MediaEncrypter.encryptContent()`, que devuelve un `MediaEncrypterResult` objeto. Llama `MediaEncrypterResult.getKeyInfo()` y envía el resultado a `V2KeyStatus`. A continuación, recupere los metadatos del contenido y guárdelos en un archivo.

Todas estas tareas se pueden realizar mediante la API de Java. Para obtener más información sobre la API de Java que se describe en este capítulo, consulte Referencia de la API de *Adobe Access*.

Para obtener información sobre la implementación de referencia de Media Packager, consulte *Uso de las implementaciones* de referencia de Adobe Access.
