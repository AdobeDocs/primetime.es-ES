---
title: Notas de la versión de TVSDK 2.4.1 para Android
description: Las notas de la versión de TVSDK 2.4.1 para Android describen las funciones nuevas y admitidas, así como los problemas y limitaciones conocidos de TVSDK para Android 2.4.1.
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# Notas de la versión de TVSDK 2.4.1 para Android {#tvsdk-for-android-release-notes}

Las notas de la versión de TVSDK 2.4.1 para Android describen las funciones nuevas y admitidas, así como los problemas y limitaciones conocidos de TVSDK para Android 2.4.1.

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe lanza TVSDK 2.4.1 para Android.

Para utilizar esta versión de TVSDK, asegúrese de que su sistema cumple los requisitos descritos en [Requisitos del sistema](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

Aquí es donde puede encontrar la documentación:

· Sistema de ayuda en línea TVSDK 2.4 para Ayuda de Android

· [Javadocs TVSDK 2.4 para la API de Java de Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Los Javadocs son la autoridad final, ya que se generan automáticamente directamente a partir del código fuente de TVSDK.

· [Documentación de la API de C++ TVSDK 2.4 para la API de Android C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

Cada clase Java tiene una clase C++ correspondiente y la documentación de C++ contiene más material explicativo que Javadocs. Por lo tanto, consulte la documentación de C++ para obtener más información sobre la API de Java.

· Guía de migración ([Guía de migración de TVSDK 2.4 para Android](../migration-guides/tvsdk-14-25-android.md))

Esta guía explica lo que debe modificar para migrar una aplicación basada en TVSDK 1.4 a una basada en TVSDK 2.4.

## Nuevas funciones {#new-features}

TVSDK 2.4.1 para Android proporciona muchas mejoras de rendimiento con respecto a versiones anteriores. Proporciona una experiencia de visualización de alta calidad.

Esta versión incluye todas las funciones de las versiones 2.4 y 2.4.1, y ninguna función está en desuso.

Estas son las nuevas funciones clave de la versión 2.4.1:

* Funciones de la versión 4 de HLS

   * **Reproducción de vídeo** (reproducir, pausar, buscar) con el control del reproductor para emisiones en directo, lineales y de VOD.
   * **Subtítulos opcionales.** TVSDK puede mostrar subtítulos cerrados 608/708 con una selección de fuentes, tamaños de fuente, colores y fondo. También puede admitir vídeos con subtítulos resumidos y cambiar entre pistas de idioma si están disponibles.
   * **Modo de reproducción engañosa** admite avance y rebobinado rápido para flujos HLS que utilizan I-Frames. Todos los controles de reproducción de vídeo funcionan en el contenido. El modo de reproducción de vídeo externo a cámara lenta (hacia delante) tiene velocidades entre 0 y 1.
   * **Velocidad de bits adaptable (ABR)** permite que el reproductor seleccione dinámicamente cuál de las varias versiones del mismo flujo de contenido se reproducirá, en función de la red y otras condiciones. Puede definir parámetros de forma dinámica o en el archivo de manifiesto para seleccionar entre políticas de selección agresivas, moderadas y conservadoras.
   * **Intervalos de bytes** habilite un solo archivo TS para que contenga varios segmentos TS.
   * **Representaciones de audio alternativas** activar el reproductor para cambiar entre las pistas de audio disponibles.
   * **Compatibilidad con ID3.** TVSDK puede reproducir secuencias de audio y vídeo HLS que contengan metadatos de audio ID3, como el nombre del artista, el título y el álbum.
   * **Conmutación por error. **TVSDK utiliza estrategias para continuar la reproducción ininterrumpida, a pesar de los errores de los servidores host, los archivos de lista de reproducción y los segmentos.
   * **Transferencia de audio multicanal (DD+).** TVSDK puede pasar datos de audio Dolby Digital Plus (E-AC3) al hardware compatible.

* Funciones de protección de contenido

   * **DRM para HLS.** Todas las API de reproducción de vídeo funcionan con contenido de vídeo cifrado protegido por Acceso a Adobe. Se admiten las siguientes funciones de DRM:

      * Rotación de licencias
      * Rotación de clave
      * Almacenamiento en caché de licencias
      * Hora de la política
      * Rotación IV

* **Reproducción AES 128.** TVSDK puede reproducir contenido HLS estándar de cifrado avanzado (AES) con un tamaño de clave de 128 bits.
* **HLS protegido (PHLS)** proporciona un conjunto limitado de políticas DRM prediseñadas, un subconjunto de lo que proporciona Acceso desde Adobe, para habilitar DRM ligera a través de HLS para emisiones en directo y VOD.

* Contenido alternativo/publicitario y funciones de monetización

   * **Seguimiento de anuncios insertados en el servidor.** TVSDK puede rastrear las publicidades insertadas por el servicio de inserción de anuncios de Adobe Cloud. Admite anuncios lineales en los formatos VAST2, VAST3 y VMAP para VOD y emisiones en directo/lineales.
   * **Etiquetas HLS personalizadas.** TVSDK utiliza su `MediaPlayerConfig` para permitir notificar a la aplicación de reproducción cuando aparecen etiquetas HLS personalizadas en el flujo.
   * **Inserción de publicidad del lado del cliente.** La biblioteca de inserción de anuncios de Auditude funciona con los servidores de Adobe Auditude para resolver anuncios para su inserción de forma dinámica en contenido en directo, lineal y VOD, en posiciones anteriores, intermedias o posteriores a la emisión.
   * **Resoluciones de anuncios personalizadas.** El `ContentResolver, OpportunityGenerator,` y `MediaPlayerClientFactory` Las interfaces de le permiten implementar una resolución de contenido personalizada y/o alternativa y registrar un detector de oportunidades personalizado para trabajar con TVSDK. El `TestAdResolver` y `AuditudeResolver` Las clases de proporcionan ejemplos en C++ de cómo implementar un solucionador de contenido. Puede encontrar un ejemplo de Javascript en `samples/jspsdk/testapp/psdk.js`.
   * **Comportamiento de publicidad coherente.** Utilice el `AdPolicySelector` para permitir un comportamiento coherente en todos los reproductores para operaciones como búsqueda y trucos cuando los anuncios están presentes en el contenido. Si no implementa los suyos propios, TVSDK utiliza `DefaultAdPolicySelector`.
   * **Eliminar/reemplazar anuncios C3.** Utilice la API de TVSDK adecuada para eliminar intervalos de contenido personalizados e insertar dinámicamente nuevos anuncios sin necesidad de realizar trabajos de preparación adicionales. Esto resulta muy útil cuando se emite contenido lineal o en directo, y se pone inmediatamente a disposición del usuario a petición y sin necesidad de limpieza.

Estas son las nuevas funciones clave de la versión 2.4:

* **Instantáneo para VOD y en directo** Cuando se activa el inicio instantáneo, el TVSDK inicializa y almacena en búfer el contenido antes de que comience la reproducción. Ya que puede iniciar varios `MediaPlayerItemLoader` instancias simultáneamente en segundo plano, puede almacenar en búfer varias secuencias. Cuando un usuario cambia el canal y el flujo se ha almacenado en búfer correctamente, la reproducción en el nuevo canal se inicia inmediatamente. TVSDK 2.4 también es compatible con Instant On para emisiones en directo. Los flujos en directo se vuelven a almacenar en búfer cuando se mueve la ventana en directo.

* **Mejoras de rendimiento **La nueva arquitectura de TVSDK 2.4 ofrece varias mejoras de rendimiento:

   * **Subsegmentación** : TVSDK reduce aún más el tamaño de cada fragmento para iniciar la reproducción lo antes posible.
   * **Descargas de anuncios paralelos** : TVSDK recupera previamente los anuncios en paralelo a la reproducción del contenido antes de llegar a la pausa publicitaria, lo que permite una reproducción perfecta de los anuncios y el contenido.
   * **Resolución de anuncio diferida** : Con esta función, no esperamos la resolución de anuncios que no sean previos a la emisión antes de iniciar la reproducción, lo que reduce el tiempo de inicio. Las API como seek y trick-play siguen sin estar permitidas hasta que se resuelvan todos los anuncios.

* **Reproducción de contenido MP4**

Esta versión de TVSDK admite la reproducción de MP4 como contenido principal.

* **Conexiones de red persistentes**

TVSDK mantiene un conjunto de conexiones de red reutilizables, por lo que no incurre en la sobrecarga de crear y destruir una conexión de red para cada solicitud de red.

* **Protección de salida basada en resolución**

Esta función vincula las restricciones de reproducción a resoluciones específicas, proporcionando controles DRM de grano más preciso.

* **Juego de trucos con velocidad de bits adaptable (ABR)**

Esta función permite a TVSDK cambiar entre flujos de iFrame en el modo de reproducción con trucos. Puede utilizar perfiles que no sean de iFrame para realizar trucos a velocidades más bajas.

* **Juego de truco más suave**

Estas mejoras mejoran la experiencia del usuario:

· Selección de velocidad de bits adaptable y velocidad de fotogramas durante el truco, según el ancho de banda y el perfil del búfer

· Utilice el flujo principal en lugar del flujo IDR para obtener una reproducción rápida de hasta 30 fps.

* **Lógica ABR mejorada**

La nueva lógica ABR se basa en la longitud del búfer, la velocidad de cambio de la longitud del búfer y el ancho de banda medido. Esto garantiza que ABR elija la velocidad de bits correcta cuando el ancho de banda fluctúa y también optimiza el número de veces que el conmutador de velocidad de bits realmente se produce al monitorizar la velocidad a la que cambia la longitud del búfer.

* **Factura**

TVSDK recopila automáticamente las métricas, cumpliendo con el contrato de ventas del cliente, para generar los informes de uso periódicos necesarios para la facturación. En cada evento de inicio de flujo, TVSDK utiliza la API de inserción de datos de Adobe Analytics para enviar métricas de facturación como tipo de contenido, indicadores habilitados de inserción de publicidad y indicadores habilitados para drm, en función de la duración del flujo facturable, al grupo de informes propiedad de Adobe Analytics Primetime. Esto no interfiere ni se incluye en los grupos de informes de Adobe Analytics del cliente ni en las llamadas al servidor. Si se solicita, este informe de uso de la facturación se envía periódicamente a los clientes. Esta es la primera fase de la función de facturación que solo admite la facturación de uso. Se puede configurar en función del contrato de venta utilizando las API descritas en la documentación.

## Funciones compatibles {#supported-features}

TVSDK para Android 2.4 admite una serie de funciones que puede implementar para agregar funcionalidad a las aplicaciones de vídeo.

>[!NOTE]
>
>En las tablas de la matriz de funciones que se muestran a continuación, una √ significa que la función es compatible con la versión actual.

### Funciones de reproducción principales {#core-playback-features}

| **Función** | **Tipo de contenido** | **HLS** | **GUIÓN** |
|---|---|---|---|
| Reproducción general (reproducir, pausar, buscar) | VOD + Activo | √ | √ (solo VOD) |
| FER: reproducción general (reproducción, pausa, búsqueda) | VOD FER | √ | No compatible |
| MP3 | VOD | No compatible | No compatible |
| Reproducción de contenido MP4 | VOD | √ | √ |
| Lógica de conmutación de velocidad de bits adaptable | VOD + Activo | √ | No compatible |
| Reproducción solo de audio | VOD + Activo | √ | No compatible |
| Subtítulos opcionales - 608/708 | VOD + Activo | √ | √ (solo VOD) |
| Subtítulos - WebVTT | VOD + Activo | √ | √ (solo VOD) |
| Conmutación por error de manifiesto | VOD + Activo | √ | √ (solo VOD) |
| Conmutación por error avanzada | VOD + Activo | √ | √ (solo VOD) |
| QoS y notificaciones del reproductor | VOD + Activo | √ | √ (solo VOD) |
| Compatibilidad con encabezados de cookie | VOD + Activo | √ | √ (solo VOD) |
| Compatibilidad con encabezados personalizados | VOD + Activo | No compatible | No compatible |
| Establecer parámetros de control de búfer | VOD + Activo | √ | √ (solo VOD) |
| Establecer controles de velocidad de bits adaptables | VOD + Activo | √ | √ (solo VOD) |
| Etiquetas de manifiesto personalizadas (HLS) / Flujos de eventos (DASH) | VOD + Activo | √ | √ (solo VOD) |
| Audio de enlace tardío | VOD + Activo | √ | √ (solo VOD) |
| Redirección 302 | VOD + Activo | √ | √ (solo VOD) |

### Funciones de reproducción avanzadas {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>Función</strong></td> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>GUIÓN</strong></td> 
  </tr>
  <tr>
   <td>Reproducción con desplazamiento</td> 
   <td>Activo</td> 
   <td>√</td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Reproducción solo de audio</td> 
   <td>VOD + Activo</td> 
   <td>√</td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Juego de trucos </td> 
   <td>VOD + Activo</td> 
   <td>√</td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Juego de trucos suave (con ABR)</td> 
   <td>VOD + Activo</td> 
   <td>√</td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Análisis de ID3 (HLS) / Metadatos cronometrados (DASH)</td> 
   <td>VOD + Activo</td> 
   <td>√</td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Interrupciones </td> 
   <td>VOD + Activo</td> 
   <td>No compatible</td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Instant On</td> 
   <td>VOD + Activo</td> 
   <td>√</td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Soporte de marcador de discontinuidad (HLS) </li> 
     <li>Periodo múltiple (GUIÓN)</li> 
    </ul> </td> 
   <td>VOD + Activo</td> 
   <td>√</td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Adherencia de redirección 302</td> 
   <td>VOD + Activo</td> 
   <td>√</td> 
   <td>√ (solo VOD)</td> 
  </tr>
  <tr>
   <td>Eliminación de miniaturas (Iframe y JPEG)</td> 
   <td>VOD + Activo</td> 
   <td>No compatible</td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Integridad del flujo </td> 
   <td>VOD + Activo</td> 
   <td>√</td> 
   <td>No compatible</td> 
  </tr>
 </tbody>
</table>

### Funciones principales del Ad Insertion (CSAI) {#core-ad-insertion-features-csai}

| **Función** | **Tipo de contenido** | **HLS** | **GUIÓN** |
|---|---|---|---|
| Reproducción general, anuncios habilitados | VOD + Activo | √ | √ (solo en las versiones preliminares de VOD) |
| Contenido de FER con anuncios habilitados | VOD | √ | No compatible |
| Comportamientos de publicidad predeterminados | VOD + Activo | √ | √ (solo en las versiones preliminares de VOD) |
| VAST 2.0/3.0 | VOD + Activo | √ | √ (solo en las versiones preliminares de VOD) |
| VMAP 1.0 | VOD + Activo | √ | √ (solo en las versiones preliminares de VOD) |
| Anuncios MP4 | VOD + Activo | √ (de CRS) | √ (solo desde CRS, pre-rolls) |

### Funciones avanzadas de Ad Insertion (CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>Función</strong></td> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>GUIÓN</strong></td> 
  </tr>
  <tr>
   <td>Trick Play con anuncios habilitados</td> 
   <td>VOD + Activo</td> 
   <td>√</td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Solo anuncio </td> 
   <td>VOD</td> 
   <td>No compatible</td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Parámetros de segmentación</td> 
   <td>VOD + Activo</td> 
   <td>√</td> 
   <td>√ (solo en las versiones preliminares de VOD)</td> 
  </tr>
  <tr>
   <td>Parámetros personalizados</td> 
   <td>VOD + Activo</td> 
   <td>√</td> 
   <td>√ (solo en las versiones preliminares de VOD)</td> 
  </tr>
  <tr>
   <td>Comportamientos de publicidad personalizados</td> 
   <td>VOD + Activo</td> 
   <td>√</td> 
   <td>√ (solo en las versiones preliminares de VOD)</td> 
  </tr>
  <tr>
   <td>Etiquetas de publicidad personalizadas</td> 
   <td>Activo</td> 
   <td>√ </td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Resoluciones de anuncios personalizadas</td> 
   <td>VOD + Activo</td> 
   <td>√ </td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Freewheel Custom Ad Resolver</td> 
   <td>VOD</td> 
   <td>No compatible</td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Sustitución de anuncio C3 </td> 
   <td>VOD + Activo</td> 
   <td>√ </td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Carga diferida de publicidad</td> 
   <td>VOD</td> 
   <td>√ </td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Soporte de marcador de discontinuidad - SSAI (HLS) </li> 
     <li>Periodo múltiple (GUIÓN)</li> 
    </ul> </td> 
   <td>VOD + Activo</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>Anuncios complementarios, anuncios de banner y anuncios en los que se puede hacer clic</td> 
   <td>VOD + Activo</td> 
   <td>√ </td> 
   <td>√ (solo en las versiones preliminares de VOD)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Activo</td> 
   <td>√ (JS) </td> 
   <td>√ (solo en las versiones preliminares de VOD)</td> 
  </tr>
  <tr>
   <td>Salida anticipada del anuncio</td> 
   <td>Activo</td> 
   <td>√ </td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Creative VOD basado en reglas + Priorización en directo</td> 
   <td>VOD + Activo</td> 
   <td>√ </td> 
   <td>No compatible</td> 
  </tr>
  <tr>
   <td>Reglas CRS </td> 
   <td>VOD + Activo</td> 
   <td>√ </td> 
   <td>No compatible</td> 
  </tr>
 </tbody>
</table>

## Funciones de protección de contenido {#content-protection-features}

| **Función** | **Tipo de contenido** | **HLS** | **GUIÓN** |
|---|---|---|---|
| Cifrado AES | VOD + Activo | √ | √ (solo VOD) |
| Ejemplo de cifrado AES | VOD + Activo | √ |  |
| Flujos Tokenizados | VOD + Activo | √ |  |
| DRM | VOD + Activo | Solo DRM de Primetime (futuro: Widevine) | Solo Widevine |
| Reproducción externa (RBOP) | VOD + Activo | Solo DRM de Primetime | No compatible |
| Rotación de licencia | VOD + Activo | Solo DRM de Primetime | No compatible |
| Rotación de clave | VOD + Activo | Solo DRM de Primetime | No compatible |

### Funciones de integración {#integration-features}

| **Función** | **Tipo de contenido** | **HLS** | **GUIÓN** |
|---|---|---|---|
| Integración de VHL de Adobe Analytics | VOD + Activo | √ | √ |
| Factura | VOD + Activo | √ | No compatible |

## Funciones no admitidas {#features-not-supported}

Esta versión de TVSDK no admite:

* Apagón de anuncios.
* Cámara lenta en el juego de trucos.
* Búsqueda y trucos con contenido MP4.
* Inserción de publicidad con contenido principal de MP4.
* Busca cuándo se está reproduciendo un anuncio.
* Reproducción de anuncios con medios de solo audio.

## Problemas y limitaciones conocidos {#known-issues-and-limitations}

Esta versión de TVSDK tiene los siguientes problemas:

* El dispositivo específico (Samsung Galaxy Tab 4) bloquea VOD DRM LBA con la audiencia y hace clic en los anuncios
* El anuncio posterior a la emisión no se reproduce para un contenido específico.
* No funciona la configuración del pie de ilustración en JDK.
* El vídeo puede salir del modo truco automáticamente entre VOD y en directo.
* VHL: se envían llamadas de latido incorrectas cuando iniciamos un contenido desde un desplazamiento.
* Cuando se reproducen anuncios VPAID, VHL Heartbeat llama a un evento:type:falta el anuncio de reproducción.
* El anuncio previo a la emisión se reproduce incluso cuando se elige OMITIR de adBreakPolicy.
* Después de entrar en el estado Completo, el reproductor vuelve al estado de Reproducción con SKIP adBreakPolicy para los anuncios posteriores a la emisión.

Sin vídeo, no hay ninguna dimensión de ventanilla móvil y, sin ella, no se puede mostrar ningún gráfico para los subtítulos.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
