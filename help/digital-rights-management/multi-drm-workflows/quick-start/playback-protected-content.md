---
description: Para probar la solución DRM, necesita una aplicación de vídeo que pueda procesar la solución DRM concreta con la que está trabajando. Este reproductor puede ser un reproductor de muestras disponible mediante Adobe o una aplicación de vídeo propia basada en TVSDK.
title: Reproducción del contenido protegido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Reproducción del contenido protegido {#playback-your-protected-content}

Para probar la solución DRM, necesita una aplicación de vídeo que pueda procesar la solución DRM concreta con la que está trabajando. Este reproductor puede ser un reproductor de muestras disponible mediante Adobe o una aplicación de vídeo propia basada en TVSDK.

1. Utilice la URL del servidor de licencias de la respuesta de token que obtuvo del servidor ExpressPlay para probar si puede reproducir el contenido protegido.

   * **Widevine** - Utilice la respuesta de Widevine directamente como recibida desde su solicitud de token de licencia de ExpressPlay.
   * **PlayReady** : obtenga la URL y el token del servidor de licencias del objeto JSON devuelto desde su solicitud de token de licencia.
   * **FairPlay** - Utilice la respuesta de FairPlay directamente como recibida desde su solicitud de token de licencia de ExpressPlay.

1. Pruebe la reproducción del contenido protegido con su propio reproductor o con un reproductor de muestras de Adobe existente.

   Proporcione la URL al contenido protegido (la ubicación del manifiesto M3U8 o MPD, según la solución DRM que esté probando).

   Según la interfaz proporcionada por el reproductor con el que realice la prueba, se le puede pedir que proporcione la URL de licencia y el token por separado como cadenas en campos de entrada, o como un objeto JSON pegado en un cuadro de texto o quizás como un parámetro de consulta en la URL.

   Aquí se enumeran algunas posibilidades para los reproductores de prueba:

   * Reproductor de referencia de HTML 5:

     ```
     https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
     ```

   * Reproductor de Shaka:

     ```
     https://shaka-player-demo.appspot.com
     ```

   * Reproductor de TVSDK de muestra (en desarrollo):

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **Comprobación de la reproducción al probar la configuración de FairPlay:** FairPlay requiere algunos pasos adicionales para reproducir contenido cuando se utilizan los servidores de licencias ExpressPlay. Si está utilizando [!DNL curl] para probar las conexiones (como se describe en [Licencias](../../multi-drm-workflows/quick-start/handle-the-licensing.md)), debe hacer lo siguiente *editar el manifiesto M3U8* (su contenido empaquetado) de la siguiente manera:

1. Agregue la respuesta que obtuvo de su solicitud de token de licencia a `#EXT-X-KEY:` etiqueta en el manifiesto, y
1. Cambie el protocolo de esa dirección URL desde la respuesta (ahora en el manifiesto), desde `https://` hasta `skd://`.

   Aquí tiene un ejemplo completo de cómo probar la reproducción con FairPlay, incluido el paso de licencia:

1. Utilice la solicitud de token de licencia de FairPlay para obtener la URL de su token de licencia. (Utilice su propio autenticador de cliente de producción, y asegúrese de utilizar la misma CEK y `iv` que se utilizó para empaquetar el contenido de FairPlay). Ejecute el siguiente comando para obtener la URL del token de licencia para el contenido de ejemplo:

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   Debe recibir una respuesta con la URL del token de licencia que tenga este aspecto:

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. Coloque la respuesta URL del token de licencia devuelto en el manifiesto M3U8, y *cambiar el esquema de la URL del token de licencia a* `sdk://` de `https://`. A continuación se muestra un ejemplo de la etiqueta #EXT-X-KEY del manifiesto M3U8:

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
   >La información anterior se aplica solo a la prueba de su configuración de FairPlay. Es posible que no se aplique a su configuración de producción, dependiendo de cómo configure su controlador FairPlay. Consulte [Habilitar Apple FairPlay en aplicaciones de iOS](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) para obtener más información.

Si se reproduce el vídeo, ha empaquetado y autorizado correctamente el contenido. Si el vídeo no se reproduce, consulte la página de solución de problemas para ver algunas posibles soluciones a los problemas.

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

Por ejemplo, esta es la parte de la interfaz de usuario del primer reproductor de prueba mencionado anteriormente, donde proporciona la información de licencias obtenida del servidor ExpressPlay:

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
