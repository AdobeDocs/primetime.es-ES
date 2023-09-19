---
description: Las licencias son el mecanismo principal por el cual a los usuarios se les permite o deniega la capacidad de reproducir un fragmento de contenido de vídeo protegido. Un usuario legítimo (con derecho a acceso) puede recibir una licencia (una clave) para descifrar y reproducir una parte específica del contenido cifrado de su proveedor de contenido.
title: Licencias
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Licencias{#licensing}

Las licencias son el mecanismo principal por el cual a los usuarios se les permite o deniega la capacidad de reproducir un fragmento de contenido de vídeo protegido. Un usuario legítimo (con derecho a acceso) puede recibir una licencia (una clave) para descifrar y reproducir una parte específica del contenido cifrado de su proveedor de contenido.

Para que la aplicación o la página web del dispositivo de un usuario final pueda reproducir contenido protegido por DRM, debe adquirir un token de un servidor de derechos o de tiendas que usted, el cliente, utilice. Adobe proporciona un servidor de referencia de ejemplo para este fin: [Servidor de referencia: Servidor de derechos de ExpressPlay de muestra (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

Su servidor de derechos o tienda solicitará un token de licencia al servidor ExpressPlay correspondiente, solo después de consultar con sus propios sistemas back-end para determinar si el usuario específico tiene derecho a ver el contenido solicitado. La respuesta devuelta por la solicitud de token de licencia es una URL lista para usar para el servidor de licencias o la respuesta contiene la URL en una estructura JSON, según la solución DRM con la que esté trabajando.

>[!NOTE]
>
>La solicitud de token de licencia no se puede realizar desde el propio cliente:
>1. Los derechos deben comprobarse en un entorno de confianza; y
>1. El autenticador del cliente debe mantenerse en secreto.

1. Realice la solicitud del token de licencia.

   Para un escenario de inicio rápido, en el que solo desea asegurarse de que los distintos componentes implicados funcionan juntos, es posible que desee utilizar algo como [!DNL curl] para realizar la solicitud del token de licencia (en lugar de poner en marcha inicialmente una aplicación y probar las llamadas desde allí). Por ejemplo:

   * Widevine:

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

   Ejemplo de token de prueba de Widevine:

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   Tenga en cuenta que la respuesta de Widevine es una cadena de URL &quot;lista para usar&quot;.

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

   Token de prueba PlayReady de muestra:

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   Tenga en cuenta que la respuesta de PlayReady es un objeto JSON, con elementos URL y token independientes.

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

   Muestra de token de prueba de FairPlay:

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   Tenga en cuenta que la respuesta de FairPlay es una cadena de URL &quot;lista para usar&quot;.
