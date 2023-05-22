---
description: Los problemas comunes durante las pruebas suelen involucrar a los autenticadores de ExpressPlay, protocolos de transporte y parámetros de solicitud de servicio requeridos.
title: Solución de problemas de inicio rápido
exl-id: d8908f9c-98f4-4100-a003-d3b990105dee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Solución de problemas de inicio rápido{#troubleshooting-your-quick-start}

Los problemas comunes durante las pruebas suelen involucrar a los autenticadores de ExpressPlay, protocolos de transporte y parámetros de solicitud de servicio requeridos.

Si su [!DNL curl] Las solicitudes a ExpressPlay para la generación de tokens fallan, el cuerpo de respuesta contendrá un mensaje de error que explica el motivo del error.

Si la generación del token se realiza correctamente, pero el contenido sigue sin reproducirse, compruebe en los registros de canje del token de ExpressPlay si hay errores como &quot;Token caducado&quot;.

Si la generación del token se ha realizado correctamente y el canje no ha producido ningún error, pero el vídeo sigue sin reproducirse, compruebe que el CEK coincida con el contenido y que el formato del contenido coincida con las capacidades del dispositivo de destino.

Además:

* Compruebe que está utilizando el autenticador de cliente correcto en sus solicitudes de servicio. Es fácil utilizar accidentalmente el autenticador de producción cuando pretendía utilizar el autenticador de prueba. Además, asegúrese de que está utilizando *su* autenticador. Por ejemplo, durante las pruebas, puede tomar prestado el de otra persona `curl` y olvide cambiar el autenticador por el suyo.

* Compruebe que está utilizando el protocolo de transporte adecuado en sus solicitudes o manifiestos ( `https://` frente `https://`, o en el caso de FairPlay, `skd://` frente `https://` frente `https://`.

* Asegúrese de incluir todos los parámetros de consulta necesarios para la solución DRM con la que está trabajando. Por ejemplo, es fácil confundir entre PlayReady y Widevine, porque ambos funcionan con DASH, pero los parámetros de solicitud y las configuraciones de empaquetado requeridos son diferentes.
* Confirme que su cuenta de ExpressPlay tiene suficientes créditos de token y que no se ha agotado.
* Confirme que el triplete de datos DRM que se envía al TVSDK es correcto: token de ExpressPlay, URL del servidor de licencias y tipo de DRM.
* Confirme que todos los componentes asumen lo mismo sobre el entorno ExpressPlay que está en uso, ya que hay dos entornos, Prueba y Producción.
* Tenga en cuenta que los distintos exploradores generalmente solo admiten un DRM para el contenido DASH.
* A partir de TVSDK 2.4, solo se admite el perfil de empaquetado DASH-LIVE. (La asistencia de DASH-OnDemand está en la hoja de ruta).
* La compatibilidad con AndroidTV PlayReady es intermitente debido a las limitaciones del fabricante del dispositivo. Para dar ejemplos,

   * el dispositivo Razer Forge tiene problemas con el contenido PlayReady
   * Amazon FireTV no puede consumir contenido de DASH que tenga cifrada la pista de audio

* A partir de TVSDK 2.4, solo los dispositivos Android TV suelen admitir DRM PlayReady y Widevine. El resto de dispositivos Android solo suelen admitir Widevine.
* A partir de TVSDK 2.4, TVSDK para Android actualmente requiere que el cuadro PSSH esté en el manifiesto .mpd. Esto es contrario al estándar DASH, que especifica que el cuadro PSSH puede estar en cualquier lugar, como en el propio contenido, y no solo en el .mpd.
