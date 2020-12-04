---
description: Puede utilizar las funciones del sistema Primetime Digital Rights Management (DRM) para proporcionar un acceso seguro al contenido del vídeo. Como alternativa, puede utilizar soluciones DRM de terceros como alternativa a la solución integrada de Adobe.
seo-description: Puede utilizar las funciones del sistema Primetime Digital Rights Management (DRM) para proporcionar un acceso seguro al contenido del vídeo. Como alternativa, puede utilizar soluciones DRM de terceros como alternativa a la solución integrada de Adobe.
seo-title: DRM amplio
title: DRM amplio
uuid: 3a5fd786-4319-4e92-83b6-0f5328df6a44
translation-type: tm+mt
source-git-commit: 0271af21b74e80455ddb2c53571cd75f3a0f56ba
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# DRM {#widevine-drm} Widevine

Puede utilizar las funciones del sistema Primetime Digital Rights Management (DRM) para proporcionar un acceso seguro al contenido del vídeo. Como alternativa, puede utilizar soluciones DRM de terceros como alternativa a la solución integrada de Adobe.

Póngase en contacto con su representante de Adobe para obtener la información más actualizada sobre la disponibilidad de soluciones DRM de terceros.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

Puede utilizar la DRM nativa de Android Widevine con flujos CMAF HLS.

>[!NOTE]
>
> El esquema CTR de Widevine CENC requiere la versión mínima de Android 4.4 (Nivel de API 19).
>
> El esquema amplio de CBCS requiere la versión mínima de Android 7.1 (nivel de API 25).

## Definir detalles del servidor de licencias {#license-server-details}

Llame a la siguiente API `com.adobe.mediacore.drm.DRMManager` antes de cargar el recurso de MediaPlayer:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### Argumentos {#arguments-license-server}

* `drm` -  `"com.widevine.alpha"` para Widevine.

* `licenseServerURL` - Dirección URL del servidor de licencias Widevine que recibe solicitudes de licencia.

* `requestProperties` - Contiene encabezados adicionales para incluirlos en la solicitud de licencia saliente.

Por ejemplo, al usar contenido empaquetado para Expresiones DRM, utilice el siguiente código antes de reproducir:

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## Proporcionar llamada de retorno personalizada {#custom-callback}

Llame a la siguiente API `com.adobe.mediacore.drm.DRMManager` antes de cargar el recurso de MediaPlayer.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### Argumentos {#arguments-custom-callback}

* `callback` - implementación personalizada de MediaDrmCallback para usar en lugar de usar el valor predeterminado  `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

Para obtener más información, consulte la [documentación de la API de Android TVSDK 3.11](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## Buscar el cuadro PSSH del recurso de MediaPlayer cargado {#pssh-box-mediaplayer-resoource}

Llame a la siguiente API `com.adobe.mediacore.drm.DRMManager`, preferiblemente en la implementación de llamada de retorno personalizada.

```java
public static byte[] getPSSH()
```

La API devuelve el Cuadro de encabezado específico del sistema de protección asociado al recurso de medios Widevine cargado.

Hay un cuadro válido disponible para una duración corta (entre la creación de instancias de DRM y la carga de claves). `MediaDrmCallback callback executeKeyRequest()` Puede utilizarla para personalizar la recuperación de claves de licencia.

>[!NOTE]
>
> `getPSSH()` La API solo se admite en instancias de un solo reproductor. Varios reproductores o la función Instant On deben inicializarse en serie para recibir el cuadro correcto.
