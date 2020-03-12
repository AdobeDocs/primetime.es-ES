---
description: Adobe Offline Packager toma como entrada contenido mp4 sin cifrar.
seo-description: Adobe Offline Packager toma como entrada contenido mp4 sin cifrar.
seo-title: Empaquete su contenido con Adobe Offline Packager
title: Empaquete su contenido con Adobe Offline Packager
uuid: d0676147-c20f-49ea-93a6-9c8dbbbba992
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Empaquete su contenido con Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}

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
