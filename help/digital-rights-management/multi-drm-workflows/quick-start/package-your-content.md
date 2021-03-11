---
description: El empaquetado de contenido es el proceso de preparación de contenido de vídeo para su reproducción en la web. El empaquetado incluye la transformación de vídeo sin procesar en archivos de manifiesto y, opcionalmente, el cifrado del contenido mediante distintas soluciones DRM para distintos dispositivos y navegadores.
title: Empaquete su contenido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Empaquete su contenido {#package-your-content}

El empaquetado de contenido es el proceso de preparación de contenido de vídeo para su reproducción en la web. El empaquetado incluye la transformación de vídeo sin procesar en archivos de manifiesto y, opcionalmente, el cifrado del contenido mediante distintas soluciones DRM para distintos dispositivos y navegadores.

Para preparar el contenido, puede utilizar Adobe Offline Packager u otras herramientas como el empaquetador Bento4 de ExpressPlay. Los empaquetadores preparan el vídeo para su reproducción (por ejemplo, fragmentando el archivo original y poniéndolo en un manifiesto) y protegen el vídeo con la solución DRM elegida (PlayReady, Widevine, FairPlay, Access, etc.):

* [Paquete sin conexión de Adobe](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [Paquetes ExpressPlay](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. Empaquete u obtenga contenido para usarlo para probar su configuración.

   Uno de los puntos cruciales que hay que recordar para el empaquetado es que el ID de clave (ID de contenido) que se utiliza en este paso de empaquetado es el mismo que se debe proporcionar en la solicitud de token de licencia posterior. El ID de clave es el único elemento que identifica su CEK (que puede almacenarse en su propia base de datos de administración de claves o almacenarse utilizando el servicio de almacenamiento de claves [ExpressPlay&#39;s Key Storage Service](https://www.expressplay.com/developer/key-storage/).

   >[!NOTE]
   >
   >Para aquellos familiarizados con el acceso a Adobe, esta es una diferencia importante en el funcionamiento de las distintas soluciones. En Access, la clave de licencia está incrustada en los metadatos DRM y se transfiere de un lado a otro con el contenido protegido. En los sistemas Multi-DRM descritos aquí, la licencia real no se transfiere, sino que se almacena de forma segura y se obtiene mediante el ID de clave.

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

Este es un ejemplo de paquete que utiliza Adobe Offline Packager para Widevine. El empaquetador utiliza un archivo de configuración (por ejemplo, [!DNL widevine.xml]), que tiene este aspecto:

```
<config> 
<in_path>sample.mp4</in_path> 
<out_type>dash</out_type> 
<out_path>dash2</out_path> 
<drm/> 
<drm_sys>widevine</drm_sys> 
<frag_dur>4</frag_dur> 
<target_dur>6</target_dur> 
<key_file_path>keyfile.bin</key_file_path> 
<widevine_content_id>2a</widevine_content_id> 
<widevine_provider>intertrust</widevine_provider> 
<widevine_key_id>7debe705d938c76bfd886f077b8fa5f7</widevine_key_id> 
</config>
```

* `in_path` - Esta entrada apunta a la ubicación del vídeo de origen en su máquina de embalaje local.
* `out_type` - Esta entrada describe el tipo de salida empaquetada, en este caso DASH (para protección Widevine en HTML5).
* `out_path` - La ubicación en el equipo local donde desea que vaya la salida.
* `drm_sys` - La solución DRM para la que está empaquetando. Será `widevine`, `fairplay` o `playready`.

* `frag_dur` y  `target_dur` son entradas de duración específicas de DASH que pertenecen a la reproducción de vídeo.

* `key_file_path` - Esta es la ubicación del archivo de licencia en el equipo de embalaje que sirve como clave de cifrado de contenido (CEK). Es una cadena hexadecimal con codificación Base-64 de 16 bytes.
* `widevine_content_id` - Este es &quot;repetidor&quot; Widevine; siempre lo es  `2a`. (No confunda esto con `widevine_key_id`).

* `widevine_provider` - Para nuestros propósitos, establezca siempre esto como  `intertrust`.

* `widevine_key_id` - Este es el identificador de la licencia especificada en la  `key_file_path` entrada. En otras palabras, esto identifica la clave que se utiliza para cifrar el contenido. Este ID es una cadena HEX de 16 bytes que usted mismo crea.

Como se indica en la [documentación de Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf), &quot;Como práctica recomendada, cree un archivo de configuración que contenga las opciones comunes que desee utilizar para generar las salidas. A continuación, cree el resultado proporcionando opciones específicas como argumento de línea de comandos&quot;. En este caso, nuestro archivo de configuración es bastante completo, por lo que puede crear su salida de la siguiente manera:

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>Los parámetros de la línea de comandos tienen prioridad sobre los parámetros del archivo de configuración. En este ejemplo, todo lo necesario está en el archivo de configuración, pero hemos anulado la ruta de salida especificada en el archivo de configuración con `-out_path test_dash/`.

