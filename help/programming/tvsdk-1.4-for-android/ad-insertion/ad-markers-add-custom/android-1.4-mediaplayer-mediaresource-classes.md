---
description: MediaResource representa el contenido que está a punto de cargarse en la instancia de MediaPlayer.
seo-description: MediaResource representa el contenido que está a punto de cargarse en la instancia de MediaPlayer.
seo-title: Clases MediaPlayer y MediaResource
title: Clases MediaPlayer y MediaResource
uuid: 7393c320-7dbb-4580-9425-a735f9d03ef5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Clases MediaPlayer y MediaResource{#mediaplayer-and-mediaresource-classes}

MediaResource representa el contenido que está a punto de cargarse en la instancia de MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

La biblioteca TVSDK proporciona un método sencillo para cargar y preparar contenido para la reproducción mediante el `replaceCurrentItem` método de la interfaz de MediaPlayer. Este método recibe una instancia de la clase MediaResource como único argumento de entrada. La clase MediaResource consta de la siguiente información:

* Dirección URL que representa la ubicación del contenido que se va a cargar.
* Tipo, que es el tipo de contenido que se va a cargar.

   Es una enumeración sencilla de la `MediaResource` clase que define los tipos de contenido que puede cargar MediaPlayer. Los valores posibles son HLS y HDS. Cada valor se asocia con la cadena que representa las extensiones de archivo utilizadas habitualmente `m3u8` , para HLS y `f4m` para HDS.
* Algunos metadatos, que son una instancia de la `Metadata` clase.

   Esta estructura de diccionario puede contener información adicional sobre el contenido que se va a cargar, como información sobre el contenido alternativo o de publicidad que se debe colocar en el contenido principal.

Los metadatos son el medio mediante el cual se pasa a TVSDK la información relacionada con el contenido alternativo. La `Metadata` interfaz define la API de un almacén de clave-valor genérico, donde tanto la clave como el valor son cadenas sin formato.
