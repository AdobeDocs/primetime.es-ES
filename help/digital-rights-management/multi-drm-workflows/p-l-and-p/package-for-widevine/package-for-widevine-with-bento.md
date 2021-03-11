---
description: Utilizamos el empaquetador Bento4 y el empaquetador sin conexión de Adobe para crear contenido DASH cifrado. Bento4 toma como entrada contenido mp4 sin encriptar.
title: Empaquete su contenido con Bento4
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Contenido de paquetes para Widevine y PlayReady {#package-for-widevine}

Utilizamos el empaquetador Bento4 y el empaquetador sin conexión de Adobe para crear contenido DASH cifrado. Bento4 toma como entrada contenido mp4 sin encriptar.

## Empaquete su contenido con Bento4{#package-your-content-with-bento}

El empaquetador Bento4 espera que el mp4 de entrada se prefragmente. La distribución del paquete Bento4 incluye una herramienta para esto.

**Llamada a Bento4**

Las invocaciones típicas del empaquetador Bento4 tendrían el aspecto siguiente:

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
```

El ejemplo siguiente combina esquemas PlayReady y Widevine. En este caso concreto, el empaquetador agrega tanto la protección de contenido Widevine como los datos de inicialización de protección de contenido PlayReady al contenido DASH de salida.

```
/mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

donde

El valor del indicador `--encryption-key` tiene el formato `<base16 encoded key id>:<base16 encoded encryption key>`.

El indicador `--widevine-header=provider:intertrust#content_id:2a` indica al empaquetador que incluya el cuadro pssh en el manifiesto, que TVSDK requiere actualmente para la reproducción.

El valor de `-playready-header` es para la adquisición de licencias PlayReady.

## Empaquete el contenido con Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

Adobe de paquetes sin conexión toma como entrada contenido mp4 sin encriptar.

**Llamada a Adobe Offline Packager**

Una invocación típica de adobe offline packager sería como la llamada a continuación:

```
java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path "Jaigo.mp4"
-out_path "Jaigo_DASH"
-key_file_path "Jaigo_DASH/_info/key.B64.random"
-widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
-widevine_provider intertrust
-playready_LA_URL
http://pr.test.expressplay.com/playready/RightsManager.asmx
-playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
-content_id c595f214d84dc7ecf31a8ebf1b7ddda5
```

En este caso concreto, el empaquetador sin conexión agrega tanto la protección de contenido Widevine como los datos de inicialización de protección de contenido PlayReady al contenido DASH de salida. El valor de `-key_file_path` es para una clave codificada base64. El valor de `-playready_LA_URL` es para la adquisición de licencias PlayReady.

El argumento conf_path apunta al archivo de configuración que contendría lo siguiente:

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

Como algunos dispositivos Android, principalmente Amazon Fire TV, no admiten el descifrado de audio, el cifrado de audio es opcional.
