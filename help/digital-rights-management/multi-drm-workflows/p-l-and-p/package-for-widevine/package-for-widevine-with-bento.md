---
description: Utilizamos tanto el empaquetador Bento4 como el empaquetador sin conexión de Adobe para crear contenido DASH cifrado. Bento4 toma como entrada contenido mp4 no cifrado.
title: Empaquete su contenido con Bento4
exl-id: c873eaf6-c738-4f95-a900-a8aecb03754d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Empaquetando contenido para Widevine y PlayReady {#package-for-widevine}

Utilizamos tanto el empaquetador Bento4 como el empaquetador sin conexión de Adobe para crear contenido DASH cifrado. Bento4 toma como entrada contenido mp4 no cifrado.

## Empaquete su contenido con Bento4{#package-your-content-with-bento}

El empaquetador Bento4 espera que el mp4 de entrada esté prefragmentado. La distribución Bento4 Packager incluye una herramienta para esto.

**Llamando a Bento4**

Las invocaciones típicas del empaquetador Bento4 tendrían el aspecto de los ejemplos siguientes:

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

El ejemplo siguiente combina los esquemas PlayReady y Widevine. En este caso particular, el empaquetador agrega los datos de inicialización de protección de contenido Widevine y de protección de contenido PlayReady al contenido DASH de salida.

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

El valor de `--encryption-key` el indicador está en el formulario `<base16 encoded key id>:<base16 encoded encryption key>`.

El `--widevine-header=provider:intertrust#content_id:2a` El indicador indica al empaquetador que incluya el cuadro pssh en el manifiesto, que TVSDK requiere actualmente para la reproducción.

El valor de `-playready-header` es para la adquisición de licencias PlayReady.

## Empaquetar el contenido con Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

El empaquetador sin conexión de Adobe toma como entrada contenido mp4 sin cifrar.

**Llamando al empaquetador sin conexión de Adobe**

Una invocación típica del empaquetador sin conexión de Adobe tendría el siguiente aspecto:

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

En este caso particular, el empaquetador sin conexión agrega los datos de inicialización de la protección de contenido Widevine y de la protección de contenido PlayReady al contenido DASH de salida. El valor de `-key_file_path` es para una clave codificada en base64. El valor de `-playready_LA_URL` es para la adquisición de licencias PlayReady.

El argumento conf_path apunta al archivo de configuración que contendría lo siguiente:

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

Debido a que algunos dispositivos Android, principalmente Amazon Fire TV, no admiten el descifrado de audio, el cifrado de audio es opcional.
