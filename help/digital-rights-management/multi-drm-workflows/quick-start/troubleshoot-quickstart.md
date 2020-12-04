---
description: Los problemas comunes durante las pruebas suelen incluir los autenticadores de ExpressPlay, los protocolos de transporte y los parámetros de solicitud de servicio requeridos.
seo-description: Los problemas comunes durante las pruebas suelen incluir los autenticadores de ExpressPlay, los protocolos de transporte y los parámetros de solicitud de servicio requeridos.
seo-title: Solución de problemas del inicio rápido
title: Solución de problemas del inicio rápido
uuid: 42256aa0-2efc-4602-aefc-3bab2dc58ec0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# Solución de problemas del inicio rápido{#troubleshooting-your-quick-start}

Los problemas comunes durante las pruebas suelen incluir los autenticadores de ExpressPlay, los protocolos de transporte y los parámetros de solicitud de servicio requeridos.

Si fallan las solicitudes [!DNL curl] a ExpressPlay para la generación de tokens, el cuerpo de la respuesta contendrá un mensaje de error que explica el motivo del error.

Si la generación de tokens se realiza correctamente, pero el contenido aún no se reproduce, compruebe los registros de canje de tokens de ExpressPlay en busca de errores como &quot;token caducado&quot;.

Si la generación del token se realizó correctamente y el canje no tuvo errores, pero el vídeo aún no se reproduce, compruebe que el CEK coincide con el contenido y que el formato del contenido coincide con las capacidades del dispositivo destinatario.

Además:

* Compruebe que está utilizando el autenticador de cliente correcto en las solicitudes de servicio. Es fácil utilizar accidentalmente el autenticador de producción cuando se pretendía utilizar el autenticador de prueba. Además, asegúrese de que está utilizando *el autenticador*. Por ejemplo: durante la prueba, puede tomar prestado el comando `curl` de otra persona y olvidarse de intercambiar su autenticador por el suyo.

* Compruebe que está utilizando el protocolo de transporte adecuado en sus solicitudes o en los manifiestos ( `https://` frente a `https://`, o en el caso de FairPlay, `skd://` frente a `https://` frente a `https://`.

* Asegúrese de incluir todos los parámetros de consulta necesarios para la solución DRM con la que está trabajando. Es fácil confundirse entre PlayReady y Widevine, por ejemplo, porque ambos trabajan con DASH, pero los parámetros de solicitud y las configuraciones de empaquetado requeridos son diferentes.
* Confirme que su cuenta de ExpressPlay tiene suficientes créditos de token y no se ha agotado.
* Confirme que el triplete de datos DRM que se envían al TVSDK es correcto: Distintivo ExpressPlay, URL del servidor de licencias y tipo DRM.
* Confirme que todos los componentes están asumiendo lo mismo sobre qué entorno ExpressPlay se está utilizando que hay dos entornos: Prueba y Producción.
* Tenga en cuenta que los distintos navegadores suelen admitir solo un DRM para el contenido DASH.
* A partir de TVSDK 2.4, solo se admite el perfil de empaquetado DASH-LIVE. (La compatibilidad con DASH-OnDemand está en la hoja de ruta).
* La compatibilidad con AndroidTV PlayReady es intermitente debido a las limitaciones del fabricante del dispositivo. Para dar ejemplos,

   * el dispositivo Razer Forge tiene problemas con el contenido de PlayReady
   * Amazon FireTV no puede consumir contenido DASH que tenga cifrada la pista de audio

* A partir de TVSDK 2.4, solo los dispositivos AndroidTV suelen ser compatibles con los DRM de PlayReady y Widevine. El resto de dispositivos Android solo suelen ser compatibles con Widevine.
* A partir de TVSDK 2.4, el Android TVSDK requiere actualmente que el cuadro PSSH esté en el manifiesto .mpd. Esto es contrario al estándar DASH, que especifica que el cuadro PSSH puede estar en cualquier parte, como en el propio contenido, y no solo en el archivo .mpd.

