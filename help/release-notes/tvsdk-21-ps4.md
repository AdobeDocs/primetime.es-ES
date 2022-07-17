---
title: Notas de la versión de TVSDK 2.1 PlayStation 4
description: Las notas de la versión de TVSDK 2.1 para PlayStation 4 describen las funciones compatibles y los problemas conocidos de TVSDK 2.1 PlayStation 4 .
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 32af3fe4-c730-41f6-a558-987bd14c9bae
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# Notas de la versión de TVSDK 2.1 PlayStation 4 {#tvsdk-playstation-release-notes}

Las notas de la versión de TVSDK 2.1 para PlayStation 4 describen las funciones compatibles y los problemas conocidos de TVSDK 2.1 PlayStation 4 .

## Problemas resueltos {#resolved-issues}

Estos son los problemas resueltos para TVSDK 2.1 para PlayStation 4:

**Versión 2.1.0.638**

* **PTPLAY-10439:**
Cuando se rompió el enlace de anuncio de envoltorio VMAP, el reproductor se quedaba atascado en el estado de preparación (no enviaba 
`onComplete` a su llamador).

* **PTPLAY-10179:**

   `creativeRepackaging` y `fallbackOnInvalidCreative` ahora están desactivados de forma predeterminada. Además, cuando la variable `creativeRepackaging` se estableció el indicador pero no `creativeRepackaging` se proporcionó, la variable `onRepackagingComplete` se llamaba tantas veces como había anuncios en la pausa publicitaria, lo que provocaba que las pausas publicitarias se crearan varias veces.

* **Zendesk #10304**: No se inicializó la variable de activación/desactivación de perdón de publicidad. Ahora inicializamos la variable desde `DataSetEntry's` ctor.

* **PTPLAY-10318:**
Se ha introducido la compatibilidad con el modo en segundo plano.
* **Zendesk #17409:**
Al entrar en el modo de reproducción de trucos, volver al modo de reproducción normal y, a continuación, volver al modo de reproducción de trucos, la posición de reproducción estaba saltando.
* **PTPLAY-9552:**
Después de analizar los archivos XML de respuesta, el código de error 1108 ahora se pica siempre que no hay anuncios presentes.
* **PTPLAY-9551:**
Cuando no hay pausa publicitaria después del procesamiento de Auditude, las llamadas CRS 
**onPrefetchComplete** que reduce el valor de groupCount. Dado que no hay pausa publicitaria, el **groupCount** es 0 y se reduce en 1. Anteriormente, la variable **groupCount** was **uint32_t** debido a lo cual solía cambiar al valor máximo. Esto es ahora **int32_t**.

**Versión 2.1.0.621**

* **Zendesk #4555**
Problemas con Instant on Memory que generan errores de carga: 
`MediaItemLoader` Corrección de un bloqueo que se produce al soltarlo `mediaitemloader`

* **Zendesk #17223**
2.x CSAI: No todas las URL de seguimiento de anuncios se activan
   * Algunos anuncios VAST que, a su vez, apuntaban a un anuncio en línea faltaban direcciones url de seguimiento.
   * Cuando hay varias etiquetas de impresión en un anuncio en VAST XML, solo se guardó la primera URL de impresión y se omitieron los demás. Ahora, todas las direcciones URL de impresión se guardarán y anidarán más adelante.
* **Zendesk #17224**
El agente de usuario de PS4 mueve la información de horario primario hasta el final de UAString
* **Zendesk #17226**
2.x CSAI: No todos los anuncios están vinculados.
\
   La corrección es indicar que la línea de tiempo ha cambiado debido a las operaciones insertBy o eraseBy, y realizar el cambio de período correspondiente.

* **Zendesk #17284**
   [Todas las plataformas] Los subtítulos no aparecen.\
   HLS: compatibilidad con `EXT-X-MEDIA-TIME` para archivos de subtítulos VTT.

* **Zendesk #17889**
Reproducción &quot;Láctea&quot; en PS4
\
   se ha aplicado un desplazamiento correcto (para conversión de color)

* **Zendesk #17954**
Lógica de reserva de anuncio + administración de vastas vacías
\
   Se ha corregido el problema si uno de los contenedores Vast estaba vacío, el analizador Vast solía seguir procesando el envoltorio.

* **Zendesk #17807**
No se puede pasar del vasto vacío Igual que Zendesk #3103

* **Zendesk #17865**
Lógica de reserva en PS4 y XBox One
\
   Igual que Zendesk #3103

**Versión 2.1.0.591**

* **Zendesk #3767**
Fragmento de código de anuncio PS4, la resolución de anuncios falla al procesar redirecciones VMAP.
* **Zendesk #4096**
PS4 CSAI: Error de segmentación Se ha corregido un bloqueo cuando TVSDK genera un error de segmentación cuando la biblioteca de publicidad está procesando una respuesta VMAP.

* **Zendesk #4161**
Trickplay 16x al final de la película bloquea Se produce un bloqueo fijo cuando trickplay vuelve a la reproducción normal

* **Zendesk #4208**
Bloqueo aleatorio cuando los subtítulos están activados Fuga de memoria fija cuando los subtítulos están habilitados

* **Zendesk #4213**
PS4 CSAI: Cambiar la cadena predeterminada de usuario-agente para todas las llamadas relacionadas con anuncios La cadena de usuario-agente se crea con la misma cadena de UA que utiliza el explorador + añadir cadena de Primetime

* **PTPLAY-7675** (interno) Los anuncios transcodificados no están reproduciendo Creative Repackaging estaba fallando cuando se llamaba dentro de una respuesta VMAP o VAST. La corrección es leer el archivo multimedia de un anuncio en lugar de leer del recurso en caso de anuncios extensos.

* **PTPLAY-7895** (interno) al `allowMultipleAds=false`, sin anuncios reproducidos Se ha corregido un error en el que `allowMultipleAds` no se estaba siguiendo correctamente.

* **PTPLAY-7896** (interno) Los anuncios se están mostrando fuera del orden de secuencia en PS4 Se ha corregido un problema en el que los anuncios no estaban en el orden en el que aparecían en las respuestas XML.

* PS4 TVSDK se volvió a probar dentro de una miniaplicación en lugar de en un juego.

**Versión 2.1.0.563**

* **Zendesk #3868**
¿TVSDK es compatible con Playstation SDK 2.5? El TVSDK se ha creado con el SDK 2.5 Playstation.

* **Zendesk #4093**
pares clave-valor de targetingInfo en la solicitud de Pt Ads.
\
   Se ha añadido un carácter de nueva línea que separa los pares clave/valor.

## Funciones compatibles {#supported-features}

TVSDK 2.1 para PlayStation 4 admite las siguientes funciones:

**Versión 2.1.0.621**

* Abandono de anuncios, encadenamiento de margaritas en la lógica de selección de anuncios (Zendesk #3103) Para anuncios VAST (creativos) con la regla de reserva activada, TVSDK trata una publicidad con un tipo MIME no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar.Puede configurar algunos aspectos del comportamiento de reserva

**Versión 2.1.0.538**

* Reproducción de VOD de HLS, incluida la reproducción, la pausa, la búsqueda
* Flujo continuo de velocidad de bits adaptable
* Reproducción de contenido cifrado con contenido protegido con AES de vainilla y DRM de Primetime
* Inserción de publicidad del lado del cliente con comportamientos de publicidad predeterminados y perdón de publicidad
* Nuevo embalaje
* Subtítulos cerrados de WebVTT
* Instantáneo con posición de inicio personalizada
* Juego travieso con avance rápido y rebobinado rápido
* 302 redireccionamiento

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Información y asistencia de Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
