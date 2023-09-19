---
description: Un MediaResource representa el contenido que está a punto de cargar la instancia de MediaPlayer.
title: Clases MediaPlayer y MediaResource
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Clases MediaPlayer y MediaResource{#mediaplayer-and-mediaresource-classes}

Un MediaResource representa el contenido que está a punto de cargar la instancia de MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

La biblioteca TVSDK proporciona un medio sencillo para cargar y preparar el contenido para la reproducción mediante `replaceCurrentResource` método en la `MediaPlayer` interfaz. Este método recibe una instancia de `MediaResource` como único argumento de entrada. El `MediaResource` La clase se compone de la siguiente información:

* Una dirección URL que representa la ubicación del contenido que se va a cargar.
* Un tipo, que es el tipo de contenido que se va a cargar.

  Es una cadena que define los tipos de contenido que puede cargar el `MediaPlayer`. Los valores posibles son HLS y HDS. Cada valor está asociado con la cadena que representa las extensiones de archivo utilizadas normalmente, &quot;m3u8&quot; para HLS y &quot;f4m&quot; para HDS.
* Algunos metadatos, que es una instancia de `Metadata` clase.

  Esta estructura de tipo diccionario puede contener información adicional sobre el contenido que se va a cargar, como información sobre el contenido alternativo o publicitario que se debe colocar en el contenido principal.

Los metadatos son el medio a través del cual se pasa información relacionada con contenido alternativo a TVSDK. El `Metadata` define la API para un almacén genérico de clave-valor, donde tanto la clave como el valor son cadenas sin formato.
