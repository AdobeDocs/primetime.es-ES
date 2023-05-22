---
title: Detalles del proceso de adquisición de licencia
description: Detalles del proceso de adquisición de licencia
copied-description: true
exl-id: d772339a-8d05-401b-b5c1-18169b3627b6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# Detalles del proceso de adquisición de licencia {#license-acquisition-process-details}

Este proceso presenta una vista detallada a nivel de API del flujo de trabajo de contenido protegido de Primetime DRM:

1. Uso de un `URLLoader` objeto, cargue los bytes del archivo de metadatos del contenido protegido.

   Establezca este objeto en una variable, como `metadata_bytes`. Todo el contenido controlado por DRM de Primetime tiene metadatos DRM de Primetime. Cuando el contenido se empaqueta, estos metadatos se pueden guardar como un archivo de metadatos independiente ( [!DNL .metadata]) junto con el contenido. Alternativamente, los metadatos pueden codificarse en Base64 e insertarse en el cuerpo del archivo de manifiesto de vídeo. Para obtener más información, consulte [Empaquetando archivos multimedia](../protecting-content/packaging-media-overview/packaging-media-files.md).
   1. Si es necesario, quite el signo de exclamación `!` desde el inicio de la cadena.
   1. Si es necesario para el contenido HLS o HDS, descodifique los metadatos incluidos en la cadena codificada en Base64 en datos binarios antes de pasarlos.
1. Crear un `DRMContentData` ejemplo.

   Coloque este código en un bloque try-catch:

   ```
   new DRMContentData(metadata_bytes)
   ```

   donde `metadata_bytes` es el `URLLoader` objeto obtenido en el paso 1.

   [iOS: metadatos DRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android: DTMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. Crear oyentes para escuchar `DRMStatusEvent` y `DRMErrorEvent` enviado desde el `DRMManager` objeto.

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   En el `DRMStatusEvent` oyente, compruebe que la licencia sea válida (no nula). En el `DRMErrorEvent` detector, identificador `DRMErrorEvents`. Consulte *Uso de la clase DRMStatusEvent* y *Uso de la clase DRMErrorEvent* en esta guía.

1. Cargue la licencia necesaria para reproducir el contenido.
En primer lugar, intente cargar una licencia almacenada localmente para reproducir el contenido:

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android: DRManager.acquisitionLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: acquisitionLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   Una vez finalizada la carga, la variable `DRMManager` distribuciones de objetos `DRMStatusEvent.DRM_Status`.

1. Compruebe la `DRMVoucher` objeto.


   Si la variable `DRMVoucher` el objeto no es nulo; la licencia es válida. Vaya al paso 9.

   [Android: DRMLicenseAcquiredCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS: DRMLicenseAcquired](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. Compruebe el método de autenticación requerido por la directiva para este contenido.

   Utilice el `DRMContentData.authenticationMethod` propiedad.
   1. Si el método de autenticación es `ANONYMOUS`, vaya al paso 9. 

      [Android: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. Si el método de autenticación es `USERNAME_AND_PASSWORD`Sin embargo, la aplicación debe proporcionar un mecanismo para permitir que el usuario introduzca las credenciales.

      Pase las credenciales del usuario al servidor de licencias para autenticar al usuario:

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      El `DRMManager` envía un `DRMAuthenticationErrorEvent` si la autenticación falla, o una `DRMAuthenticationCompleteEvent` si la autenticación se realiza correctamente. Cree oyentes para estos eventos.

      [Android: authenticate()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS: autenticar:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >El Adobe recomienda utilizar un mecanismo más seguro para proporcionar credenciales. Consulte la sección [KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html).

   1. Si el método de autenticación es `UNKNOWN`, debe utilizar un método de autenticación personalizado.

      En este caso, el proveedor de contenido ha organizado que la autenticación se realice de forma fuera de banda, no utilizando las API de Primetime. El procedimiento de autenticación personalizado debe producir un token de autenticación que se pueda pasar al `DRMManager.setAuthenticationToken()` método.

      [Android: setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[],%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS: setAuthenticationToken:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >Alternativamente, independientemente del método de autenticación, `.setAuthenticationToken()` se puede utilizar para enviar datos personalizados del cliente al servidor de licencias. Se trata de una sobrecarga de la API, ya que este mecanismo es la única manera de enviar datos personalizados dinámicos desde el cliente al servidor de licencias en el momento de la adquisición de la licencia. Este método de transporte de datos personalizados se analiza en profundidad en varias publicaciones del foro en la [Foros de DRM (acceso al Adobe) de Primetime ](https://forums.adobe.com/community/adobe_access).

1. Si la autenticación falla, la aplicación debe volver al paso 6.

   Asegúrese de que la aplicación tenga un mecanismo para gestionar y limitar los errores de autenticación repetidos. Por ejemplo, después de tres intentos, muestra un mensaje al usuario que indica que la autenticación ha fallado y que el contenido no se puede reproducir.
1. Para utilizar el token almacenado en lugar de pedir al usuario que introduzca las credenciales, establezca el token con la variable `DRMManager.setAuthenticationToken()` método.

   A continuación, descargue la licencia del servidor de licencias y reproduzca el contenido como en el paso 6.
   1. **Opcional:** Si la autenticación se realiza correctamente, puede capturar el token de autenticación, que es una matriz de bytes almacenada en caché en la memoria.

      Obtenga este token con el `DRMAuthenticationCompleteEvent.token` propiedad. Puede almacenar y utilizar el token de autenticación para que el usuario no tenga que introducir credenciales repetidamente para este contenido. El servidor de licencias determina el período válido del token de autenticación.

      [Android: OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS: DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. Si la autenticación se realiza correctamente, descargue la licencia del servidor de licencias:

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   Una vez finalizada la carga, la variable `DRMManager` distribuciones de objetos `DRMStatusEvent.DRM_STATUS`. Escuche este evento y, cuando se envíe, podrá reproducir el contenido.  Reproduzca el vídeo creando un objeto Primetime y llamando a su `play()` método:

   ```
   stream = new Primetime(connection); 
   stream.addEventListener(DRMStatusEvent.DRM _STATUS, drmStatusHandler); 
   stream.addEventListener(DRMErrorEvent.DRM_ERROR, drmErrorHandler); 
   stream.addEventListener(NetStatusEvent.NET_STATUS, netStatusHandler); 
   stream.client = new CustomClient(); 
   video.attachPrimetime(stream); 
   stream.play(videoURL);
   ```

   [Android: acquisitionLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: acquisitionLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)
