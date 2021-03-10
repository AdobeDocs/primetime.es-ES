---
description: Puede utilizar las funciones del sistema de Digital Rights Management Primetime (DRM) para proporcionar acceso seguro al contenido de vídeo. Como alternativa, puede utilizar soluciones DRM de terceros como una alternativa a la solución integrada de Adobe.
title: DRM Widevine
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# DRM {#widevine-drm} Widevine

Puede utilizar las funciones del sistema de Digital Rights Management Primetime (DRM) para proporcionar acceso seguro al contenido de vídeo. Como alternativa, puede utilizar soluciones DRM de terceros como una alternativa a la solución integrada de Adobe.

Póngase en contacto con su representante de Adobe para obtener la información más actualizada sobre la disponibilidad de soluciones DRM de terceros.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

Puede utilizar el DRM nativo de Android Widevine con flujos HLS CMAF.

>[!NOTE]
>
> El esquema Widevine CENC CTR requiere una versión mínima de Android 4.4 (nivel 19 de la API).
>
> El esquema Widevine CBCS requiere una versión mínima de Android 7.1 (nivel de API 25).

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

* `licenseServerURL` - La URL del servidor de licencias Widevine que recibe solicitudes de licencia.

* `requestProperties` - Contiene encabezados adicionales para incluirlos en la solicitud de licencia saliente.

Por ejemplo, cuando utilice contenido empaquetado para Expressplay DRM, utilice el siguiente código antes de reproducir:

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## Proporcionar una devolución de llamada personalizada {#custom-callback}

Llame a la siguiente API `com.adobe.mediacore.drm.DRMManager` antes de cargar el recurso de MediaPlayer.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### Argumentos {#arguments-custom-callback}

* `callback` : implementación personalizada de MediaDrmCallback para usar en lugar del  `com.adobe.mediacore.drm.WidevineMediaDrmCallback` predeterminado.

Para obtener más información, consulte [Documentación de la API de Android TVSDK 3.11](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## Recuperación del cuadro PSSH del recurso de MediaPlayer cargado actualmente {#pssh-box-mediaplayer-resoource}

Llame a la siguiente API `com.adobe.mediacore.drm.DRMManager`, preferiblemente en la implementación de rellamada personalizada.

```java
public static byte[] getPSSH()
```

La API devuelve el Cuadro de encabezado específico del sistema de protección asociado al recurso de medios Widevine cargado.

Hay disponible un cuadro válido para una duración corta (entre la creación de instancias DRM y la carga de claves). `MediaDrmCallback callback executeKeyRequest()` puede utilizarla para personalizar la recuperación de claves de licencia.

>[!NOTE]
>
> `getPSSH()` La API solo es compatible con instancias de reproductor único. Varios reproductores o la función Instant On se deben inicializar en serie para recibir el cuadro correcto.
