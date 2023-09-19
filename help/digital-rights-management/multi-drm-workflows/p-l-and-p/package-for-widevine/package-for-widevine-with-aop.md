---
description: El empaquetador sin conexión de Adobe toma como entrada contenido mp4 sin cifrar.
title: Empaquetar el contenido con Adobe Offline Packager
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Empaquetar el contenido con Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}

El empaquetador sin conexión de Adobe toma como entrada contenido mp4 sin cifrar.

**Llamando al empaquetador sin conexión de Adobe**

Una invocación típica del empaquetador sin conexión de Adobe tendría el siguiente aspecto:

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
    interconfianza -widevine_provider
    -playready_LA_URL
    http://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
    -content_id c595f214d84dc7ecf31a8ebf1b7ddda5

En este caso particular, el empaquetador sin conexión agrega los datos de inicialización de la protección de contenido Widevine y de la protección de contenido PlayReady al contenido DASH de salida. El valor de `-key_file_path` es para una clave codificada en base64. El valor de `-playready_LA_URL` es para la adquisición de licencias PlayReady.

El argumento conf_path apunta al archivo de configuración que contendría lo siguiente:

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

Debido a que algunos dispositivos Android, principalmente Amazon Fire TV, no admiten el descifrado de audio, el cifrado de audio es opcional.
