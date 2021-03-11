---
title: Notas de la versión de TVSDK 2.1 PlayStation 4
description: Las notas de la versión de TVSDK 2.1 para PlayStation 4 describen las funciones compatibles y los problemas conocidos de TVSDK 2.1 PlayStation 4 .
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
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
Cuando se rompió el enlace de anuncio de envoltorio VMAP, el reproductor se quedaba atascado en estado de preparación (no enviaba 
`onComplete` a su llamador).

* **PTPLAY-10179:**

   `creativeRepackaging` Los  `fallbackOnInvalidCreative` valores y están desactivados de forma predeterminada. Además, cuando se configuró el indicador `creativeRepackaging` pero no se proporcionó el formato `creativeRepackaging` , se llamaba al `onRepackagingComplete` tantas veces como había anuncios en la pausa publicitaria, lo que provocaba que se crearan pausas publicitarias varias veces.

* **Zendesk #10304**: No se inicializó la variable de activación/desactivación de perdón de publicidad. Ahora inicializamos la variable desde `DataSetEntry's` ctor.

* **PTPLAY-10318:**
Se ha introducido la compatibilidad con el modo en segundo plano.
* **Zendesk # 17409:**
Al entrar en el modo de reproducción de trucos, volver al modo de reproducción normal y, a continuación, volver al modo de reproducción de trucos, la posición de reproducción estaba saltando.
* **PTPLAY-9552:**
Después de analizar los archivos XML de respuesta, el código de error 1108 ahora se pica siempre que no hay anuncios presentes.
* **PTPLAY-9551:**
Cuando no hay pausa publicitaria después del procesamiento de Auditude, las llamadas CRS 
**** onPrefetchComplete, que reduce el groupCount. Dado que no hay pausa publicitaria, el **groupCount** es 0 y se reduce en 1. Anteriormente, **groupCount** era **uint32_t** debido a lo cual solía cambiar al valor máximo. Ahora es **int32_t**.

**Versión 2.1.0.621**

* **Zendesk #4555**
Instant on Memory (Problemas instantáneos de la memoria): errores de carga principales. 
`MediaItemLoader` Corrección de un bloqueo que se produce al soltarlo  `mediaitemloader`

* **Zendesk #17223**
2.x CSAI: No todas las URL de seguimiento de anuncios se activan
   * Algunos anuncios VAST que, a su vez, apuntaban a un anuncio en línea faltaban direcciones url de seguimiento.
   * Cuando hay varias etiquetas de impresión en un anuncio en VAST XML, solo se guardó la primera URL de impresión y se omitieron los demás. Ahora, todas las direcciones URL de impresión se guardarán y anidarán más adelante.
* **Zendesk #17224**
Agente de usuario PS4 mueve la información de horario estelar al final de UAString
* **Zendesk #17226**
2.x CSAI: No todos los anuncios están vinculados.
\
   La corrección es indicar que la línea de tiempo ha cambiado debido a las operaciones insertBy o eraseBy, y realizar el cambio de período correspondiente.

* **Zendesk #17284**
   [Todas las ] plataformasLos subtítulos no se muestran.\
   HLS: compatibilidad con la etiqueta `EXT-X-MEDIA-TIME` para archivos de subtítulos VTT.

* **Zendesk #17889**
Reproducción &quot;lechosa&quot; en PS4
\
   desplazamiento correcto aplicado (para conversión de color)

* **Zendesk #17954**
Lógica de reserva de anuncio + manejo de vasta vacío
\
   Se ha corregido el problema si uno de los contenedores Vast estaba vacío, el analizador Vast solía seguir procesando el envoltorio.

* **Zendesk #17807**
No puede pasar de estar vacío vasto Igual que Zendesk #3103

* **Lógica de reserva de Zendesk #17865**
 en PS4 y XBox One
\
   Igual que Zendesk #3103

**Versión 2.1.0.591**

* **Zendesk #3767**
Fragmento de código de anuncio PS4, la resolución de anuncios falla al procesar redirecciones VMAP.
* **Zendesk #4096**
PS4 CSAI: Error de segmentación Se ha corregido un bloqueo cuando TVSDK genera un error de segmentación cuando la biblioteca de publicidad está procesando una respuesta VMAP.

* **Zendesk #4161**
Trickplay 16x al final de la película bloquea Se ha corregido un punto muerto que se producía cuando el trickplay regresa a la reproducción normal

* **Zendesk #4208**
Bloqueo aleatorio cuando los subtítulos están activados Fuga de memoria fija cuando los subtítulos cerrados estaban habilitados

* **Zendesk #4213**
PS4 CSAI: Cambiar la cadena predeterminada de usuario-agente para todas las llamadas relacionadas con anuncios La cadena de usuario-agente se crea con la misma cadena de UA que utiliza el explorador + añadir cadena de Primetime

* **PTPLAY-7675**  (interno) Los anuncios transcodificados no están reproduciendo Creative Repackaging estaba fallando cuando se llamaba dentro de una respuesta VMAP o VAST. La corrección es leer el archivo multimedia de un anuncio en lugar de leer del recurso en caso de anuncios extensos.

* **PTPLAY-7895**  (interno) Cuando  `allowMultipleAds=false`, ningún anuncio reprodujo un error corregido en el que el  `allowMultipleAds` parámetro no se seguía correctamente.

* **PTPLAY-7896**  (interno) Los anuncios se están mostrando fuera de secuencia en PS4 Se ha corregido un problema en el que los anuncios no estaban en el orden en el que aparecían en las respuestas XML.

* PS4 TVSDK se volvió a probar dentro de una miniaplicación en lugar de en un juego.

**Versión 2.1.0.563**

* **Zendesk #3868**
¿Admite TVSDK Playstation SDK 2.5? El TVSDK se ha creado con el SDK 2.5 Playstation.

* **Pares de clave-valor Zendesk #4093**
targetingInfo en la solicitud de Anuncios de anuncio.
\
   Se ha añadido un carácter de nueva línea que separa los pares clave/valor.

## Funciones compatibles {#supported-features}

TVSDK 2.1 para PlayStation 4 admite las siguientes funciones:

**Versión 2.1.0.621**

* Abandono de anuncios, encadenamiento de margaritas en la lógica de selección de anuncios (Zendesk #3103)
En el caso de los anuncios VAST (creativos) con la regla de reserva habilitada, TVSDK trata un anuncio con un tipo MIME no válido como un anuncio vacío e intenta utilizar anuncios de reserva en su lugar.Puede configurar algunos aspectos del comportamiento de reserva

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

* Consulte la documentación de ayuda completa en la página [Aprendizaje y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).