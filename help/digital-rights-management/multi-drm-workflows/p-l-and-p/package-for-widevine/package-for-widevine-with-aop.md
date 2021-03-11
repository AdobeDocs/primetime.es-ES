---
description: Adobe de paquetes sin conexión toma como entrada contenido mp4 sin encriptar.
title: Empaquete el contenido con Adobe Offline Packager
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Empaquete el contenido con Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}

Adobe de paquetes sin conexión toma como entrada contenido mp4 sin encriptar.

**Llamada a Adobe Offline Packager**

Una invocación típica de adobe offline packager sería como la llamada a continuación:

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7f3 1a8ebf1b7ddda5
    -widevine_provider intertrust
    -playready_LA_
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
    -content_id c595f214d d84dc7ecf31a8ebf1b7ddda5

En este caso concreto, el empaquetador sin conexión agrega tanto la protección de contenido Widevine como los datos de inicialización de protección de contenido PlayReady al contenido DASH de salida. El valor de `-key_file_path` es para una clave codificada base64. El valor de `-playready_LA_URL` es para la adquisición de licencias PlayReady.

El argumento conf_path apunta al archivo de configuración que contendría lo siguiente:

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

Como algunos dispositivos Android, principalmente Amazon Fire TV, no admiten el descifrado de audio, el cifrado de audio es opcional.
