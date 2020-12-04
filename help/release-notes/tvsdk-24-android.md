---
title: Notas de la versión de TVSDK 2.4.1 para Android
seo-title: Notas de la versión de TVSDK 2.4.1 para Android
description: Las notas de la versión de TVSDK 2.4.1 para Android describen las funciones nuevas y admitidas, así como los problemas conocidos y las limitaciones de TVSDK Android 2.4.1.
seo-description: Las notas de la versión de TVSDK 2.4.1 para Android describen las funciones nuevas y admitidas, así como los problemas conocidos y las limitaciones de TVSDK Android 2.4.1.
uuid: 929fc577-e851-4e03-9201-13280cc6137a
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: a6dbcc4a-9e14-4452-9004-b39ed13fad6f
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '1988'
ht-degree: 0%

---


# Notas de la versión de TVSDK 2.4.1 para Android {#tvsdk-for-android-release-notes}

Las notas de la versión de TVSDK 2.4.1 para Android describen las funciones nuevas y admitidas, así como los problemas conocidos y las limitaciones de TVSDK Android 2.4.1.

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe está lanzando TVSDK 2.4.1 para Android.

Para utilizar esta versión de TVSDK, asegúrese de que su sistema cumple los requisitos descritos en [Requisitos del sistema](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

Aquí puede encontrar la documentación:

・ Ayuda del sistema de ayuda en línea TVSDK 2.4 para Android

・ [Javadocs TVSDK 2.4 para la API Java de Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Los javadocs son la máxima autoridad, ya que se generan automáticamente directamente a partir del código fuente TVSDK.

・ [Documentación de API de C++ TVSDK 2.4 para Android C++ API](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

Cada clase Java tiene una clase C++ correspondiente y la documentación de C++ contiene más material explicativo que los Java, por lo que consulte la documentación de C++ para obtener una comprensión más profunda de la API de Java.

・ Guía de migración ([Guía de migración de TVSDK 2.4 para Android](../migration-guides/tvsdk-14-25-android.md))

En esta guía se explica qué debe modificar para migrar una aplicación basada en TVSDK 1.4 a una basada en TVSDK 2.4.

## Nuevas funciones {#new-features}

TVSDK 2.4.1 para Android proporciona muchas mejoras de rendimiento con respecto a versiones anteriores. Proporciona una experiencia de visualización de alta calidad.

Esta versión incluye todas las funciones de las versiones 2.4 y 2.4.1, y no hay ninguna característica en desuso.

Estas son las nuevas funciones clave de la versión 2.4.1:

* Funciones de HLS versión 4

   * **Reproducción**  de vídeo (reproducción, pausa, búsqueda) con control del reproductor para flujos en directo, lineales y VOD.
   * **Subtítulos opcionales.** TVSDK puede mostrar subtítulos opcionales 608/708 con una selección de fuentes, tamaños de fuente, colores y fondo. También puede admitir vídeos con subtítulos resumidos y cambiar entre las pistas de idiomas si están disponibles.
   * **El** modelo de reproducción de trucos permite avanzar y rebobinar rápidamente para flujos HLS que utilizan I-Frames. Todos los controles de reproducción de vídeo funcionan en el contenido. El movimiento lento (hacia delante) está disponible para el modo de reproducción de vídeo externo con velocidades entre 0 y 1.
   * **La velocidad de bits adaptable (ABR)** permite al reproductor seleccionar dinámicamente cuál de las versiones múltiples del mismo flujo de contenido se va a reproducir, en función de la red y otras condiciones. Puede definir parámetros de forma dinámica o en el archivo de manifiesto para seleccionarlos entre políticas de selección agresivas, moderadas y conservadoras.
   * **Los rangos de** bytes permiten que un solo archivo TS contenga varios segmentos de TS.
   * **Se puede** reproducir audio alternativo para que el reproductor pueda cambiar entre las pistas de audio disponibles.
   * **Compatibilidad con ID3.** TVSDK puede reproducir flujos de audio y vídeo HLS que contengan metadatos de audio ID3, como nombre del artista, título y álbum.
   * **Failover. **TVSDK utiliza estrategias para continuar la reproducción ininterrumpida, a pesar de los errores de los servidores host, los archivos de listas de reproducción y los segmentos.
   * **Transferencia de audio de varios canales (DD+).** TVSDK puede pasar datos de audio Dolby Digital Plus (E-AC3) a hardware compatible.

* Funciones de protección de contenido

   * **DRM para HLS.** Todas las API de reproducción de vídeo funcionan con contenido de vídeo cifrado protegido por Adobe Access. Se admiten las siguientes funciones de DRM:

      * Rotación de licencia
      * Rotación de clave
      * Caché de licencias
      * Hora de la política
      * Rotación IV

* **Reproducción de AES 128.** TVSDK puede reproducir contenido HLS estándar de codificación avanzada (AES) con un tamaño de clave de 128 bits.
* **HLS protegido (PHLS)** proporciona un conjunto limitado de directivas DRM prediseñadas, un subconjunto de lo que Adobe Access proporciona, para permitir DRM livianos sobre HLS para flujos en vivo y VOD.

* Publicidad/contenido alternativo y funciones de monetización

   * **Seguimiento de anuncios insertados en el lado del servidor.** TVSDK puede rastrear las publicidades insertadas por el servicio de inserción de anuncios de Adobe Cloud. Admite anuncios lineales en los formatos VAST2, VAST3 y VMAP para flujos en directo y lineal.
   * **Etiquetas HLS personalizadas.** TVSDK utiliza su  `MediaPlayerConfig` clase para permitir la notificación a la aplicación del reproductor cuando aparecen etiquetas HLS personalizadas en el flujo.
   * **Inserción de publicidad en el lado del cliente.** La biblioteca de inserción de anuncios de Auditude funciona con servidores de Adobe Auditude para resolver anuncios que se pueden insertar dinámicamente en contenido en directo, lineal y VOD, en posiciones anteriores, intermedias o posteriores al lanzamiento.
   * **Resoluciones de publicidad personalizadas.** Las  `ContentResolver, OpportunityGenerator,` interfaces  `MediaPlayerClientFactory` y le permiten implementar una resolución de contenido alternativo o de publicidad personalizada y registrar un detector de oportunidades personalizado para trabajar con TVSDK. Las clases `TestAdResolver` y `AuditudeResolver` proporcionan ejemplos de C++ para implementar una resolución de contenido. Puede encontrar un ejemplo de Javascript en `samples/jspsdk/testapp/psdk.js`.
   * **Comportamiento publicitario coherente.** Utilice la  `AdPolicySelector` interfaz para permitir un comportamiento coherente en todos los reproductores para operaciones como la búsqueda y la reproducción mediante trucos cuando hay anuncios presentes en el contenido. Si no implementa el suyo propio, TVSDK utiliza `DefaultAdPolicySelector`.
   * **Retire o reemplace las publicidades C3.** Utilice la API de TVSDK adecuada para eliminar intervalos de contenido personalizados e insertar de forma dinámica nuevas publicidades sin necesidad de realizar ningún trabajo previo adicional. Esto resulta práctico cuando se difunde contenido en directo o lineal y, a continuación, se pone a disposición inmediatamente bajo demanda sin limpieza.

Estas son las nuevas funciones clave de la versión 2.4:

* **Activado instantáneamente para VOD y** liveCuando se activa instantáneamente, TVSDK inicializa y almacena en búfer los medios antes de los inicios de reproducción. Dado que puede iniciar varias instancias `MediaPlayerItemLoader` simultáneamente en segundo plano, puede almacenar en búfer varios flujos. Cuando un usuario cambia el canal y el flujo se almacena correctamente en el búfer, la reproducción en los nuevos inicios de canal se realiza inmediatamente. TVSDK 2.4 también admite Instant On para transmisiones en directo. Los flujos activos se vuelven a almacenar en búfer cuando se mueve la ventana activa.

* **Mejoras de rendimiento **La nueva arquitectura TVSDK 2.4 ofrece varias mejoras de rendimiento:

   * **Subsegmentación** : TVSDK reduce aún más el tamaño de cada fragmento a la reproducción de inicio lo antes posible.
   * **Descargas**  de anuncios paralelas: TVSDK obtiene previamente anuncios en paralelo a la reproducción de contenido antes de visitar los saltos de publicidad, lo que permite una reproducción sin problemas de los anuncios y el contenido.
   * **Resolución**  de anuncios diferida: Con esta función, no esperamos la resolución de anuncios no previos antes de iniciar la reproducción, lo que reduce el tiempo de inicio. Las API, como la búsqueda y la reproducción mediante trucos, siguen sin permitirse hasta que se resuelvan todos los anuncios.

* **Reproducción de contenido MP4**

Esta versión de TVSDK admite la reproducción de MP4 como contenido principal.

* **Conexiones de red persistentes**

TVSDK mantiene un conjunto de conexiones de red reutilizables, por lo que no incurre en gastos generales de creación y destrucción de una conexión de red para cada solicitud de red.

* **Protección de salida basada en resolución**

Esta función vincula las restricciones de reproducción con resoluciones específicas, proporcionando controles DRM más precisos.

* **Reproducción de trucos con velocidad de bits adaptable (ABR)**

Esta función permite que TVSDK cambie entre flujos de iFrame mientras se encuentra en modo de reproducción de trucos. Puede utilizar perfiles que no sean de iFrame para realizar el juego con trucos a velocidades más bajas.

* **Juego de trucos más suave**

Estas mejoras mejoran la experiencia del usuario:

・ Selección de velocidad de bits y velocidad de fotogramas adaptable durante la reproducción de trucos, según el ancho de banda y el perfil del búfer

・ Utilice el flujo principal en lugar del flujo IDR para obtener una reproducción rápida de hasta 30 fps.

* **Lógica de ABR mejorada**

La nueva lógica ABR se basa en la longitud del búfer, la velocidad de cambio de la longitud del búfer y el ancho de banda medido. Esto garantiza que el ABR elija la velocidad de bits correcta cuando el ancho de banda fluctúe y también optimiza el número de veces que el conmutador de velocidad de bits realmente se produce monitoreando la velocidad a la que cambia la longitud del búfer.

* **Facturación**

TVSDK recopila automáticamente métricas, de acuerdo con el contrato de venta del cliente, para generar informes de uso periódicos requeridos para fines de facturación. En todos los eventos de inicio de flujo, TVSDK utiliza la API de inserción de datos de Adobe Analytics para enviar métricas de facturación como, por ejemplo, tipo de contenido, marcas habilitadas para la inserción de anuncios y marcas habilitadas para drm (basadas en la duración del flujo facturable) al grupo de informes propiedad de Adobe Analytics Primetime. Esto no interfiere con los grupos de informes o las llamadas al servidor de Adobe Analytics del cliente ni se incluye en ellos. Si se solicita, este informe de uso de facturación se envía a los clientes de forma periódica. Esta es la primera fase de la función de facturación que admite únicamente la facturación de uso. Se puede configurar en función del contrato de venta mediante las API descritas en la documentación.

## Funciones admitidas {#supported-features}

TVSDK para Android 2.4 admite una serie de funciones que puede implementar para agregar funcionalidad a las aplicaciones de vídeo.

>[!NOTE]
>
>En las tablas de matriz de funciones que se muestran a continuación, un vínculo de ayuda significa que la función se admite en la versión actual.

### Características principales de reproducción {#core-playback-features}

| **Función** | **Tipo de contenido** | **HLS** | **DASH** |
|---|---|---|---|
| Reproducción general (Reproducir, Pausa, Buscar) | VOD + Activo | ♦ | ♦ (solo VOD) |
| FER: reproducción general (Reproducir, Pausa, Buscar) | FER VOD | ♦ | No admitido |
| MP3 | VOD | No admitido | No admitido |
| Reproducción de contenido MP4 | VOD | ♦ | ♦ |
| Lógica de conmutación de velocidad de bits adaptable | VOD + Activo | ♦ | No admitido |
| Reproducción solo de audio | VOD + Activo | ♦ | No admitido |
| Subtítulos opcionales - 608/708 | VOD + Activo | ♦ | ♦ (solo VOD) |
| Subtítulos opcionales - WebVTT | VOD + Activo | ♦ | ♦ (solo VOD) |
| Conmutación por error de manifiesto | VOD + Activo | ♦ | ♦ (solo VOD) |
| Failover avanzado | VOD + Activo | ♦ | ♦ (solo VOD) |
| Notificaciones de QoS y reproductor | VOD + Activo | ♦ | ♦ (solo VOD) |
| Compatibilidad con encabezados de cookie | VOD + Activo | ♦ | ♦ (solo VOD) |
| Compatibilidad con encabezados personalizados | VOD + Activo | No admitido | No admitido |
| Establecer parámetros de control de búfer | VOD + Activo | ♦ | ♦ (solo VOD) |
| Establecer controles de velocidad de bits adaptables | VOD + Activo | ♦ | ♦ (solo VOD) |
| Etiquetas de manifiesto personalizadas (HLS) / Flujos de Evento (DASH) | VOD + Activo | ♦ | ♦ (solo VOD) |
| Audio enlazado tardío | VOD + Activo | ♦ | ♦ (solo VOD) |
| 302 Redirección | VOD + Activo | ♦ | ♦ (solo VOD) |

### Características avanzadas de reproducción {#advanced-playback-features}

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
   <td>Live Live</td> 
   <td>♦</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Reproducción solo de audio</td> 
   <td>VOD + Activo</td> 
   <td>♦</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Reproducción de trucos </td> 
   <td>VOD + Activo</td> 
   <td>♦</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Reproducción suave de trucos (con ABR)</td> 
   <td>VOD + Activo</td> 
   <td>♦</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Análisis de ID3 (HLS) / Metadatos temporizados (DASH)</td> 
   <td>VOD + Activo</td> 
   <td>♦</td> 
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
   <td>♦</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Compatibilidad con los marcadores de discontinuidad (HLS) </li> 
     <li>Varios períodos (DASH)</li> 
    </ul> </td> 
   <td>VOD + Activo</td> 
   <td>♦</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Fiebre redireccionada</td> 
   <td>VOD + Activo</td> 
   <td>♦</td> 
   <td>♦ (solo VOD)</td> 
  </tr>
  <tr>
   <td>Anulación de miniaturas (Iframe y JPEG)</td> 
   <td>VOD + Activo</td> 
   <td>No admitido</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Integridad del flujo </td> 
   <td>VOD + Activo</td> 
   <td>♦</td> 
   <td>No admitido</td> 
  </tr>
 </tbody>
</table>

### Características principales del Ad Insertion (CSAI) {#core-ad-insertion-features-csai}

| **Función** | **Tipo de contenido** | **HLS** | **DASH** |
|---|---|---|---|
| Reproducción general, publicidades habilitadas | VOD + Activo | ♦ | ♦ (Solo prerolls de VOD) |
| Contenido FER con anuncios habilitados | VOD | ♦ | No admitido |
| Comportamientos de publicidad predeterminados | VOD + Activo | ♦ | ♦ (Solo prerolls de VOD) |
| VAST 2.0/3.0 | VOD + Activo | ♦ | ♦ (Solo prerolls de VOD) |
| VMAP 1.0 | VOD + Activo | ♦ | ♦ (Solo prerolls de VOD) |
| Publicidades MP4 | VOD + Activo | ♦ (de CRS) | ♦ (desde CRS, sólo versiones previas) |

### Funciones avanzadas de Ad Insertion (CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>Función</strong></td> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>DASH</strong></td> 
  </tr>
  <tr>
   <td>Reproducción de trucos con publicidades habilitadas</td> 
   <td>VOD + Activo</td> 
   <td>♦</td> 
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
   <td>♦</td> 
   <td>♦ (Solo prerolls de VOD)</td> 
  </tr>
  <tr>
   <td>Parámetros personalizados</td> 
   <td>VOD + Activo</td> 
   <td>♦</td> 
   <td>♦ (Solo prerolls de VOD)</td> 
  </tr>
  <tr>
   <td>Comportamientos de publicidad personalizados</td> 
   <td>VOD + Activo</td> 
   <td>♦</td> 
   <td>♦ (Solo prerolls de VOD)</td> 
  </tr>
  <tr>
   <td>Etiquetas de publicidad personalizadas</td> 
   <td>Live Live</td> 
   <td>♦ </td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Resoluciones de publicidad personalizadas</td> 
   <td>VOD + Activo</td> 
   <td>♦ </td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Resolución de publicidad personalizada FreeWheel</td> 
   <td>VOD</td> 
   <td>No admitido</td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Sustitución de anuncios C3 </td> 
   <td>VOD + Activo</td> 
   <td>♦ </td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Carga de publicidad diferida</td> 
   <td>VOD</td> 
   <td>♦ </td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Compatibilidad con los marcadores de discontinuidad - SSAI (HLS) </li> 
     <li>Varios períodos (DASH)</li> 
    </ul> </td> 
   <td>VOD + Activo</td> 
   <td>♦ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>Publicidades complementarias, publicidades tipo titular y publicidades en las que se puede hacer clic</td> 
   <td>VOD + Activo</td> 
   <td>♦ </td> 
   <td>♦ (Solo prerolls de VOD)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Activo</td> 
   <td>♦ (JS) </td> 
   <td>♦ (Solo prerolls de VOD)</td> 
  </tr>
  <tr>
   <td>Salida de publicidad anticipada</td> 
   <td>Live Live</td> 
   <td>♦ </td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>VOD creativa basada en reglas + prioridad en directo</td> 
   <td>VOD + Activo</td> 
   <td>♦ </td> 
   <td>No admitido</td> 
  </tr>
  <tr>
   <td>Reglas de CRS </td> 
   <td>VOD + Activo</td> 
   <td>♦ </td> 
   <td>No admitido</td> 
  </tr>
 </tbody>
</table>

## Funciones de protección de contenido {#content-protection-features}

| **Función** | **Tipo de contenido** | **HLS** | **DASH** |
|---|---|---|---|
| Cifrado AES | VOD + Activo | ♦ | ♦ (solo VOD) |
| Cifrado AES de muestra | VOD + Activo | ♦ |  |
| Flujos tokenizados | VOD + Activo | ♦ |  |
| DRM | VOD + Activo | Solo DRM de Primetime (Futuro: Widevine) | Solo Widevine |
| Reproducción externa (RBOP) | VOD + Activo | Solo DRM de Primetime | No admitido |
| Rotación de licencia | VOD + Activo | Solo DRM de Primetime | No admitido |
| Rotación de clave | VOD + Activo | Solo DRM de Primetime | No admitido |

### Características de integración {#integration-features}

| **Función** | **Tipo de contenido** | **HLS** | **DASH** |
|---|---|---|---|
| Integración con Adobe Analytics VHL | VOD + Activo | ♦ | ♦ |
| Facturación | VOD + Activo | ♦ | No admitido |

## Características no admitidas {#features-not-supported}

Esta versión de TVSDK no admite:

* Apagón de anuncios.
* Movimiento lento en juego de trucos.
* Buscar y jugar con contenido MP4.
* Inserción de anuncios con contenido principal MP4.
* Busque cuándo se está reproduciendo un anuncio.
* Reproducción de anuncios con medios solo de audio.

## Problemas y limitaciones conocidos {#known-issues-and-limitations}

Esta versión de TVSDK presenta los siguientes problemas:

* Específico del dispositivo (Samsung Galaxy Tab 4) bloquea VOD DRM LBA con auditud y hace clic en los anuncios
* El anuncio posterior no se reproduce para un contenido específico.
* No funciona establecer el rótulo de cierre en idiomas CJK.
* El vídeo puede salir del modo de truco automáticamente entre VOD y en directo.
* VHL: se envían llamadas de latidos incorrectas cuando se inicio un contenido desde un desplazamiento.
* Cuando se reproducen anuncios VPAID, faltan las llamadas de evento:type:play de Heartbeat en llamadas de VHL.
* El anuncio previo se reproduce incluso cuando se elige adBreakPolicy SKIP.
* Después de entrar en el reproductor de estado Completo, vuelve al estado Reproducción con SKIP adBreakPolicy para anuncios posteriores.

Sin vídeo, no hay ninguna dimensión de ventanilla móvil y, sin ella, no se puede mostrar ningún gráfico para los rótulos.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Información y soporte de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).