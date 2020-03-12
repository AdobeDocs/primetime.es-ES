---
description: Utilizamos el empaquetador Bento4 y el empaquetador sin conexión de Adobe para crear contenido DASH cifrado. Bento4 toma como entrada contenido mp4 sin cifrar.
seo-description: Utilizamos el empaquetador Bento4 y el empaquetador sin conexión de Adobe para crear contenido DASH cifrado. Bento4 toma como entrada contenido mp4 sin cifrar.
seo-title: Empaquete su contenido con Bento4
title: Empaquete su contenido con Bento4
uuid: 88323a4e-d0b5-4a41-acec-7126d3e0c90b
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Contenido del paquete para Widevine y PlayReady {#package-for-widevine}

Utilizamos el empaquetador Bento4 y el empaquetador sin conexión de Adobe para crear contenido DASH cifrado. Bento4 toma como entrada contenido mp4 sin cifrar.

## Empaquete su contenido con Bento4{#package-your-content-with-bento}

El empaquetador Bento4 espera que la entrada mp4 esté prefragmentada. La distribución del envasador Bento4 incluye una herramienta para esto.

**Llamando a Bento4**

Las invocaciones típicas del empaquetador Bento4 serían como los ejemplos siguientes:

    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtítulos
    —encrypad-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc 0747c7c5ac215b3b
    —widevine
    —widevine-header=provider:intertrust#content_id:2a &quot;CC_300_640x360.mp4&quot;
    -o &quot;CC_300_640x360_DASM H&quot;
>
    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtítulos
    —encrypad-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc 0747c7c5ac215b3b
    —playready
    —playready-header=\&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;

El ejemplo siguiente combina esquemas PlayReady y Widevine. En este caso concreto, el empaquetador está agregando los datos de inicialización de protección de contenido Widevine y de protección de contenido PlayReady al contenido DASH de salida.

    /mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtítulos
    —encrypad-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc 0747c7c5ac215b3b
    —playready
    —playready-header=\&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;
    —widevine
    —widevine-header=provider:intertrust#content_id:2a &quot;CC_300_640x360.mp4&quot;
    
    
    -o &quot;CC 300_640x360_DASH&quot;donde

El valor del `--encryption-key` indicador está en el formulario `<base16 encoded key id>:<base16 encoded encryption key>`.

El `--widevine-header=provider:intertrust#content_id:2a` indicador indica al empaquetador que incluya el cuadro pssh en el manifiesto, que TVSDK requiere actualmente para la reproducción.
El valor para `-playready-header` es para la adquisición de licencias PlayReady.

## Empaquete su contenido con Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager toma como entrada contenido mp4 sin cifrar.

**Llamada a Adobe Offline Packager**

Una invocación típica de adobe offline Packager tendría el aspecto de la llamada siguiente:

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7ecf33 1a8ebf1b7ddda5
    -widevine_provider intertrust
    -playready_LA_
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7dda5
    -content_id c595f214f d84dc7ecf31a8ebf1b7ddda5

En este caso concreto, el empaquetador sin conexión está agregando los datos de inicialización de protección de contenido Widevine y de protección de contenido PlayReady al contenido DASH de salida. El valor de `-key_file_path` es para una clave codificada en base64. El valor de `-playready_LA_URL` es para la adquisición de licencias PlayReady.

El argumento conf_path apunta al archivo de configuración que contendría lo siguiente:

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

Porque ciertos dispositivos Android — principalmente Amazon Fire TV — no admite el descifrado de audio, el cifrado de audio es opcional.