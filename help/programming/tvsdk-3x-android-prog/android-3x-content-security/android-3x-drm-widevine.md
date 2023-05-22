---
description: Puede utilizar las funciones del sistema de Digital Rights Management de Primetime (DRM) para proporcionar acceso seguro al contenido de vídeo. Como alternativa, puede utilizar soluciones de DRM de terceros como alternativa a la solución integrada de Adobe.
title: DRM de Widevine
exl-id: 44ab032e-e665-4b63-a08b-54e862894987
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# DRM de Widevine {#widevine-drm}

Puede utilizar las funciones del sistema de Digital Rights Management de Primetime (DRM) para proporcionar acceso seguro al contenido de vídeo. Como alternativa, puede utilizar soluciones de DRM de terceros como alternativa a la solución integrada de Adobe.

Póngase en contacto con su representante de Adobe para obtener la información más actualizada sobre la disponibilidad de soluciones de DRM de terceros.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

Puede utilizar la DRM nativa de Android Widevine con flujos HLS CMAF.

>[!NOTE]
>
> El esquema Widevine CENC CTR requiere una versión mínima de Android 4.4 (nivel de API 19).
>
> El esquema CBCS de Widevine requiere la versión mínima 7.1 de Android (nivel de API 25).

## Establecer detalles del servidor de licencias {#license-server-details}

Realice una llamada a lo siguiente `com.adobe.mediacore.drm.DRMManager` API antes de cargar el recurso de MediaPlayer:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### Argumentos {#arguments-license-server}

* `drm` - `"com.widevine.alpha"` para Widevine.

* `licenseServerURL` : URL del servidor de licencias de Widevine que recibe las solicitudes de licencia.

* `requestProperties` : contiene encabezados adicionales para incluirlos en la solicitud de licencia saliente.

Por ejemplo, cuando utilice contenido empaquetado para Expressplay DRM, utilice el siguiente código antes de reproducir:

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## Proporcionar devolución de llamada personalizada {#custom-callback}

Realice una llamada a lo siguiente `com.adobe.mediacore.drm.DRMManager` API antes de cargar el recurso de MediaPlayer.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### Argumentos {#arguments-custom-callback}

* `callback` : implementación personalizada de MediaDrmCallback para utilizar en lugar del predeterminado `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

Para obtener más información, consulte [Documentación de la API de Android TVSDK 3.11](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## Recuperar el cuadro PSSH del recurso MediaPlayer cargado actualmente {#pssh-box-mediaplayer-resoource}

Realice una llamada a lo siguiente `com.adobe.mediacore.drm.DRMManager` API, preferiblemente en la implementación de devolución de llamada personalizada.

```java
public static byte[] getPSSH()
```

La API devuelve el cuadro de encabezado específico del sistema de protección asociado al recurso de medios Widevine cargado.

Hay un cuadro válido disponible para una corta duración (entre la creación de instancias DRM y la carga de claves). `MediaDrmCallback callback executeKeyRequest()` Puede utilizarlo para personalizar la recuperación de claves de licencia.

>[!NOTE]
>
> `getPSSH()` La API solo es compatible con instancias de un solo reproductor. Múltiples reproductores o función Instant On deben inicializarse en serie para recibir la casilla correcta.
