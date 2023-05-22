---
description: Un MediaResource representa el contenido que está a punto de cargar la instancia de MediaPlayer.
title: Clases MediaPlayer y MediaResource
exl-id: d3ac1a8d-3549-417a-83e9-c561a3d12127
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Clases MediaPlayer y MediaResource{#mediaplayer-and-mediaresource-classes}

Un MediaResource representa el contenido que está a punto de cargar la instancia de MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

La biblioteca TVSDK proporciona un medio sencillo para cargar y preparar el contenido para la reproducción mediante `replaceCurrentItem` en la interfaz de MediaPlayer. Este método recibe una instancia de la clase MediaResource como único argumento de entrada. La clase MediaResource consta de la siguiente información:

* Una dirección URL que representa la ubicación del contenido que se va a cargar.
* Un tipo, que es el tipo de contenido que se va a cargar.

   Esta es una enumeración simple en el `MediaResource` que define los tipos de contenido que MediaPlayer puede cargar. Los valores posibles son HLS y HDS. Cada valor está asociado con la cadena que representa las extensiones de archivo utilizadas comúnmente, `m3u8` para HLS y `f4m` para el HDS.
* Algunos metadatos, que es una instancia de `Metadata` clase.

   Esta estructura de tipo diccionario puede contener información adicional sobre el contenido que se va a cargar, como información sobre el contenido alternativo o publicitario que se debe colocar en el contenido principal.

Los metadatos son el medio a través del cual se pasa información relacionada con contenido alternativo a TVSDK. El `Metadata` define la API para un almacén genérico de clave-valor, donde tanto la clave como el valor son cadenas sin formato.
