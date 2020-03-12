---
title: Notas de la versión de TVSDK 2.1 PlayStation 4
seo-title: Notas de la versión de TVSDK 2.1 PlayStation 4
description: Las notas de la versión de TVSDK 2.1 para PlayStation 4 describen las funciones admitidas y los problemas conocidos de TVSDK 2.1 PlayStation 4.
seo-description: Las notas de la versión de TVSDK 2.1 para PlayStation 4 describen las funciones admitidas y los problemas conocidos de TVSDK 2.1 PlayStation 4.
uuid: 494569cf-07e2-476a-b88e-e46c9cca4cdc
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: ebfc8819-f5a9-47a2-b454-0e4e6f9e4640
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Notas de la versión de TVSDK 2.1 PlayStation 4 {#tvsdk-playstation-release-notes}

Las notas de la versión de TVSDK 2.1 para PlayStation 4 describen las funciones admitidas y los problemas conocidos de TVSDK 2.1 PlayStation 4.

## Problemas resueltos {#resolved-issues}

Estos son los problemas resueltos para TVSDK 2.1 para PlayStation 4:

**Versión 2.1.0.638**

* **PTPLAY-10439:**
Cuando se rompió el vínculo de anuncio de contenedor VMAP, el reproductor se quedaba atascado en el estado de preparación (no se enviaba `onComplete` a su llamador).

* **PTPLAY-10179:**
   `creativeRepackaging` y `fallbackOnInvalidCreative` los valores están desactivados de forma predeterminada. Además, cuando se configuró el `creativeRepackaging` indicador pero no se proporcionó `creativeRepackaging` formato, `onRepackagingComplete` se llamaba al visitante tantas veces como había anuncios en la pausa publicitaria, lo que provocaba que se crearan varias veces saltos de publicidad.

* **Zendesk #10304**:
No se inicializó la variable on/off de perdón de publicidad. Ahora inicializamos la variable desde `DataSetEntry's` ctor.

* **PTPLAY-10318:**
Se ha introducido la compatibilidad con el modo de fondo.
* **Zendesk Nº 17409:**
Al entrar en el modo de reproducción ficticia, volver al modo de reproducción normal y volver al modo de reproducción ficticia, la posición de reproducción saltaba.
* **PTPLAY-9552:**
Después de analizar los archivos XML de respuesta, el código de error 1108 ahora se pega cada vez que no hay anuncios presentes.
* **PTPLAY-9551:**
Cuando no hay un salto de publicidad después del procesamiento de Auditude, el CRS llama **a onPrefetchComplete** , lo que reduce el valor de groupCount. Como no hay pausa publicitaria, el **groupCount** es 0 y se reduce en 1. Anteriormente, **groupCount** era **uint32_t** , ya que solía cambiar al valor máximo. Ahora es **int32_t**.

**Versión 2.1.0.621**

* **Zendesk #4555** Instant on Memory (Problemas de memoria: errores de carga principales): `MediaItemLoader` Corrección de bloqueo que se produce al soltar `mediaitemloader`

* **Zendesk #17223** 2.x CSAI: No todas las direcciones URL de seguimiento de publicidad se activan
   * Algunos anuncios VAST que, a su vez, apuntaban a un anuncio en línea faltaban las direcciones URL de seguimiento.
   * Cuando hay varias etiquetas de impresión en una publicidad en VAST XML, solo se guardó la dirección URL de la primera impresión y se omitió el resto. Ahora todas las direcciones URL de impresión se guardarán y colocarán más tarde.
* **Zendesk #17224** PS4 Agente de usuario mueve la información de hora principal al final de UAString
* **Zendesk #17226** 2.x CSAI: No todas las publicidades están vinculadas.\
   La corrección es para indicar que la línea de tiempo ha cambiado debido a las operaciones insertBy o eraseBy y realizar el cambio de período correspondiente.

* **Zendesk #17284**
   [No se muestran todos los subtítulos opcionales de plataformas] .\
   HLS: compatibilidad con la `EXT-X-MEDIA-TIME` etiqueta para archivos de subtítulos VTT.

* **Zendesk #17889** Reproducción &quot;lechosa&quot; en PS4\
   desplazamiento correcto aplicado (para conversión de color)

* **Zendesk #17954** Lógica de reserva de anuncios + manejo de vastas vacías\
   Se corrigió el problema si uno de los contenedores de Vast estaba vacío, el analizador de Vast utilizado para continuar procesando el envoltorio.

* **Zendesk #17807** No puede superar vastas vacías Igual que Zendesk #3103

* **Lógica de reserva de Zendesk #17865** en PS4 y XBox One\
   Igual que Zendesk #3103

**Versión 2.1.0.591**

* **Fragmento de código de anuncio Zendesk #3767** PS4. La resolución de anuncios falla al procesar redirecciones VMAP.
* **Zendesk #4096** PS4 CSAI: Error de segmentaciónSe corrigió un bloqueo cuando TVSDK genera un error de segmentación cuando la biblioteca de publicidad está procesando una respuesta VMAP.

* **Zendesk #4161** Trickplay 16x al final de la película se bloqueaSe ha corregido el punto muerto que se producía cuando la reproducción de trickplay regresaba a la reproducción normal

* **Zendesk #4208** Bloqueo aleatorio cuando los subtítulos opcionales están activadosSe corrigió una fuga de memoria cuando los subtítulos opcionales estaban habilitados

* **Zendesk #4213** PS4 CSAI: Cambiar la cadena predeterminada de usuario-agente para todas las llamadas relacionadas con la publicidadLa cadena de usuario-agente se crea con la misma cadena de UA que utiliza el explorador + agregar cadena de Primetime

* **PTPLAY-7675** (interno)Los anuncios transcodificados no se reproducenCreative Repacks fallaba cuando se llamaba dentro de una respuesta VMAP o VAST. Corregir es simplemente leer el archivo multimedia de un anuncio en lugar de leer del recurso en caso de anuncios extensos.

* **PTPLAY-7895** (interno)Cuando `allowMultipleAds=false`, ningún anuncio playFixed error donde no se estaba siguiendo correctamente `allowMultipleAds` el parámetro.

* **PTPLAY-7896** (interno)Las publicidades se están mostrando fuera del orden de secuencia en PS4Se ha solucionado el problema de los anuncios que no se mostraban en el orden en que aparecían en las respuestas en XML.

* PS4 TVSDK se volvió a probar en una miniaplicación en lugar de jugar.

**Versión 2.1.0.563**

* **Zendesk #3868** Is TVSDK support Playstation SDK 2.5El TVSDK ahora se ha creado con el SDK 2.5 Playstation.

* **Pares clave-valor de Zendesk #4093** targetingInfo en la solicitud de Anuncios de anuncio.\
   Se agregó un carácter de nueva línea que separa los pares clave/valor.

## Funciones admitidas {#supported-features}

TVSDK 2.1 para PlayStation 4 admite las siguientes funciones:

**Versión 2.1.0.621**

* Acontecimiento publicitario, encadenamiento por marea en la lógica de selección de anuncios (Zendesk #3103)En anuncios VAST (elementos creativos) con la regla de reserva activada, el TVSDK trata una publicidad con un tipo MIME no válido como una publicidad vacía e intenta usar anuncios de reserva en su lugar.Puede configurar algunos aspectos del comportamiento de reserva

**Versión 2.1.0.538**

* Reproducción de HLS VOD, incluida la reproducción, pausa y búsqueda
* Flujo continuo de velocidad de bits adaptable
* Reproducción de contenido cifrado con contenido protegido por AES y DRM de Primetime
* Inserción de anuncios en el lado del cliente con comportamientos de publicidad predeterminados y perdón de anuncios
* Reempaquetado creativo
* Subtítulos cerrados WebVTT
* Activado instantáneamente con posición de inicio personalizada
* Juego rápido con avance rápido y rebobinado rápido
* 302 redireccionamiento

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página de información y asistencia [de](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.