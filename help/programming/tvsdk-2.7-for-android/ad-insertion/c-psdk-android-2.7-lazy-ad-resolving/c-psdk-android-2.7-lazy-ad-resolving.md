---
description: La resolución y carga de anuncios puede provocar un retraso inaceptable para un usuario que espera la reproducción en el inicio. Las funciones de carga de publicidad diferida y resolución de publicidad diferida pueden reducir este retraso de inicio.
keywords: Lazy;Ad resolving;Ad loading
seo-description: La resolución y carga de anuncios puede provocar un retraso inaceptable para un usuario que espera la reproducción en el inicio. Las funciones de carga de publicidad diferida y resolución de publicidad diferida pueden reducir este retraso de inicio.
seo-title: Resolución de anuncios diferidos
title: Resolución de anuncios diferidos
uuid: cf9ba788-b83f-43aa-94c4-db391d92a77b
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# Información general {#lazy-ad-resolving}

La resolución y carga de anuncios puede provocar un retraso inaceptable para un usuario que espera la reproducción en el inicio. Las funciones de carga de publicidad diferida y resolución de publicidad diferida pueden reducir este retraso de inicio.

* Proceso básico de resolución y carga de anuncios:

   1. TVSDK descarga un manifiesto (lista de reproducción) y *resuelve* todas las publicidades.
   1. TVSDK *carga* todas las publicidades y las coloca en la línea de tiempo.
   1. TVSDK mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.

   El reproductor utiliza las direcciones URL del manifiesto para obtener el contenido de la publicidad (elementos creativos), garantiza que el contenido de la publicidad tenga un formato que TVSDK pueda reproducir y TVSDK coloca las publicidades en la línea de tiempo. Este proceso básico de resolución y carga de publicidades puede provocar un retraso inaceptablemente prolongado para un usuario que espera reproducir su contenido, especialmente si el manifiesto contiene varias direcciones URL de publicidad.

* *Carga* diferida de publicidad:

   1. TVSDK descarga una lista de reproducción y *resuelve* todas las publicidades.
   1. TVSDK *carga* anuncios preliminares, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
   1. TVSDK *carga* el resto de las publicidades y las coloca en la línea de tiempo a medida que se produce la reproducción.

   Esta función mejora el proceso básico al colocar el reproductor en el estado PREPARADO antes de que se carguen todas las publicidades.

* *Resolución* de publicidad diferida:

   1. TVSDK descarga la lista de reproducción.
   1. TVSDK resuelve y carga cualquier anuncio previo, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
   1. TVSDK resuelve y carga los anuncios restantes y los coloca en la línea de tiempo a medida que se produce la reproducción.

   La resolución diferida de publicidad se basa en la carga diferida de publicidad para permitir un inicio aún más rápido. Una vez que TVSDK coloca cualquier anuncio previo, mueve el reproductor al estado PREPARADO y, a continuación, resuelve anuncios adicionales y los coloca en la línea de tiempo.

>[!IMPORTANT]
>
>Factores a tener en cuenta con la resolución de publicidad diferida:
>
>* La resolución diferida de publicidad está habilitada de forma predeterminada. Si lo deshabilita, todas las publicidades se resuelven antes de que se produzcan inicios de reproducción.
>* La resolución de publicidad diferida no permite la búsqueda o reproducción de trucos hasta que se resuelvan todas las publicidades:

   >
   >    
   * El jugador debe esperar el `kEventAdResolutionComplete` evento antes de permitir la búsqueda o el juego truco.
   >    * Si el usuario intenta realizar operaciones de búsqueda o reproducción mediante trucos mientras los anuncios aún se están resolviendo, TVSDK emite el `kECLazyAdResolutionInProgress` error.
   >    * Si es necesario, el reproductor debe actualizar la barra de borrado *después* de recibir el `kEventAdResolutionComplete` evento.
>
>* La resolución diferida de publicidad es solo para VOD. No funcionará con los flujos LIVE.
>* La resolución diferida de publicidad no es compatible con la función Activado *instantáneo* .

>
>  

Para obtener más información sobre la activación instantánea, consulte la activación instantánea.
>
>* Aunque la resolución diferida de publicidad da como resultado que la reproducción comience mucho más rápido, si se produce una pausa publicitaria en los primeros 60 segundos de reproducción, es posible que no se resuelva.
>* La resolución diferida de los anuncios no afecta a los anuncios anteriores.