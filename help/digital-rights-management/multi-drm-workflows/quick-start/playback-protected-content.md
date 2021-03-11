---
description: Para probar la solución DRM, necesita una aplicación de vídeo que pueda procesar la solución DRM concreta con la que está trabajando. Este reproductor podría ser un reproductor de muestra disponible por Adobe o su propia aplicación de vídeo basada en TVSDK.
title: Reproducción del contenido protegido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---


# Reproducción del contenido protegido {#playback-your-protected-content}

Para probar la solución DRM, necesita una aplicación de vídeo que pueda procesar la solución DRM concreta con la que está trabajando. Este reproductor podría ser un reproductor de muestra disponible por Adobe o su propia aplicación de vídeo basada en TVSDK.

1. Use la URL del servidor de licencias de la respuesta de token que obtuvo del servidor ExpressPlay para comprobar si puede reproducir el contenido protegido.

   * **Widevine** : use la respuesta Widevine directamente como se recibió de su solicitud de token de licencia de ExpressPlay.
   * **PlayReady** : obtenga la URL y el token del servidor de licencias del objeto JSON devuelto desde la solicitud del token de licencia.
   * **FairPlay** : use la respuesta de FairPlay directamente como se recibe de su solicitud de token de licencia de ExpressPlay.

1. Pruebe la reproducción del contenido protegido utilizando su propio reproductor o un reproductor de muestra de Adobe existente.

   Proporcione la URL al contenido protegido (la ubicación de su manifiesto M3U8 o MPD, según la solución DRM que esté probando).

   Según la interfaz proporcionada por el reproductor con el que realice la prueba, se le puede pedir que proporcione la URL de licencia y el token separados como cadenas en campos de entrada, o como un objeto JSON pegado en un cuadro de texto, o tal vez como un parámetro de consulta en la URL.

   A continuación se enumeran algunas posibilidades para los reproductores de prueba:

   * Reproductor de referencia HTML5:

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * Shaka Player:

      ```
      https://shaka-player-demo.appspot.com
      ```

   * Reproductor TVSDK de muestra (en desarrollo) -

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **Comprobación de la reproducción al probar la configuración de FairPlay:** FairPlay requiere algunos pasos adicionales para reproducir el contenido cuando utilice los servidores de licencias ExpressPlay. Si utiliza [!DNL curl] para probar las conexiones (como se describe en [Licencias](../../multi-drm-workflows/quick-start/handle-the-licensing.md)), debe *editar el manifiesto M3U8* (su contenido empaquetado) de la siguiente manera:

1. Agregue la respuesta que obtuvo de su solicitud de token de licencia a la etiqueta `#EXT-X-KEY:` del manifiesto; y
1. Cambie el protocolo de esa URL de la respuesta (ahora en el manifiesto) de `https://` a `skd://`.

   Este es un ejemplo completo de la prueba de reproducción con FairPlay, incluido el paso de licencia:

1. Utilice la solicitud del token de licencia de FairPlay para obtener la URL del token de licencia. (Utilice su propio autenticador de cliente de producción y asegúrese de utilizar el mismo CEK y `iv` que se utilizó para empaquetar el contenido de FairPlay). Ejecute el siguiente comando para obtener la URL del token de licencia para el contenido de ejemplo:

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   Debe obtener una respuesta con la URL del token de licencia que tenga este aspecto:

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. Coloque la respuesta URL del token de licencia devuelta en el manifiesto M3U8 y *cambie el esquema de la URL del token de licencia a* `sdk://` desde `https://`. A continuación se muestra un ejemplo de la etiqueta #EXT-X-KEY en el manifiesto M3U8:

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES, 
   URI="skd://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g- 
   CR1rnJKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPx 
   N5qomYsnwYSSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw", 
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1"
   ```

   >[!NOTE]
   >
   >La información anterior se aplica sólo a la prueba de la configuración de FairPlay. Puede que no se aplique a la configuración de producción, dependiendo de cómo configure su gestor FairPlay. Consulte [Habilitar Apple FairPlay en aplicaciones iOS](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) para obtener más información.

Si se reproduce el vídeo, el contenido se empaqueta y se concede una licencia correcta. Si el vídeo no se reproduce, consulte la página de solución de problemas para encontrar soluciones a sus problemas.

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

Por ejemplo, esta es la parte de la interfaz de usuario del primer reproductor de prueba que se muestra arriba, donde se proporciona la información de licencia obtenida del servidor ExpressPlay:

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
