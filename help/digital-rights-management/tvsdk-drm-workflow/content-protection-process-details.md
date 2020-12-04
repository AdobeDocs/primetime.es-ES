---
seo-title: Detalles del proceso de adquisición de licencias
title: Detalles del proceso de adquisición de licencias
uuid: 4825c49e-fa6f-4c98-9d21-a2743930ca2e
translation-type: tm+mt
source-git-commit: 3fdef12b717bb6f70ca27d9278de61d709f8349c
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# Detalles del proceso de adquisición de licencias {#license-acquisition-process-details}

Este proceso presenta una vista detallada a nivel de API del flujo de trabajo de contenido protegido de Primetime DRM:

1. Con un objeto `URLLoader`, cargue los bytes del archivo de metadatos del contenido protegido.

   Establezca este objeto en una variable, como `metadata_bytes`. Todo el contenido controlado por Primetime DRM tiene metadatos Primetime DRM. Cuando se empaqueta el contenido, estos metadatos se pueden guardar como un archivo de metadatos independiente ( [!DNL .metadata]) junto con el contenido. Como alternativa, los metadatos pueden codificarse en Base64 e insertarse en el cuerpo del archivo de manifiesto de vídeo. Para obtener más información, consulte [Empaquetado de archivos multimedia](../protecting-content/packaging-media-overview/packaging-media-files.md).
   1. Si es necesario, elimine el signo de exclamación `!` del inicio de la cadena.
   1. Si es necesario para contenido HLS o HDS, descodifique los metadatos incluidos en la cadena codificada en Base64 a datos binarios antes de pasarlos.
1. Cree una instancia `DRMContentData`.

   Coloque este código en un bloque try-catch:

   ```
   new DRMContentData(metadata_bytes)
   ```

   donde `metadata_bytes` es el objeto `URLLoader` obtenido en el paso 1.

   [iOS: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. Cree oyentes para escuchar los `DRMStatusEvent` y `DRMErrorEvent` enviados desde el objeto `DRMManager`.

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   En el detector `DRMStatusEvent`, compruebe que la licencia es válida (no es nula). En el detector `DRMErrorEvent`, gestione `DRMErrorEvents`. Consulte *Uso de la clase DRMStatusEvent* y *Uso de la clase DRMErrorEvent* en esta guía.

1. Cargue la licencia necesaria para reproducir el contenido.
En primer lugar, intente cargar una licencia almacenada localmente para reproducir el contenido:

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android: DRMManager.acquisitionLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: acquisitionLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   Una vez completada la carga, el objeto `DRMManager` distribuye `DRMStatusEvent.DRM_Status`.

1. Compruebe el objeto `DRMVoucher`.


   Si el objeto `DRMVoucher` no es nulo, la licencia es válida. Vaya al paso 9.

   [Android: DRMLicenseAcquiredCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS: DRMLicenseAcquired](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. Compruebe el método de autenticación requerido por la directiva para este contenido.

   Utilice la propiedad `DRMContentData.authenticationMethod`.
   1. Si el método de autenticación es `ANONYMOUS`, vaya al paso 9. 

      [Android: DRMAuthauthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS: DRMAuthauthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. Si el método de autenticación es `USERNAME_AND_PASSWORD`, la aplicación debe proporcionar un mecanismo para permitir que el usuario introduzca credenciales.

      Pase las credenciales del usuario al servidor de licencias para autenticar al usuario:

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      El `DRMManager` distribuye un `DRMAuthenticationErrorEvent` si falla la autenticación o un `DRMAuthenticationCompleteEvent` si la autenticación se realiza correctamente. Cree oyentes para estos eventos.

      [Android: authentication()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS: autenticar:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >Adobe recomienda utilizar un mecanismo más seguro para proporcionar credenciales. Para obtener referencia, consulte [KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html).

   1. Si el método de autenticación es `UNKNOWN`, debe utilizar un método de autenticación personalizado.

      En este caso, el proveedor de contenido ha dispuesto que la autenticación se realice de forma fuera de banda, no utilizando las API de Primetime. El procedimiento de autenticación personalizada debe producir un token de autenticación que se pueda pasar al método `DRMManager.setAuthenticationToken()`.

      [Android: setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[],%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS: setAuthenticationToken:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >Como alternativa, independientemente del método de autenticación, `.setAuthenticationToken()` puede utilizarse para enviar datos personalizados del cliente al servidor de licencias. Se trata de una sobrecarga de la API, ya que este mecanismo es la única manera de enviar datos personalizados dinámicos del cliente al servidor de licencias en el momento de la adquisición de la licencia. Este método de transporte de datos personalizado se analiza en profundidad en varias publicaciones de foros en los foros [Primetime DRM (Adobe Access) ](https://forums.adobe.com/community/adobe_access).

1. Si falla la autenticación, la aplicación debe volver al paso 6.

   Asegúrese de que la aplicación tenga un mecanismo para gestionar y limitar los errores de autenticación repetidos. Por ejemplo, después de tres intentos, se muestra un mensaje al usuario indicando que la autenticación ha fallado y que no se puede reproducir el contenido.
1. Para utilizar el token almacenado en lugar de solicitar al usuario que introduzca credenciales, configure el token con el método `DRMManager.setAuthenticationToken()`.

   A continuación, descargue la licencia del servidor de licencias y reproduzca el contenido como se muestra en el paso 6.
   1. **Opcional:** Si la autenticación se realiza correctamente, puede capturar el autentificador, que es una matriz de bytes almacenada en la memoria caché.

      Obtenga este token con la propiedad `DRMAuthenticationCompleteEvent.token`. Puede almacenar y utilizar el autentificador para que el usuario no tenga que introducir repetidamente credenciales para este contenido. El servidor de licencias determina el período válido del autentificador.

      [Android: OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS: DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. Si la autenticación se realiza correctamente, descargue la licencia del servidor de licencias:

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   Una vez completada la carga, el objeto `DRMManager` distribuye `DRMStatusEvent.DRM_STATUS`. Escuche este evento y cuando se envíe, podrá reproducir el contenido.  Reproduzca el vídeo creando un objeto Primetime y llamando a su método `play()`:

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