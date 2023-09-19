---
title: Notas de la versión de TVSDK 2.1 PlayStation 4
description: Las notas de la versión de TVSDK 2.1 para PlayStation 4 describen las funciones compatibles y los problemas conocidos de TVSDK 2.1 PlayStation 4 .
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# Notas de la versión de TVSDK 2.1 PlayStation 4 {#tvsdk-playstation-release-notes}

Las notas de la versión de TVSDK 2.1 para PlayStation 4 describen las funciones compatibles y los problemas conocidos de TVSDK 2.1 PlayStation 4 .

## Problemas resueltos {#resolved-issues}

Estos son los problemas resueltos para TVSDK 2.1 para PlayStation 4:

**Versión 2.1.0.638**

* **PLAY-10439:**
Cuando el enlace del anuncio envoltorio de VMAP se rompió, el reproductor se quedaba atascado en el estado de preparación (no se enviaba) `onComplete` a su llamador).

* **PLAY-10179:**
  `creativeRepackaging` y `fallbackOnInvalidCreative` Los valores de ahora están desactivados de forma predeterminada. Además, cuando la variable `creativeRepackaging` se ha establecido el indicador, pero no `creativeRepackaging` se ha proporcionado, la variable `onRepackagingComplete` recibía llamadas tantas veces como anuncios en la pausa publicitaria, lo que provocaba que las pausas publicitarias se crearan varias veces.

* **#10304 de Zendesk**: no se inicializó la variable de activación/desactivación de cancelación de publicidad. Ahora inicializamos la variable desde `DataSetEntry's` Actor.

* **PLAY-10318:**
Se ha introducido compatibilidad con el modo de fondo.
* **Zendesk # 17409:**
Al entrar en el modo de reproducción con trucos, volver al modo de reproducción normal y volver al modo de reproducción con trucos, la posición de reproducción saltaba.
* **PTPLAY-9552**
Después de analizar los archivos XML de respuesta, el código de error 1108 ahora se ping siempre que no haya anuncios presentes.
* **PTPLAY-9551**
Cuando no hay pausa publicitaria después del procesamiento del Auditude, el CRS llama a **onPrefetchComplete** lo que reduce groupCount. Dado que no hay pausa publicitaria, la variable **groupCount** es 0 y se reduce en 1. Anteriormente, el **groupCount** era **uint32_t** debido a lo cual se utilizaba para cambiar al valor máximo. Esto es ahora **int32_t**.

**Versión 2.1.0.621**

* **#4555 de Zendesk**
Problemas instantáneos de memoria que generan errores de carga - `MediaItemLoader` Corrección de que se produzca un bloqueo durante la liberación `mediaitemloader`

* **#17223 de Zendesk**
CSAI 2.x: No se activan todas las direcciones URL de seguimiento de anuncios
   * Algunos anuncios VAST que a su vez apuntaban a un anuncio en línea faltaban direcciones URL de seguimiento.
   * Cuando hay varias etiquetas de impresión en un anuncio en XML VAST, solo se guardó la primera URL de impresión y el resto se ignoró. Ahora todas las direcciones URL de impresión se guardarán y se hará ping más adelante.
* **#17224 de Zendesk**
El agente de usuario de PS4 mueve la información de primetime al final de UAString
* **#17226 de Zendesk**
CSAI 2.x: No todos los anuncios se vinculan en.\
  La corrección indica que la escala de tiempo ha cambiado debido a las operaciones insertBy o eraseBy, y realiza el cambio de punto en consecuencia.

* **#17284 de Zendesk**
  [Todas las plataformas] Los subtítulos opcionales no aparecen.\
  HLS: compatibilidad con `EXT-X-MEDIA-TIME` para archivos de subtítulos VTT.

* **#17889 de Zendesk**
Reproducción &quot;Milky&quot; en PS4\
  se aplicó el desplazamiento correcto (para la conversión de color)

* **#17954 de Zendesk**
Lógica de reserva de publicidad + administración de contenido vasto vacío\
  Se ha corregido el problema de que si uno de los contenedores de Vast estaba vacío, el analizador de Vast solía seguir procesando el contenedor.

* **#17807 de Zendesk**
No se puede pasar de la vasta y vacía Igual que Zendesk #3103

* **#17865 de Zendesk**
Lógica alternativa en PS4 y XBox One\
  Igual que Zendesk #3103

**Versión 2.1.0.591**

* **#3767 de Zendesk**
Fragmento de código de anuncio PS4, la resolución de anuncios falla al procesar las redirecciones de VMAP.
* **#4096 de Zendesk**
PS4 CSAI: Error de segmentación Se ha corregido un bloqueo cuando TVSDK generaba un error de segmentación cuando una biblioteca de anuncios estaba procesando una respuesta VMAP.

* **#4161 de Zendesk**
Trickplay 16x al final de la película se congela Se produce un interbloqueo corregido cuando trickplay vuelve a la reproducción normal

* **#4208 de Zendesk**
Bloqueo aleatorio cuando se activan los subtítulos opcionales Se ha corregido una fuga de memoria al activar los subtítulos opcionales

* **#4213 de Zendesk**
CSAI de PS4: cambiar la cadena predeterminada de usuario-agente para todas las llamadas relacionadas con el anuncio. La cadena de usuario-agente se crea con la misma cadena de UA que utiliza el explorador + agregar cadena de Primetime

* **PTPLAY-7675** (interno) Los anuncios transcodificados no se reproducen porque Creative Repacking estaba fallando cuando llamó dentro de una respuesta VMAP o VAST. La corrección es solo leer el archivo multimedia del anuncio en lugar de leer el recurso en caso de anuncios grandes.

* **PTPLAY-7895** (interno) Cuándo `allowMultipleAds=false`, no se reproducen anuncios Error corregido donde `allowMultipleAds` El parámetro no se seguía correctamente.

* **PTPLAY-7896** (interno) Los anuncios se reproducen sin orden de secuencia en PS4 Problema corregido en el que los anuncios no estaban en el orden en el que aparecían en las respuestas XML.

* El SDK de TVSDK de PS4 volvió a probarse en una miniaplicación en lugar de en un juego.

**Versión 2.1.0.563**

* **#3868 de Zendesk**
¿TVSDK es compatible con Playstation SDK 2.5? El TVSDK ahora se crea con el SDK 2.5 de Playstation.

* **#4093 de Zendesk**
targetingInfo pares de clave-valor en la solicitud de Pt Ads.\
  Se agregó un carácter de nueva línea que separa los pares clave/valor.

## Funciones compatibles {#supported-features}

TVSDK 2.1 admite las siguientes funciones para PlayStation 4:

**Versión 2.1.0.621**

* Reserva de anuncios, encadenamiento de margaritas en la lógica de selección de anuncios (Zendesk #3103) Para los anuncios VAST (creativos) con la regla de reserva habilitada, el TVSDK trata un anuncio con un tipo MIME no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva

**Versión 2.1.0.538**

* Reproducción de VOD de HLS, incluida la reproducción, la pausa y la búsqueda
* Flujo de velocidad de bits adaptable
* Reproducción de contenido cifrado con DRM de Primetime y contenido protegido por AES convencional
* Inserción de publicidad del lado del cliente con comportamientos de publicidad predeterminados y perdón por la publicidad
* Reempaquetado creativo
* Subtítulos opcionales de WebVTT
* Inicio instantáneo con posición de inicio personalizada
* Juego de trucos con avance rápido y rebobinado rápido
* Redirección 302

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
