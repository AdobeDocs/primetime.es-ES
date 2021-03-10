---
description: Los problemas comunes durante las pruebas suelen incluir los autenticadores de ExpressPlay, los protocolos de transporte y los parámetros de solicitud de servicio necesarios.
title: Solución de problemas de inicio rápido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# Solución de problemas del inicio rápido{#troubleshooting-your-quick-start}

Los problemas comunes durante las pruebas suelen incluir los autenticadores de ExpressPlay, los protocolos de transporte y los parámetros de solicitud de servicio necesarios.

Si sus [!DNL curl] solicitudes a ExpressPlay para la generación de tokens fallan, el cuerpo de la respuesta contendrá un mensaje de error que explica el motivo del error.

Si la generación de tokens se realiza correctamente, pero el contenido sigue sin reproducirse, compruebe los registros de canje de tokens de ExpressPlay para ver si hay errores como &quot;Token caducado&quot;.

Si la generación de tokens se ha realizado correctamente y el canje no ha producido ningún error, pero el vídeo aún no se reproduce, compruebe que el CEK coincida con el contenido y que el formato de contenido coincida con las capacidades del dispositivo de destino.

Además:

* Compruebe que está utilizando el autenticador del cliente correcto en sus solicitudes de servicio. Es fácil utilizar accidentalmente el autenticador de producción cuando pretendía utilizar el autenticador de prueba. Además, asegúrese de que está utilizando *su* autenticador. Por ejemplo, durante la prueba puede tomar prestado el comando `curl` de otra persona y olvidar intercambiar el autenticador por el suyo.

* Compruebe que está utilizando el protocolo de transporte adecuado en sus solicitudes o en sus manifiestos ( `https://` frente a `https://`, o en el caso de FairPlay, `skd://` frente a `https://` frente a `https://`.

* Asegúrese de incluir todos los parámetros de consulta necesarios para la solución DRM con la que está trabajando. Por ejemplo, es fácil confundirlo entre PlayReady y Widevine porque ambos trabajan con DASH, pero los parámetros de solicitud y las configuraciones de empaquetado requeridos son diferentes.
* Confirme que su cuenta de ExpressPlay tiene suficientes créditos de token y que no se ha agotado.
* Confirme que el triplete de datos DRM que se envían al TVSDK es correcto: Token ExpressPlay, URL del servidor de licencias y tipo DRM.
* Confirme que todos los componentes están asumiendo lo mismo sobre qué entorno de ExpressPlay se está utilizando que hay dos entornos, Test y Production.
* Tenga en cuenta que los distintos navegadores suelen admitir solo un DRM para el contenido DASH.
* A partir de TVSDK 2.4, solo se admite el perfil de empaquetado DASH-LIVE. (La compatibilidad con DASH-OnDemand está en la hoja de ruta).
* La compatibilidad con AndroidTV PlayReady es intermitente debido a las limitaciones del fabricante del dispositivo. Para dar ejemplos,

   * el dispositivo Razer Forge tiene problemas con el contenido PlayReady
   * Amazon FireTV no puede consumir contenido DASH con pista de audio cifrada

* A partir de TVSDK 2.4, solo los dispositivos AndroidTV admiten normalmente los DRM PlayReady y Widevine. El resto de dispositivos Android solo suelen admitir Widevine.
* A partir de TVSDK 2.4, Android TVSDK actualmente requiere que el cuadro PSSH esté en el manifiesto .mpd . Esto es contrario al estándar DASH, que especifica que el cuadro PSSH puede estar en cualquier parte, como en el propio contenido, y no solo en el .mpd.

