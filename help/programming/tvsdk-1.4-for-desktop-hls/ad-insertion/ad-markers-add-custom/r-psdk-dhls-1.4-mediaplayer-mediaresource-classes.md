---
description: MediaResource representa el contenido que está a punto de cargarse en la instancia de MediaPlayer.
title: Clases MediaPlayer y MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Clases MediaPlayer y MediaResource{#mediaplayer-and-mediaresource-classes}

MediaResource representa el contenido que está a punto de cargarse en la instancia de MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

La biblioteca TVSDK proporciona un método sencillo para cargar y preparar contenido para la reproducción mediante el método `replaceCurrentResource` de la interfaz `MediaPlayer`. Este método recibe una instancia de la clase `MediaResource` como único argumento de entrada. La clase `MediaResource` está compuesta por la siguiente información:

* Una dirección URL que representa la ubicación del contenido que está a punto de cargarse.
* Un tipo, que es el tipo de contenido que está a punto de cargarse.

   Es una cadena que define los tipos de contenido que puede cargar el `MediaPlayer`. Los valores posibles son HLS y HDS. Cada valor está asociado con la cadena que representa las extensiones de archivo utilizadas comúnmente, &quot;m3u8&quot; para HLS y &quot;f4m&quot; para HDS.
* Algunos metadatos, que son una instancia de la clase `Metadata`.

   Esta estructura similar a un diccionario puede contener información adicional sobre el contenido que está a punto de cargarse, como información sobre el contenido alternativo o del anuncio que debe colocarse en el contenido principal.

Los metadatos son el medio a través del cual se pasa a TVSDK información relacionada con contenido alternativo. La interfaz `Metadata` define la API para un almacén de clave-valor genérico, donde tanto la clave como el valor son cadenas sin formato.
