---
description: MediaResource representa el contenido que está a punto de cargarse en la instancia de MediaPlayer.
seo-description: MediaResource representa el contenido que está a punto de cargarse en la instancia de MediaPlayer.
seo-title: Clases MediaPlayer y MediaResource
title: Clases MediaPlayer y MediaResource
uuid: 36ef75f3-08f7-4fc5-88a7-9bab9198b917
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Clases MediaPlayer y MediaResource{#mediaplayer-and-mediaresource-classes}

MediaResource representa el contenido que está a punto de cargarse en la instancia de MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

La biblioteca TVSDK proporciona un método sencillo para cargar y preparar contenido para la reproducción mediante el `replaceCurrentResource` método de la `MediaPlayer` interfaz. Este método recibe una instancia de la `MediaResource` clase como único argumento de entrada. La `MediaResource` clase se compone de la siguiente información:

* Dirección URL que representa la ubicación del contenido que se va a cargar.
* Tipo, que es el tipo de contenido que se va a cargar.

   Es una cadena que define los tipos de contenido que puede cargar el `MediaPlayer`. Los valores posibles son HLS y HDS. Cada valor está asociado con la cadena que representa las extensiones de archivo utilizadas habitualmente, &quot;m3u8&quot; para HLS y &quot;f4m&quot; para HDS.
* Algunos metadatos, que son una instancia de la `Metadata` clase.

   Esta estructura de diccionario puede contener información adicional sobre el contenido que se va a cargar, como información sobre el contenido alternativo o de publicidad que se debe colocar en el contenido principal.

Los metadatos son el medio mediante el cual se pasa a TVSDK la información relacionada con el contenido alternativo. La `Metadata` interfaz define la API de un almacén de clave-valor genérico, donde tanto la clave como el valor son cadenas sin formato.
