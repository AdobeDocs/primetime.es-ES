---
description: La licencia es el mecanismo principal mediante el cual se permite o se deniega a los usuarios la capacidad de reproducir un fragmento de contenido de vídeo protegido. A un usuario legítimo (autorizado) se le puede otorgar una licencia (una clave) para descifrar y reproducir un fragmento específico del contenido cifrado de su proveedor de contenido.
seo-description: La licencia es el mecanismo principal mediante el cual se permite o se deniega a los usuarios la capacidad de reproducir un fragmento de contenido de vídeo protegido. A un usuario legítimo (autorizado) se le puede otorgar una licencia (una clave) para descifrar y reproducir un fragmento específico del contenido cifrado de su proveedor de contenido.
seo-title: Licencias
title: Licencias
uuid: 9f433d62-5609-4d88-95fd-c1e7c0f6aa75
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---


# Licencias{#licensing}

La licencia es el mecanismo principal mediante el cual se permite o se deniega a los usuarios la capacidad de reproducir un fragmento de contenido de vídeo protegido. A un usuario legítimo (autorizado) se le puede otorgar una licencia (una clave) para descifrar y reproducir un fragmento específico del contenido cifrado de su proveedor de contenido.

Antes de que la aplicación o la página web de un usuario final pueda reproducir contenido protegido con DRM, debe adquirir un token de un servidor de asignación de derechos o de tienda que usted, el cliente, utilice. Adobe proporciona un servidor de referencia de muestra para este fin: [Servidor de referencia: Ejemplo de ExpressPlay Entitlement Server (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

El servidor de asignación de derechos o de tienda solicitará un token de licencia del servidor ExpressPlay correspondiente, solo después de comprobar con sus propios sistemas back-end si el usuario específico tiene derecho a ver el contenido solicitado. La respuesta devuelta por la solicitud de token de licencia es una URL lista para usar para el servidor de licencias o bien la respuesta contiene la URL en una estructura JSON, según la solución DRM con la que esté trabajando.

>[!NOTE]
>
>La solicitud del token de licencia no se puede realizar desde el propio cliente:
>1. Los derechos deben comprobarse en un entorno de confianza; y
>1. El autenticador del cliente debe mantenerse en secreto.


1. Realice la solicitud del token de licencia.

   En un caso de inicio rápido, en el que solo desea asegurarse de que los distintos componentes implicados funcionan en conjunto, puede que desee utilizar algo como [!DNL curl] hacer su solicitud de token de licencia (en lugar de obtener inicialmente una aplicación y ejecutarla y probar las llamadas desde allí). Por ejemplo:

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

   Testigo de prueba de Widevine de muestra:

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   Tenga en cuenta que la respuesta de Widevine es una cadena URL &quot;lista para usar&quot;.

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

   Muestra del token de prueba de PlayReady:

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   Tenga en cuenta que la respuesta de PlayReady es un objeto JSON, con elementos de token y URL independientes.

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

   Muestra del token de prueba de FairPlay:

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   Tenga en cuenta que la respuesta de FairPlay es una cadena URL &quot;lista para usar&quot;.
