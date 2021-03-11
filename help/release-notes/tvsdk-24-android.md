---
title: Notas de la versión de TVSDK 2.4.1 para Android
description: Las notas de la versión de TVSDK 2.4.1 para Android describen las funciones nuevas y compatibles, así como los problemas y limitaciones conocidos de TVSDK Android 2.4.1.
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '1963'
ht-degree: 0%

---


# Notas de la versión de TVSDK 2.4.1 para Android {#tvsdk-for-android-release-notes}

Las notas de la versión de TVSDK 2.4.1 para Android describen las funciones nuevas y compatibles, así como los problemas y limitaciones conocidos de TVSDK Android 2.4.1.

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe está publicando TVSDK 2.4.1 para Android.

Para utilizar esta versión de TVSDK, asegúrese de que su sistema cumple los requisitos descritos en [Requisitos del sistema](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

Aquí puede encontrar documentación:

・ Ayuda en línea del sistema de ayuda TVSDK 2.4 para Android

・ [Javadocs TVSDK 2.4 para la API Java de Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Los javadocs son la máxima autoridad, ya que se generan automáticamente directamente a partir del código fuente de TVSDK.

・ Documentación de la API de [C++ TVSDK 2.4 para la API de Android C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

Cada clase Java tiene una clase C++ correspondiente, y la documentación de C++ contiene material más explicativo que los JavaScript, por lo que consulte la documentación de C++ para obtener una comprensión más profunda de la API de Java.

・ Guía de migración ([TVSDK 2.4 para la guía de migración a Android](../migration-guides/tvsdk-14-25-android.md))

Esta guía explica lo que debe modificar para migrar una aplicación basada en TVSDK 1.4 a una basada en TVSDK 2.4.

## Nuevas funciones {#new-features}

TVSDK 2.4.1 para Android proporciona muchas mejoras de rendimiento con respecto a las versiones anteriores. Proporciona una experiencia de visualización de alta calidad.

Esta versión incluye todas las funciones de las versiones 2.4 y 2.4.1, y ninguna función está en desuso.

Estas son las nuevas funciones clave de la versión 2.4.1:

* Funciones de la versión 4 de HLS

   * **Reproducción de vídeo**  (reproducción, pausa, búsqueda) con control del reproductor para emisiones en directo, lineales y VOD.
   * **Subtítulos.** TVSDK puede mostrar subtítulos cerrados 608/708 con una selección de fuentes, tamaños de fuente, colores y fondo. También puede admitir vídeos con subtítulos resumidos y cambiar entre pistas de idioma si están disponibles.
   * **El** modelado Trick play admite el avance y rebobinado rápidos para flujos HLS que utilizan I-Frames. Todos los controles de reproducción de vídeo funcionan en el contenido. El movimiento lento (hacia adelante) está disponible para el modo de reproducción de vídeo externo con velocidades entre 0 y 1.
   * **La velocidad de bits adaptable (ABR)**  permite al reproductor seleccionar dinámicamente cuál de las versiones múltiples del mismo flujo de contenido reproducir, en función de la red y otras condiciones. Puede establecer parámetros de forma dinámica o en el archivo de manifiesto para seleccionarlos entre directivas de selección agresivas, moderadas y conservadoras.
   * **Los rangos de** bytes permiten que un solo archivo TS contenga varios segmentos TS.
   * **Alterne la** representación del audio, permita que el reproductor cambie entre las pistas de audio disponibles.
   * **Compatibilidad con ID3.** TVSDK puede reproducir flujos de audio y vídeo HLS que contengan metadatos de audio ID3, como el nombre del artista, el título y el álbum.
   * **Failover. **TVSDK utiliza estrategias para continuar con la reproducción ininterrumpida, a pesar de los errores de los servidores host, los archivos de lista de reproducción y los segmentos.
   * **Transmisión de audio multicanal (DD+).** TVSDK puede pasar datos de audio Dolby Digital Plus (E-AC3) al hardware compatible.

* Funciones de protección de contenido

   * **DRM para HLS.** Todas las API de reproducción de vídeo funcionan con contenido de vídeo cifrado protegido por Adobe Access. Se admiten las siguientes funciones de DRM:

      * Rotación de licencia
      * Rotación de clave
      * Almacenamiento en caché de licencias
      * Hora de la política
      * Rotación IV

* **Reproducción de AES 128.** TVSDK puede reproducir contenido HLS estándar de cifrado avanzado (AES) con un tamaño clave de 128 bits.
* **HLS protegido (PHLS)** proporciona un conjunto limitado de políticas DRM prediseñadas, un subconjunto de lo que proporciona el acceso a Adobe, para permitir DRM ligero sobre HLS para flujos en vivo y VOD.

* Funciones de publicidad/contenido alternativo y monetización

   * **Seguimiento de anuncios insertados en el lado del servidor.** TVSDK puede rastrear anuncios insertados por el servicio de inserción de anuncios de Adobe Cloud. Admite anuncios lineales en los formatos VAST2, VAST3 y VMAP para transmisiones VOD y en directo/lineal.
   * **Etiquetas HLS personalizadas.** TVSDK utiliza su  `MediaPlayerConfig` clase para permitir la notificación a la aplicación del reproductor cuando aparecen etiquetas HLS personalizadas en el flujo.
   * **Inserción de publicidad en el lado del cliente.** La biblioteca de inserción de anuncios de Auditude funciona con servidores de Adobe Auditude para resolver anuncios que se insertan de forma dinámica en contenido en directo, lineal y VOD, en posiciones pre-roll, mid-roll o post-roll.
   * **Resolvedores de anuncios personalizados.** Las  `ContentResolver, OpportunityGenerator,` interfaces  `MediaPlayerClientFactory` y permiten implementar una resolución de contenido alternativo o de anuncio personalizada y registrar un detector de oportunidades personalizado para trabajar con TVSDK. Las clases `TestAdResolver` y `AuditudeResolver` proporcionan ejemplos C++ de implementación de una resolución de contenido. Puede encontrar un ejemplo de Javascript en `samples/jspsdk/testapp/psdk.js`.
   * **Comportamiento de publicidad coherente.** Utilice la  `AdPolicySelector` interfaz para permitir un comportamiento coherente en todos los reproductores para operaciones como la búsqueda y la reproducción mediante trucos cuando hay anuncios presentes en el contenido. Si no implementa el suyo propio, TVSDK utiliza `DefaultAdPolicySelector`.
   * **Desmonte/sustituya los anuncios C3.** Utilice la API de TVSDK adecuada para eliminar intervalos de contenido personalizados e insertar de forma dinámica nuevos anuncios sin necesidad de realizar trabajos previos adicionales. Esto resulta útil cuando se emite contenido en directo/lineal y luego se pone a disposición inmediatamente bajo demanda sin limpieza.

Estas son las nuevas funciones clave de la versión 2.4:

* **Instantáneo para VOD y** liveCuando activa instantáneamente, TVSDK inicializa y almacena en el búfer los medios antes de que se inicie la reproducción. Dado que puede iniciar varias `MediaPlayerItemLoader` instancias simultáneamente en segundo plano, puede almacenar en búfer varios flujos. Cuando un usuario cambia el canal y el flujo se almacena en el búfer correctamente, la reproducción en el nuevo canal se inicia inmediatamente. TVSDK 2.4 también es compatible con Instant On para emisiones en directo. Las emisiones en directo se vuelven a almacenar en búfer cuando se mueve la ventana en directo.

* **Mejoras de rendimiento **La nueva arquitectura TVSDK 2.4 ofrece varias mejoras de rendimiento:

   * **Subsegmentación** : TVSDK reduce aún más el tamaño de cada fragmento para iniciar la reproducción lo antes posible.
   * **Descargas de anuncios paralelas** : TVSDK recupera previamente los anuncios en paralelo a la reproducción del contenido antes de llegar a las pausas publicitarias, lo que permite una reproducción perfecta de los anuncios y el contenido.
   * **Resolución de anuncios diferida** : Con esta función, no esperamos a la resolución de los anuncios no previos al inicio de la reproducción, lo que reduce el tiempo de inicio. Las API como la búsqueda y el truco siguen sin estar permitidas hasta que se resuelvan todos los anuncios.

* **Reproducción de contenido MP4**

Esta versión de TVSDK admite la reproducción de MP4 como contenido principal.

* **Conexiones de red persistentes**

TVSDK mantiene un conjunto de conexiones de red reutilizables, por lo que no incurre en la sobrecarga de crear y destruir una conexión de red para cada solicitud de red.

* **Protección de salida basada en resolución**

Esta función vincula las restricciones de reproducción con resoluciones específicas, proporcionando controles DRM más precisos.

* **Reproducción trucada con velocidad de bits adaptable (ABR)**

Esta función permite que TVSDK cambie entre flujos de iFrame mientras se encuentra en modo de reproducción asistida. Puede utilizar perfiles que no sean iFrame para hacer la reproducción mediante trucos a velocidades más bajas.

* **Suavizar juego de trucos**

Estas mejoras mejoran la experiencia del usuario:

・ Selección de velocidad de bits adaptable y velocidad de fotogramas durante la reproducción de trucos, según el perfil de búfer y ancho de banda

・ Utilice el flujo principal en lugar del flujo IDR para obtener una reproducción rápida de hasta 30 fps.

* **Lógica ABR mejorada**

La nueva lógica ABR se basa en la longitud del búfer, la velocidad de cambio de la longitud del búfer y el ancho de banda medido. Esto garantiza que el ABR elija la velocidad de bits correcta cuando el ancho de banda fluctúe y también optimiza el número de veces que el interruptor de velocidad de bits se produce controlando la velocidad a la que cambia la longitud del búfer.

* **Facturación**

TVSDK recopila automáticamente métricas, de acuerdo con el contrato de ventas del cliente, para generar los informes de uso periódicos necesarios a efectos de facturación. En cada evento de inicio de flujo, TVSDK utiliza la API de inserción de datos de Adobe Analytics para enviar métricas de facturación como el tipo de contenido, los indicadores habilitados para la inserción de anuncios y los indicadores habilitados para drm (según la duración del flujo facturable) al grupo de informes propiedad de Adobe Analytics Primetime. Esto no interfiere con los grupos de informes de Adobe Analytics ni las llamadas al servidor del cliente, ni se incluye en ellos. Si se solicita, este informe de uso de facturación se envía a los clientes periódicamente. Esta es la primera fase de la función de facturación que solo admite la facturación de uso. Se puede configurar en función del contrato de ventas mediante las API descritas en la documentación.

## Funciones compatibles {#supported-features}

TVSDK para Android 2.4 es compatible con varias funciones que puede implementar para agregar funcionalidad a sus aplicaciones de vídeo.

>[!NOTE]
>
>En las tablas de matriz de funciones que se muestran a continuación, un Ø significa que la función es compatible con la versión actual.

### Funciones principales de reproducción {#core-playback-features}

| **Función** | **Tipo de contenido** | **HLS** | **DASH** |
|---|---|---|---|
| Reproducción general (Reproducir, Pausar, Buscar) | VOD + Activo | Ø | ✓ (Solo VOD) |
| FER: Reproducción general (reproducción, pausa, llamada a otro punto del contenido) | FER VOD | Ø | No admitido |
| MP3 | VOD | No admitido | No admitido |
| Reproducción de contenido de MP4 | VOD | Ø | Ø |
| Lógica de cambio de velocidad de bits adaptable | VOD + Activo | Ø | No admitido |
| Reproducción solo de audio | VOD + Activo | Ø | No admitido |
| Subtítulos - 608/708 | VOD + Activo | Ø | ✓ (Solo VOD) |
| Subtítulos - WebVTT | VOD + Activo | Ø | ✓ (Solo VOD) |
| Error de manifiesto | VOD + Activo | Ø | ✓ (Solo VOD) |
| Failover avanzado | VOD + Activo | Ø | ✓ (Solo VOD) |
| Notificaciones de QoS y del reproductor | VOD + Activo | Ø | ✓ (Solo VOD) |
| Compatibilidad con encabezados de cookie | VOD + Activo | Ø | ✓ (Solo VOD) |
| Compatibilidad con encabezados personalizados | VOD + Activo | No admitido | No admitido |
| Establecer parámetros de control de búfer | VOD + Activo | Ø | ✓ (Solo VOD) |
| Establecer controles de velocidad de bits adaptables | VOD + Activo | Ø | ✓ (Solo VOD) |
| Etiquetas de manifiesto personalizadas (HLS) / Emisiones de eventos (DASH) | VOD + Activo | Ø | ✓ (Solo VOD) |
| Audio enlazado tarde | VOD + Activo | Ø | ✓ (Solo VOD) |
| 302 Redireccionamiento | VOD + Activo | Ø | ✓ (Solo VOD) |

### Funciones de reproducción avanzadas {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>Función</strong></td> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>DASH</strong></td> 
  </tr>
  <tr>
   <td>Reproducción con desplazamiento</td> 
   <td>Activo</td> 
   <td>Ø</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Reproducción solo de audio</td> 
   <td>VOD + Activo</td> 
   <td>Ø</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Reproducción complicada </td> 
   <td>VOD + Activo</td> 
   <td>Ø</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Reproducción suave (con ABR)</td> 
   <td>VOD + Activo</td> 
   <td>Ø</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Análisis de ID3 (HLS)/Metadatos temporizados (DASH)</td> 
   <td>VOD + Activo</td> 
   <td>Ø</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Apagones </td> 
   <td>VOD + Activo</td> 
   <td>No admitido</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Instantáneo activado</td> 
   <td>VOD + Activo</td> 
   <td>Ø</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Compatibilidad con el marcador de discontinuidad (HLS) </li> 
     <li>Varios períodos (DASH)</li> 
    </ul> </td> 
   <td>VOD + Activo</td> 
   <td>Ø</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>302 Adhesividad de redireccionamiento</td> 
   <td>VOD + Activo</td> 
   <td>Ø</td> 
   <td>✓ (Solo VOD)</td> 
  </tr>
  <tr>
   <td>Arrastrar la miniatura (Iframe y JPEG)</td> 
   <td>VOD + Activo</td> 
   <td>No admitido</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Integridad de la emisión </td> 
   <td>VOD + Activo</td> 
   <td>Ø</td> 
   <td>No admitido</td> 
  </tr>
 </tbody>
</table>

### Características del Ad Insertion principal (CSAI) {#core-ad-insertion-features-csai}

| **Función** | **Tipo de contenido** | **HLS** | **DASH** |
|---|---|---|---|
| Reproducción general, anuncios habilitados | VOD + Activo | Ø | ✓ (Solo VOD Pre-rolls) |
| Contenido FER con anuncios habilitados | VOD | Ø | No admitido |
| Comportamientos de publicidad predeterminados | VOD + Activo | Ø | ✓ (Solo VOD Pre-rolls) |
| VAST 2.0/3.0 | VOD + Activo | Ø | ✓ (Solo VOD Pre-rolls) |
| VMAP 1.0 | VOD + Activo | Ø | ✓ (Solo VOD Pre-rolls) |
| Anuncios de MP4 | VOD + Activo | ✓ (de CRS) | ✓ (de CRS, solo de pre-roll) |

### Funciones de Ad Insertion avanzadas (CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>Función</strong></td> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>DASH</strong></td> 
  </tr>
  <tr>
   <td>Reproducción trucada con anuncios habilitados</td> 
   <td>VOD + Activo</td> 
   <td>Ø</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Solo publicidad </td> 
   <td>VOD</td> 
   <td>No admitido</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Parámetros de objetivo</td> 
   <td>VOD + Activo</td> 
   <td>Ø</td> 
   <td>✓ (Solo VOD Pre-rolls)</td> 
  </tr>
  <tr>
   <td>Parámetros personalizados</td> 
   <td>VOD + Activo</td> 
   <td>Ø</td> 
   <td>✓ (Solo VOD Pre-rolls)</td> 
  </tr>
  <tr>
   <td>Comportamientos de publicidad personalizados</td> 
   <td>VOD + Activo</td> 
   <td>Ø</td> 
   <td>✓ (Solo VOD Pre-rolls)</td> 
  </tr>
  <tr>
   <td>Etiquetas de publicidad personalizadas</td> 
   <td>Activo</td> 
   <td>Ø </td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Resolvidores de publicidad personalizados</td> 
   <td>VOD + Activo</td> 
   <td>Ø </td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Resolver publicidad personalizada a Freewheel</td> 
   <td>VOD</td> 
   <td>No admitido</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Sustitución de anuncios C3 </td> 
   <td>VOD + Activo</td> 
   <td>Ø </td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Carga de publicidad diferida</td> 
   <td>VOD</td> 
   <td>Ø </td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Compatibilidad con marcadores de discontinuidad - SSAI (HLS) </li> 
     <li>Varios períodos (DASH)</li> 
    </ul> </td> 
   <td>VOD + Activo</td> 
   <td>Ø </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>Anuncios Companion, Anuncios tipo titular y Anuncios en los que se puede hacer clic</td> 
   <td>VOD + Activo</td> 
   <td>Ø </td> 
   <td>✓ (Solo VOD Pre-rolls)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Activo</td> 
   <td>∙ (JS) </td> 
   <td>✓ (Solo VOD Pre-rolls)</td> 
  </tr>
  <tr>
   <td>Salida de publicidad anticipada</td> 
   <td>Activo</td> 
   <td>Ø </td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>VOD creativa basada en reglas + Prioridad en directo</td> 
   <td>VOD + Activo</td> 
   <td>Ø </td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Reglas CRS </td> 
   <td>VOD + Activo</td> 
   <td>Ø </td> 
   <td>No admitido</td> 
  </tr>
 </tbody>
</table>

## Funciones de protección de contenido {#content-protection-features}

| **Función** | **Tipo de contenido** | **HLS** | **DASH** |
|---|---|---|---|
| Cifrado AES | VOD + Activo | Ø | ✓ (Solo VOD) |
| Ejemplo de cifrado AES | VOD + Activo | Ø |  |
| Emisiones con token | VOD + Activo | Ø |  |
| DRM | VOD + Activo | Solo DRM de Primetime (futuro: Widevine) | Solo Widevine |
| Reproducción externa (RBOP) | VOD + Activo | Solo DRM de Primetime | No admitido |
| Rotación de licencia | VOD + Activo | Solo DRM de Primetime | No admitido |
| Rotación clave | VOD + Activo | Solo DRM de Primetime | No admitido |

### Funciones de integración {#integration-features}

| **Función** | **Tipo de contenido** | **HLS** | **DASH** |
|---|---|---|---|
| Integración de VHL de Adobe Analytics | VOD + Activo | Ø | Ø |
| Facturación | VOD + Activo | Ø | No admitido |

## Funciones no admitidas {#features-not-supported}

Esta versión de TVSDK no es compatible:

* Apagón de anuncios.
* Movimiento lento en juego de trucos.
* Busque y haga clic en Reproducir con contenido de MP4.
* Inserción de publicidad con contenido principal de MP4.
* Busque cuándo se está reproduciendo un anuncio.
* Reproducción de anuncios con medios solo de audio.

## Problemas y limitaciones conocidos {#known-issues-and-limitations}

Esta versión de TVSDK tiene los siguientes problemas:

* Específico del dispositivo (Samsung Galaxy Tab 4) bloquea VOD DRM LBA con audiencia y hace clic en los anuncios
* El anuncio posterior a la emisión no se reproduce para un contenido específico.
* Establecer el subtítulo en idiomas CJK no funciona.
* El vídeo puede salir del modo de truco automáticamente entre VOD y en directo.
* VHL: se envían llamadas de Heartbeat incorrectas cuando iniciamos un contenido desde un desplazamiento.
* Cuando los anuncios VPAID se reproducen, faltan las llamadas de Heartbeat VHL para event:type:play y .
* El anuncio previo a la emisión se reproduce incluso cuando se elige adBreakPolicy SKIP .
* Después de entrar en el reproductor de estado completo, vuelve al estado de reproducción con SKIP adBreakPolicy para anuncios posteriores a la emisión.

Sin vídeo, no hay ninguna dimensión de ventanilla móvil y sin una dimensión de ventanilla móvil, no se puede mostrar ningún gráfico para los rótulos.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Aprendizaje y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).