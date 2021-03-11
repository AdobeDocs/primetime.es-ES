---
description: La resolución de anuncios y la carga de anuncios pueden causar un retraso inaceptable para un usuario que espera a que se inicie la reproducción. Las funciones de Lazy Ad Loading y Lazy Ad Resolving pueden reducir este retraso del inicio.
keywords: Flotante;resolución de publicidad;carga de publicidad
title: Resolución de anuncios diferidos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Información general {#lazy-ad-resolving}

La resolución de anuncios y la carga de anuncios pueden causar un retraso inaceptable para un usuario que espera a que se inicie la reproducción. Las funciones de Lazy Ad Loading y Lazy Ad Resolving pueden reducir este retraso del inicio.

* Proceso básico de resolución y carga de anuncios:

   1. TVSDK descarga un manifiesto (lista de reproducción) y *resuelve* todos los anuncios.
   1. TVSDK *carga* todos los anuncios y los coloca en la cronología.
   1. TVSDK mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.

   El reproductor utiliza las URL del manifiesto para obtener el contenido de la publicidad (creativos), garantiza que el contenido de la publicidad tenga un formato que TVSDK pueda reproducir y TVSDK coloca los anuncios en la cronología. Este proceso básico de resolución y carga de anuncios puede causar un retraso inaceptablemente largo para un usuario que espera reproducir su contenido, especialmente si el manifiesto contiene varias direcciones URL de anuncios.

* *Carga* de publicidad diferida:

   1. TVSDK descarga una lista de reproducción y *resuelve* todos los anuncios.
   1. TVSDK *carga* anuncios previos a la emisión, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
   1. TVSDK *carga* los anuncios restantes y los coloca en la cronología a medida que se produce la reproducción.

   Esta función mejora con respecto al proceso básico al poner el reproductor en el estado PREPARADO antes de cargar todos los anuncios.

* *Resolución de publicidad diferida*:

   1. TVSDK descarga la lista de reproducción.
   1. TVSDK resuelve y carga cualquier anuncio previo a la emisión, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
   1. TVSDK resuelve y carga los anuncios restantes y los pone en la cronología a medida que se produce la reproducción.

   La resolución de publicidad diferida se basa en la carga de publicidad diferida para permitir un inicio aún más rápido. Una vez que TVSDK haya colocado cualquier anuncio previo a la emisión, mueve el reproductor al estado PREPARADO y, a continuación, resuelve los anuncios adicionales y los coloca en la cronología.

>[!IMPORTANT]
>
>Factores a tener en cuenta con la resolución de publicidad diferida:
>
>* La resolución de publicidad diferida está habilitada de forma predeterminada. Si la deshabilita, todas las publicidades se resolverán antes de que se inicie la reproducción.
>* La resolución de publicidad diferida no permite la búsqueda o reproducción de publicidad hasta que se resuelven todos los anuncios:

   >
   >    
   * El reproductor debe esperar al evento `kEventAdResolutionComplete` antes de permitir la llamada a otro punto del contenido o la reproducción mediante trucos.
   >    * Si el usuario intenta realizar operaciones de llamada a otro punto del contenido o de reproducción mientras los anuncios siguen resueltos, TVSDK genera el error `kECLazyAdResolutionInProgress`.
   >    * Si es necesario, el reproductor debe actualizar la barra de desplazamiento, *después* de recibir el evento `kEventAdResolutionComplete`.
>
>* La resolución de anuncios diferida solo es para VOD. No funcionará con flujos en directo.
>* La resolución de publicidad diferida es incompatible con la función *Instant On*.

>
>  

Para obtener más información sobre la activación instantánea, consulte la activación instantánea .
>
>* Aunque la resolución de publicidad diferida hace que la reproducción comience mucho más rápido, si se produce una pausa publicitaria en los primeros 60 segundos de reproducción, es posible que no se resuelva.
>* La resolución de anuncios diferidos no afecta a los anuncios previos a la emisión.