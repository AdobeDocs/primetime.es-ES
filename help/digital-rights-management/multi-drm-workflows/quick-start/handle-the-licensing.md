---
description: Las licencias son el mecanismo principal por el que se permite o se deniega a los usuarios la capacidad de reproducir un fragmento de contenido de vídeo protegido. A un usuario legítimo (autorizado) se le puede conceder una licencia (una clave) para descifrar y reproducir una parte específica del contenido cifrado de su proveedor de contenido.
title: Licencias
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# Licencias{#licensing}

Las licencias son el mecanismo principal por el que se permite o se deniega a los usuarios la capacidad de reproducir un fragmento de contenido de vídeo protegido. A un usuario legítimo (autorizado) se le puede conceder una licencia (una clave) para descifrar y reproducir una parte específica del contenido cifrado de su proveedor de contenido.

Antes de que la aplicación o página web del dispositivo de un usuario final pueda reproducir contenido protegido con DRM, debe adquirir un token de un servidor de autorizaciones o tiendas que usted, el cliente, gestione. Adobe proporciona un servidor de referencia de muestra para este fin: [Servidor de referencia: Servidor de derechos ExpressPlay de muestra (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

El servidor de autorizaciones o tiendas solicitará un token de licencia al servidor ExpressPlay correspondiente, solo después de comprobar con sus propios sistemas back-end si el usuario específico está autorizado a ver el contenido solicitado. La respuesta devuelta por la solicitud de token de licencia es una URL lista para usar para el servidor de licencias o la respuesta contiene la URL en una estructura JSON, según la solución DRM con la que esté trabajando.

>[!NOTE]
>
>La solicitud del token de licencia no se puede realizar desde el propio cliente:
>1. Los derechos deben comprobarse en un entorno de confianza; y
>1. El autenticador del cliente debe mantenerse en secreto.


1. Realice la solicitud del token de licencia.

   En el caso de un escenario de inicio rápido, en el que solo desea asegurarse de que los distintos componentes implicados están trabajando juntos, puede que desee utilizar algo como [!DNL curl] para realizar la solicitud del token de licencia (en lugar de obtener inicialmente una aplicación y ejecutar y probar llamadas desde allí). Por ejemplo:

   * Amplia:

   ```
   curl "https://wv-gen.test.expressplay.com/hms/wv/token?customerAuthenticator= 
   <Customer Authenticator> 
   &kid 
   <indexterm>
   CEKSID 
     <indexterm>
     as query parameter kid 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEKSID> 
      &contentKey 
    <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>WidevineToken 
   ```

   Token de prueba de Widevine de muestra:

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   Tenga en cuenta que la respuesta de Widevine es una cadena URL lista para usar.

   * PlayReady:

   ```
   curl "https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator= 
   <Customer Authenticator> 
      &kid 
   <indexterm>
   CEKSID 
   <indexterm>
   as query parameter kid 
   <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<Key ID> 
      &contentKey 
   <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>playreadyToken
   ```

   Token de prueba de PlayReady de muestra:

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   Tenga en cuenta que la respuesta PlayReady es un objeto JSON, con elementos de token y URL independientes.

   * FairPlay:

   ```
   curl "https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
    <Customer Authenticator> 
    &kid 
    <indexterm>
      CEKSID 
    <indexterm>
      as query parameter kid 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<Key ID> 
          &contentKey 
    <indexterm>
      CEK 
    <indexterm>
      as query parameter contentKey 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
    &iv=<IV ID> 
    &<Any additional licensing attributes desired>"
   ```

   Token de prueba de FairPlay de muestra:

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   Tenga en cuenta que la respuesta de FairPlay es una cadena URL lista para usar.
