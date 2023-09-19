---
description: Los flujos de trabajo de DRM implican empaquetar el contenido, proporcionar licencias para el contenido y reproducir el contenido protegido desde su propia aplicación de vídeo. El flujo de trabajo suele ser similar para cada solución de DRM, pero con algunas diferencias está en los detalles.
title: Flujo de trabajo de varios DRM para FairPlay
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# Flujo de trabajo de varios DRM para FairPlay {#multi-drm-workflow-for-fairplay}

Los flujos de trabajo de DRM implican empaquetar el contenido, proporcionar licencias para el contenido y reproducir el contenido protegido desde su propia aplicación de vídeo. El flujo de trabajo suele ser similar para cada solución de DRM, pero con algunas diferencias está en los detalles.

Este flujo de trabajo Multi-DRM le lleva a través de la configuración, el empaquetado, las licencias y la reproducción de contenido HLS protegido con Apple FairPlay. Este flujo de trabajo también incluye instrucciones opcionales para implementar la reproducción sin conexión y la rotación de licencias.

## Habilitar el servicio ExpressPlay para FairPlay {#enable-expressplay-service-for-fairplay}

La solución DRM FairPlay de Apple requiere cierta configuración cuando se utiliza con los servicios DRM ExpressPlay. Esto implica obtener las credenciales de Apple y cargarlas en ExpressPlay.

Siga estos pasos para habilitar el servicio ExpressPlay para la protección de contenido de FairPlay.

