---
description: La resolución de anuncios y la carga de anuncios pueden provocar un retraso inaceptable para un usuario que espera a que se inicie la reproducción. Las funciones de carga diferida de publicidad y de resolución diferida de publicidad pueden reducir este retraso en el inicio.
keywords: Diferido;Resolución de publicidad;Carga de publicidad
title: Resolución de anuncios diferida
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Información general {#lazy-ad-resolving}

La resolución de anuncios y la carga de anuncios pueden provocar un retraso inaceptable para un usuario que espera a que se inicie la reproducción. Las funciones de carga diferida de publicidad y de resolución diferida de publicidad pueden reducir este retraso en el inicio.

* Proceso básico de resolución y carga de anuncios:

   1. TVSDK descarga un manifiesto (lista de reproducción) y *resuelve* todos los anuncios.
   1. TVSDK *cargas* todos los anuncios y los coloca en la cronología.
   1. TVSDK mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.

  El reproductor utiliza las direcciones URL del manifiesto para obtener el contenido del anuncio (creativos), garantiza que el contenido del anuncio esté en un formato que TVSDK pueda reproducir y TVSDK coloca los anuncios en la cronología. Este proceso básico de resolución y carga de anuncios puede causar un retraso inaceptablemente largo a un usuario que espera para reproducir su contenido, especialmente si el manifiesto contiene varias direcciones URL de publicidad.

* *Carga diferida de publicidad*:

   1. TVSDK descarga una lista de reproducción y *resuelve* todos los anuncios.
   1. TVSDK *cargas* anuncio previo a la emisión, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
   1. TVSDK *cargas* los anuncios restantes y los coloca en la cronología a medida que se produce la reproducción.

  Esta función mejora el proceso básico al poner el reproductor en el estado PREPARADO antes de que se carguen todos los anuncios.

* *Resolución de publicidad diferida*:

   1. TVSDK descarga la lista de reproducción.
   1. TVSDK resuelve y carga los anuncios previos a la emisión, mueve el reproductor al estado PREPARADO y se inicia la reproducción del contenido.
   1. TVSDK resuelve y carga los anuncios restantes y los coloca en la cronología a medida que se produce la reproducción.

  La resolución de anuncios diferidos se basa en la carga de anuncios diferidos para permitir un inicio aún más rápido. Una vez que TVSDK coloca los anuncios previos a la emisión, mueve el reproductor al estado PREPARADO y, a continuación, resuelve los anuncios adicionales y los coloca en la cronología.

>[!IMPORTANT]
>
>Factores a considerar con la resolución de anuncios diferidos:
>
>* La resolución de anuncios diferidos está habilitada de forma predeterminada. Si lo desactiva, todos los anuncios se resuelven antes de que comience la reproducción.
>* La resolución diferida de anuncios no permite la llamada a otro punto del contenido ni el truco hasta que se resuelven todos los anuncios:
>
>    * El reproductor debe esperar al `kEventAdResolutionComplete` antes de permitir la búsqueda o el truco.
>    * Si el usuario intenta realizar operaciones de búsqueda o truco mientras los anuncios aún se están resolviendo, TVSDK emite el `kECLazyAdResolutionInProgress` error.
>    * Si es necesario, el reproductor debe actualizar la barra de desplazamiento, *después* recepción de la `kEventAdResolutionComplete` evento.
>
>* La resolución de anuncios diferidos solo es para VOD. No funcionará con emisiones en directo.
>* La resolución de publicidad diferida no es compatible con el *Instant On* función.
>
>  Para obtener más información sobre Instant On, consulte Instant-on .
>
>* Aunque la resolución diferida de anuncios hace que la reproducción se inicie mucho más rápido, es posible que no se resuelva si se produce una pausa publicitaria en los primeros 60 segundos de reproducción.
>* La resolución diferida de los anuncios no afecta a los anuncios previos a la emisión.