1. Obtenga credenciales de Apple.

   Estas credenciales se proporcionan de forma exclusiva a cada proveedor de servicios. Debe solicitarlos rellenando el siguiente formulario: [https://developer.apple.com/contact/fps/](https://developer.apple.com/contact/fps/).

   >[!NOTE]
   >
   >Seleccionar **[!UICONTROL Content Provider]** para la función principal.

   Una vez aprobada la solicitud, Apple le enviará un *Paquete de implementación de flujo FairPlay*.
1. Generar una solicitud de firma de certificado.

   Puede utilizar [!DNL openssl] para generar el par de claves pública y privada, y la solicitud firmada de certificado (CSR).

   1. Genere su par de claves.

      ```
      openssl genrsa -aes256 -out privatekey.pem 1024 
      ```

   1. Genere su CSR.

      ```
      openssl req -new -sha1 -key privatekey.pem -out certreq.csr  
        -subj "/CN=SubjectName /OU=OrganizationalUnit /O=Organization /C=US"
      ```

      >[!NOTE]
      >
      >Las instrucciones para este paso se encuentran en su *Paquete de implementación de flujo FairPlay*, pero se incluyen aquí para su comodidad. Si tiene problemas con esta parte del proceso, consulte las instrucciones en *FairPlayCertificateCreation.pdf* (en el paquete de implementación).

1. Cargue su CSR a través de Apple developer portal.
   1. El agente de equipo del equipo de desarrollo debe iniciar sesión en [!DNL developer.apple.com/account].
   1. Haga clic en **[!UICONTROL Certificates, Identifiers & Profiles]**, luego seleccione la **[!UICONTROL iOS, tvOS, watchOS]** en la parte superior izquierda de la página, y luego haga clic en **[!UICONTROL Certificates->Production]** a la izquierda de la página.
   1. Haga clic en **[!UICONTROL +]** en la parte superior derecha de la página para solicitar un nuevo certificado. Seleccione el **[!UICONTROL FairPlay Streaming Certificate]** opción en **[!UICONTROL Production]**.

      El *Agregar certificado de iOS* se abre.
   1. En el *Agregar certificado de iOS*, cargue el archivo CSR generado en el paso 2.b. y haga clic en **[!UICONTROL Generate]**.

      La clave secreta de la aplicación (ASK) se muestra en el mismo cuadro de diálogo.
   1. Anote su ASK y guárdelo en un lugar seguro.
   1. Escriba la clave en su TAREA para completar la generación de certificados y haga clic en **[!UICONTROL Continue]**.
   1. Después de comprobar que ha guardado la TAREA, haga clic en **[!UICONTROL Generate]** para continuar.

      >[!NOTE]
      >
      >Es importante que guarde una copia de su TAREA y la almacene de forma segura. *Si tu ASK se ve comprometido, ya no podrás proteger tu contenido con FairPlay Streaming.* Solo se asigna una (1) TAREA a su equipo. El valor no se volverá a proporcionar y no podrá recuperarlo más adelante.

   1. Descargue el certificado FPS.

      Asegúrese de guardar una copia de seguridad de la clave privada (del paso 2.a.) y de la clave pública (el certificado de FPS que descargó en este paso) en un lugar seguro.
1. Configura tu cuenta de ExpressPlay con tus credenciales de FairPlay.
   1. Supongamos que el nombre del certificado que descargó en el paso 3.h es [!DNL fairplay.cer].
   1. Abra el [!DNL fairplay.cer] con la utilidad Apple Keychain Access.
   1. Filtre los certificados introduciendo &quot; `fairplay`&quot; en el campo de búsqueda situado en la parte superior derecha.
   1. Identifique el certificado FairPlay de su empresa.

      El nombre de su empresa debe estar asociado al certificado emitido por Apple.
   1. Expanda el certificado seleccionando la flecha de expansión y haga clic con el botón derecho en la clave privada.
   1. Seleccionar **[!UICONTROL Export "Your Company Name"]** y guarde el [!DNL .p12] archivo.

      Se le pedirá que asigne una contraseña para proteger este archivo. Tome nota de esta contraseña, ya que deberá enviarla con su paquete de credenciales.
   1. Inicie sesión en su cuenta el [www.expressplay.com](https://www.expressplay.com).
   1. Clic **[!UICONTROL DRM SERVICES]** en la parte superior izquierda, seleccione la **[!UICONTROL FairPlay]** pestaña.
   1. Sube tus credenciales de FairPlay a tu cuenta de ExpressPlay.

      1. Cree un archivo de texto que contenga el valor de su ASK (debe tener 32 caracteres, por ejemplo: `1234567890abcdef1234567890abcdef`) y seleccione este archivo para cargarlo.
      1. Seleccione el archivo PKCS12 del paso 4.f. para cargar.
      1. Introduzca la contraseña del archivo PKCS12 desde el paso 4.f.
      1. Haga clic en el botón Upload.

Ahora puede crear aplicaciones de iOS o páginas de HTML5 con protección de contenido FairPlay junto con su [!DNL fairplay.cer] certificado que utiliza el servicio ExpressPlay para FairPlay.

<!--<a id="fig_sjr_2pn_sv"></a>-->

![](assets/multi_drm_expressplay_drm_services_web.png)

### Empaqueta tu contenido para FairPlay {#package-your-content-for-fairplay}

Para empaquetar su contenido, puede usar Adobe Offline Packager u otras herramientas como el Packager Bento4 de ExpressPlay.

Los empaquetadores preparan el vídeo para su reproducción (por ejemplo, fragmentando el archivo original y poniéndolo en un manifiesto), y protegen el vídeo con la solución DRM elegida (en este caso FairPlay):

* [Adobe Offline Packager for FairPlay DRM](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=21)
* [ExpressPlay Packagers - Bento4 para HLS](https://www.bento4.com/developers/hls/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_hls_web.png)

1. Empaquete el contenido.

   Este es un ejemplo de empaquetado con Adobe Offline Packager. El empaquetador utiliza un archivo de configuración (por ejemplo, [!DNL fairplay.xml]), que tiene este aspecto:

   ```
   <config>
   <in_path>mp4_file_path</in_path>
   <out_type>hls</out_type>
   <out_path>out_file_path</out_path>
   <drm/>
   <drm_sys>FAIRPLAY</drm_sys>
   <frag_dur>4</frag_dur>
   <target_dur>6</target_dur>
   <key_file_path>creds/fairplay.bin</key_file_path>
   <iv_file_path>creds/iv.bin</iv_file_path>
   <key_url>user_provided_value</key_url>
   <content_id>_default_</content_id>
   </config>
   ```

   * `in_path` : Esta entrada apunta a la ubicación del vídeo de origen en la máquina de embalaje local.
   * `out_type` - Esta entrada describe el tipo de salida empaquetada, en este caso HLS para FairPlay.
   * `out_path` - La ubicación del equipo local a la que desea que vaya la salida.
   * `drm_sys` - La solución DRM para la que está empaquetando. Esto es `FAIRPLAY` en este caso.
   * `frag_dur` - Duración del fragmento en segundos.
   * `target_dur` - La duración de destino de la salida HLS.
   * `key_file_path` : Esta es la ubicación del archivo de licencia en la máquina de empaquetado que sirve como clave de cifrado de contenido (CEK). Es una cadena hexadecimal de 16 bytes codificada en Base-64.
   * `iv_file_path` - Esta es la ubicación del archivo IV en su máquina de embalaje.
   * `key_url` - El parámetro URI del `EXT-X-KEY` etiqueta del [!DNL .m3u8] archivo.
   * `content_id` - Valor predeterminado.

   Como se indica en la [Documentación del empaquetador](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=7), &quot;Como práctica recomendada, cree un archivo de configuración que contenga las opciones comunes que desee utilizar para generar los resultados. A continuación, cree el resultado proporcionando opciones específicas como argumento de línea de comandos&quot;.

   ```
   java -jar OfflinePackager.jar -in_path sample.mp4 -out_type hls 
   -out_path out_file_path -drm -drm_sys FAIRPLAY -key_file_path "creds/fairplay.bin" 
   -key_url "user_provided_value"
   ```

   El archivo M3U8 generado tiene un `EXT-X-KEY` que aparece de la siguiente manera:

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="user_provided_value",​
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1" 
   ```

### Establecer directivas para FairPlay {#setting-policies-for-fairplay}

Puede establecer directivas para el contenido protegido por FairPlay mediante un servidor de derechos. Puede configurar su propio servidor o utilizar un servidor de derechos de ejemplo proporcionado por el Adobe.

Adobe proporciona un servidor de derechos de ExpressPlay de muestra (SEES) que muestra cómo hacerlo *basado en el tiempo* y *de enlace de dispositivos* derecho. Este servidor de derechos de ejemplo se basa en los servicios ExpressPlay.

[Servidor de referencia: Servidor de derechos de ExpressPlay de muestra (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

* [Servicio de referencia: derecho basado en el tiempo](../../multi-drm-workflows/feature-topics/sees-reference-server-time-entitlement.md)
* [Servicio de referencia: derecho de enlace de dispositivo](../../multi-drm-workflows/feature-topics/sees-reference-server-binding-entitlement.md)

## Licencias y reproducción para FairPlay {#licensing-and-playback-for-fairplay}

Las licencias y la reproducción de contenido protegido por FairPlay requieren el intercambio de esquemas de URL, entre el esquema utilizado en el archivo de manifiesto de vídeo (skd:) y el utilizado en las solicitudes de token de ExpressPlay (https:).

Las instrucciones para implementar las licencias y la reproducción desde un cliente TVSDK de iOS se encuentran aquí: [Habilitar Apple FairPlay en aplicaciones TVSDK](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md). También puede implementar opcionalmente la reproducción sin conexión y la rotación de licencias para FairPlay.

## HLS sin conexión con FairPlay {#section_047A05D1E3B64883858BC601CFC8F759}

Es posible que desee permitir a los usuarios reproducir contenido protegido por FairPlay cuando sus licencias no se puedan recuperar porque el reproductor está aislado de la web (como en un avión).

Antes de comenzar esta tarea, descargue y lea el documento de Apple **&quot;Reproducción sin conexión con transmisión FairPlay y transmisión HTTP en directo&quot;**. Lea la guía para aprender a descargar segmentos de Transport Stream (TS) y guardarlos en su equipo local.

Implemente la reproducción sin conexión para FairPlay con este flujo de trabajo:

1. Descargue el segmento HLS TS.
1. Solicite una licencia de alquiler permanente al servidor FairPlay (consulte **&quot;Política de Alquiler Persistente FairPlay&quot;**).
1. Guarde el `persistentContentKey`.
1. Reproducir el contenido de FairPlay sin conexión.

>[!NOTE]
>
>FairPlay Streaming en el cliente no inicia el descifrado si la clave de contenido persistente ha caducado. Sin embargo, la experiencia del usuario se mantendrá si la clave de contenido caduca durante la reproducción.
>
>Consulte [Uso del streaming en directo HTTP](https://developer.apple.com/library/content/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW3) para obtener más información.

### Rotación de licencia de FairPlay {#section_D32AA08C61474B4F876AC2A5F18CB879}

La rotación de licencias es un esquema para evitar el hackeo de licencias de contenido que se reproduce durante mucho tiempo.

En un manifiesto de M3U8, cada etiqueta de clave se aplicará a los siguientes segmentos de TS hasta la siguiente etiqueta de clave o hasta el final del archivo.

Para agregar la rotación de licencias, haga lo siguiente:

* Inserte una nueva etiqueta de clave FairPlay durante el tiempo de rotación de la licencia.

  Se puede añadir cualquier número de etiquetas de clave.

  Para el contenido lineal, asegúrese de mantener la etiqueta de clave más reciente en la ventana de M3U8. iOS solicitará el siguiente M3U8 cuando queden aproximadamente dos segmentos TS por reproducir (alrededor de 20 segundos). Si el nuevo M3U8 contiene nuevas etiquetas de clave, todas las solicitudes de clave se producirán inmediatamente. No se volverán a solicitar las claves existentes anteriormente. iOS esperará a que finalicen todas las solicitudes clave antes de que comience la reproducción.

  En el caso del contenido de VOD con rotación de licencia, todas las solicitudes de clave se producirán al principio de la reproducción.

  A continuación se muestra un ejemplo de M3U8 con rotación de clave:

  ```
  #EXTM3U
  #EXT-X-TARGETDURATION:10
  #EXT-X-VERSION:5
  #EXT-X-MEDIA-SEQUENCE:0
  #EXT-X-PLAYLIST-TYPE:VOD
  #EXT-X-KEY:METHOD=SAMPLE-AES,URI="skd://one?cek=1dc2cc71d913f4f74eca0c4632
  212b25&iv=e21f0f72b6363ff6143737cb1e9ca8d7",KEYFORMAT="com.apple.streaming
  keydelivery",KEYFORMATVERSIONS="1"
  #EXTINF:10,
  fileSequence0.ts
  #EXTINF:10,
  fileSequence1.ts
  #EXTINF:10,
  fileSequence2.ts
  #EXTINF:10,
  fileSequence3.ts
  #EXTINF:10,
  fileSequence4.ts
  #EXTINF:10,
  fileSequence5.ts
  #EXTINF:10,
  fileSequence6.ts
  #EXTINF:10,
  fileSequence7.ts
  #EXTINF:10,
  #EXT-X-KEY:METHOD=SAMPLE-AES,URI="skd://two?cek=f6efc698b96cf8f4fa46d5237d
  337c77&iv=18401077091784bcda8079acf978dc95",KEYFORMAT="com.apple.streaming
  keydelivery",KEYFORMATVERSIONS="1"
  #EXTINF:10,
  fileSequence8.ts
  #EXTINF:10,
  ```
