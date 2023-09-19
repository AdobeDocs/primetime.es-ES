---
title: Notas de la versión de PTAI 19.11.1
description: Las notas de la versión 19.11.1 de PTAI describen las novedades o los cambios, los problemas resueltos y conocidos en Primetime Ad Insertion en 2019.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 0%

---

# Notas de la versión de Primetime Ad Insertion 19.11.1

Las notas de la versión 19.11.1 del Ad Insertion de Primetime describen las novedades o los cambios, los problemas resueltos y los problemas conocidos de Primetime Ad Insertion en el año 2019.

## Novedades de PTAI 19.11.1

**Cuándo:** Lunes, 4 de noviembre de 2019 a las 12:01 AM a 01:00 AM ORIENTAL

Actualizaciones de mantenimiento.

## Cambios en versiones anteriores

### Versión 19.10.2

**Cuándo:** Jueves, 31 de octubre de 2019 de 01:00 AM a 03:00 AM Este

Actualizaciones de mantenimiento.

### Versión 19.10.1

**Cuándo:**  Martes, 22 de octubre a las 01:00 AM a las 02:00 AM EASTERN

Actualizaciones de mantenimiento.

### Versión 19.9.1

**Cuándo:** Martes, 10 de septiembre de 2019 a las 12:30 a.m. hasta las 2:00 a.m., hora del este

Actualizaciones de seguridad

### Versión 19.8.3

**Cuándo:** Miércoles, 28 de agosto de 2019, 12:30 am - 01:30 am ESTE

Se ha corregido un error por el cual los reproductores de Chromecast salían de la reproducción inesperadamente cuando los segmentos de anuncios salían de la ventana del DVR.

### Versión 19.8.2

**Cuándo:** Miércoles, 21 de agosto de 2019 2:00 AM a 3:00 AM hora del este

* Panel de SAI: sección Estado de la sesión. Puede exportar los eventos de sesión mediante la opción Descargar CSV.

* Actualizaciones de mantenimiento

### Versión 19.8.1

**Cuándo:** Martes, 6 de agosto de 2019 2:30 AM Hora del Este a martes, 6 de agosto de 2019 4:30 AM Hora del Este

* Panel de SAI: se ha añadido una nueva sección, Estado de la sesión, al panel de SAI
   * Si tiene el ID de sesión de una sesión de SSAI que tenía habilitado el modo de depuración (ptdebug=true), podrá buscar la siguiente actividad que se produjo en esa sesión:
      * Solicitudes/respuestas de publicidad
      * Anuncios insertados
      * Balizas activadas (solo seguimiento del lado del servidor)

   * Puede buscar la actividad de un ID de sesión específico hasta 30 días después de que se haya realizado esa sesión de SSAI
   * Puede exportar los eventos
* Base de datos: actualizaciones de seguridad

### Versión 19.7.1

**Cuándo:** Miércoles, 10 de julio

* SSAI: Para valores de formato de secuencia de comandos que admiten la señalización de interrupción de anuncios EXT-X-CUE-OUT en secuencias activas, se ha agregado una macro genérica para pasar datos de atributos en la etiqueta EXT-X-ASSET Ejemplo: Etiqueta que acompaña a la etiqueta #EXT-X-CUE-OUT: #EXT-X-ASSET:CAID=75BCD15,GENRE=News,Program=NewsAt10 Macros: # se puede utilizar para pasar Noticias (del atributo GENRE) a una llamada de anuncio La URL # se puede utilizar para pasar NewsAt10 (del atributo Program) a una llamada de anuncio Excepción: Por compatibilidad con versiones anteriores #, # y # tienen la misma funcionalidad. Ambas macros se pueden utilizar para pasar el valor del atributo CAID, después de convertir el valor de hex a long. El valor long se 123456789 para el valor hex, 75BCD15, en el ejemplo anterior. Ambas macros se utilizarían para pasar 123456789 a una URL de llamada de anuncio. La macro siempre empieza por #. La macro distingue entre mayúsculas y minúsculas, pero el atributo de la etiqueta EXT-X-ASSET no. Es decir, PROGRAM y Program están permitidos en la etiqueta EXT-X-ASSET
* SSAI: cambios de configuración para un cliente específico para lo siguiente:
   * Ventana deslizante (lista de reproducción en directo) de cuatro minutos
   * Si se produce una excepción de tiempo de espera de socket cuando el servidor de manifiesto obtiene contenido de origen, el servidor de manifiesto devolverá el código de respuesta HTTP (404) en lugar de 500
* Actualizaciones de seguridad

### Versión 19.6.1

**Cuándo:** Miércoles, 12 de junio de 2019 11:30 PST a jueves, 13 de junio de 2019 12:30 AM PST

* CRS: Regla de normalización para creativos de RevJet
   * Se ha añadido la regla de normalización de URL creativa para RevJet, utilizada por CRS y SSAI
   * TVSDK: Si sirve o planea publicar anuncios desde RevJet, será necesario agregar reglas de normalización al JSON de reglas de CRS para utilizar CRS con sus creativos. Hable con el administrador de cuentas técnico para obtener ayuda
* CRS: Regla de normalización para creativos de Innovid
   * Se ha añadido la regla de normalización de URL creativa para Innovid, utilizada por SSAI
   * La regla de normalización utilizada por CRS se añadió en una versión anterior
   * TVSDK: La regla de normalización que se va a añadir en las reglas CRS JSON se proporcionó después de una versión anterior, pero para mayor seguridad, póngase en contacto con su administrador de cuentas técnico para revisar todas las reglas de normalización que tenga en vigor.
     >[!NOTE]
     >
     >La mayoría de las URL creativas de Innovid se transcodificarán y vincularán correctamente sin la regla de normalización. En ocasiones, sin embargo, se encuentran URL creativas de Innovid con parámetros dinámicos. La regla de normalización es necesaria para gestionar estas instancias.

### Versión 19.5.2

**Cuándo:** Miércoles, 22 de mayo 2:30 AM Hora del Este a miércoles, 22 de mayo 4:30 AM Hora del Este

* Se ha agregado compatibilidad con CMAF (contenido HLS/fMP4)
   * SSAI: Controlar manifiestos de CMAF
   * SSAI: iniciar solicitudes de transcodificación y recuperar recursos CRS según el formato de contenido (HLS/ts y HLS/fMP4)
   * CRS: Flujo de trabajo agregado para volver a empaquetar anuncios en formato CMAF (HLS/fMP4)
* SSAI: se ha corregido un problema que impedía que los anuncios sin mezclar se insertaran en contenido sin mezclar, cuando tanto el contenido como el anuncio no tenían secuencias de solo audio (EXT-X-STREAM-INF)
* SSAI: Compatibilidad añadida para tokens de autenticación de CDN de Limelight (LNW) para segmentos de contenido
   * Cuándo `pttoken=limelight` o `pttoken=llnw` se añade a la URL de bootstrap, añadiremos un encabezado secreto al recuperar la lista de reproducción maestra de origen, luego adjuntaremos los parámetros de Adobe del encabezado X-Sign de LLNW a los segmentos de contenido
* SSAI: Se ha agregado otro valor de token de tiempo (`pttoken=centurylink`) para la compatibilidad con tokens de autenticación de CDN de CenturyLink, publicada el 30 de julio de 2018
   * `pttoken=centurylink` tiene el mismo comportamiento que `pttoken=level3`y ambos valores son válidos

### Versión 19.5.1

**Cuándo:** Jueves, 9 de mayo 2:30 AM Hora del Este a jueves, 9 de mayo 4:30 AM Hora del Este

* SSAI: Actualizaciones de seguridad
* Panel de CRS: se ha truncado la cadena &quot;Muestra de FqAdId&quot; a 255 caracteres debido a restricciones de almacenamiento de datos (8 bits)
   * La cadena &quot;Muestra de FqAdId&quot; incluye el sistema de anuncios y el ID de anuncio de cada respuesta XML en la cadena del envoltorio del anuncio para inserciones de todos los anuncios CRS con SSAI (sección Estadísticas creativas del panel CRS)
* Paneles de SAI y CRS: Actualizaciones de la versión del software

### Versión 19.4.1

**Cuándo:** Miércoles, 10 de abril 2:30 AM Hora del Este a miércoles, 10 de abril 4:30 AM Hora del Este

* CRS: La API de reempaquetado de CRS ya no admitirá comandos del POST HTTP. La API de reempaquetado de CRS redirecciona automáticamente los comandos del POST HTTP (301) a HTTPS
   * A partir del 20 de mayo, la redirección HTTP->HTTPS para comandos del POST HTTP se desactivará
   * Si utiliza la API de reempaquetado de CRS para reempaquetar anuncios por adelantado, cambie los comandos del POST a HTTPS para el 20 de mayo
* CRS: Se ha rediseñado la arquitectura y el flujo de trabajo para cargar recursos CRS en los orígenes de CDN de los clientes
   * Los procesos de trabajo por origen de CDN están separados, por lo que los cuellos de botella de carga para un origen de CDN no afectarán a las cargas a otros orígenes de CDN
   * Otras ventajas: Se mejoran los tiempos de procesamiento de trabajos de CRS y las tasas de carga en los orígenes de CDN de los clientes
* SSAI: se han agregado las URL de rastreo de clics y clics para los anuncios de vídeo al formato JSON v2 del sidecar
   * Una nueva propiedad de matriz JSON, &quot;videoClicks&quot;, seguirá la propiedad &quot;trackingURLs&quot;
   * Los nombres de los valores de &quot;evento&quot; serán &quot;clickThrough&quot; y &quot;clickTracking&quot;, y no tendrán un valor startTime
* SSAI: para los recursos CRS, se ha agregado la funcionalidad para ampliar la caducidad del registro de búsqueda de un recurso CRS en 30 días cada vez que se inserta
   * Comportamiento anterior: Los registros de búsqueda de recursos CRS se almacenan en memcache en cada pod. Los registros de búsqueda de recursos CRS se eliminan automáticamente 30 días después de agregarse a memcache. Para volver a rellenar el registro de búsqueda de recursos CRS de un creativo en un pod después de que se haya eliminado de memcache, ese creativo debe encontrarse 3 veces en ese pod
   * Nuevo comportamiento: Cuando un pod accede a un registro de búsqueda de recursos CRS para insertar el recurso CRS, la caducidad del registro de búsqueda de recursos CRS se amplía en 30 días en ese pod. Como resultado, los recursos CRS que se utilizan con frecuencia no se eliminarán de la memoria caché de un pod hasta 30 días después de su uso más reciente
   * El nuevo comportamiento abarca todo el sistema y se puede desactivar si se detecta una caída del rendimiento
* SSAI: comportamiento actualizado de manipulación de manifiestos de WebVTT solo para emisiones en directo
   * Comportamiento anterior: solo en el manifiesto WebVTT, elimine las etiquetas EXT-X-DISCONTINUITY que se insertarían antes de cada anuncio insertado y después del último segmento de la pausa publicitaria insertada
   * Nuevo comportamiento: Se ha añadido un nuevo parámetro, vttdisc, con valores aceptados de true y false, a la dirección URL de arranque de SAI
      * vttdisc=true: las etiquetas EXT-X-DISCONTINUITY se insertan en el manifiesto WebVTT antes de cada anuncio insertado y después del último segmento de la pausa publicitaria insertada, con el mismo comportamiento para los manifiestos de audio/vídeo y solo audio
      * vttdisc=false (igual que el comportamiento anterior): solo en el manifiesto WebVTT, elimine las etiquetas EXT-X-DISCONTINUITY que se insertarían antes de cada anuncio insertado y después del último segmento de la pausa publicitaria insertada
      * Si el parámetro vttdisc se omite o tiene un valor distinto de true/false, el valor predeterminado de vttdisc será true
* SSAI: Actualizaciones de seguridad y actualizaciones de la versión del software
   * Java: Se ha actualizado la versión de Java para que admita grupos de cifrado adicionales para las llamadas de publicidad activadas a través de TLS 1.2 (HTTPS)

### Versión 19.2.1

**Cuándo:** Miércoles, 20 de febrero de 2019 1:30 AM Hora del Este a miércoles, 20 de febrero de 2019 3:30 AM Hora del Este

* SSAI: se han agregado las URL de rastreo de clics y clics para los anuncios de vídeo al formato JSON v2 del sidecar
   * En la propiedad &quot;trackingURLs&quot;, sus nombres de valor &quot;event&quot; son &quot;clickthrough&quot; y &quot;clickTracking&quot;
   * Sus valores startTime serán el principio del anuncio
* SSAI: para los recursos CRS, se ha agregado la funcionalidad para ampliar la caducidad del registro de búsqueda de un recurso CRS en 30 días cada vez que se inserta
   * Comportamiento anterior: Los registros de búsqueda de recursos CRS se almacenan en memcache en cada pod. Los registros de búsqueda de recursos CRS se eliminan automáticamente 30 días después de agregarse a memcache. Para volver a rellenar el registro de búsqueda de recursos CRS de un creativo en un pod después de que se haya eliminado de memcache, ese creativo debe encontrarse 3 veces en ese pod
   * Nuevo comportamiento: Cuando un pod accede a un registro de búsqueda de recursos CRS para insertar el recurso CRS, la caducidad del registro de búsqueda de recursos CRS se amplía en 30 días en ese pod. Como resultado, los recursos CRS que se utilizan con frecuencia no se eliminarán de la memoria caché de un pod hasta 30 días después de su uso más reciente
   * El nuevo comportamiento abarca todo el sistema y se puede desactivar si se detecta una caída del rendimiento

* SSAI: Actualizaciones de la versión de software para NGINX y Kafka
   * NGINX y Kafka se utilizan para activar y rastrear URL del lado del servidor y transferir datos a los paneles de SAI y CRS
* CRS: Mejoras de rendimiento en el panel de CRS

### Versión de IU web

**Cuándo:** Miércoles, 13 de febrero, 4:00 AM - 4:30 AM Pacífico

**Qué:** Componente de IU web de Primetime y Decisioning

* Se ha corregido el problema de la interfaz de usuario del calendario que impedía al usuario seleccionar una fecha posterior al 31 de diciembre de 2018 en el componente de calendario mientras traficaba con una campaña o extraía un informe.

### Versión 19.1.2

**Cuándo:** Miércoles, 30 de enero de 2019 1:30 AM Hora del Este a miércoles, 30 de enero 3:30 AM Hora del Este

* SSAI: se ha actualizado la estructura de clave de búsqueda que SSAI utiliza para almacenar y recuperar recursos CRS, a fin de gestionar escenarios en los que los proveedores de publicidad tienen un ID de publicidad dinámico o un ID creativo para el mismo anuncio
   * Nueva estructura de clave de búsqueda: zona, URL creativa y parámetros de formato (duración del objetivo, formato de salida, CDN de destino)
   * Estructura clave de búsqueda antigua: Zona, Sistema de publicidad, ID de publicidad, ID de creativo, URL de creativo y parámetros de formato (duración de destino, formato de salida, CDN de destino)
   * Las claves de búsqueda de los recursos CRS existentes se actualizarán para que coincidan con la nueva estructura antes de la versión de producción, pero tenga en cuenta que podrían perderse los nuevos recursos transcodificados entre la actualización de claves de búsqueda y la versión de producción. Si es así, iniciarían una nueva solicitud de CRS la próxima vez que se encuentren después de la versión

* CRS: Se ha agregado la capacidad de lista de bloqueados/lista de permitidos de solicitudes CRS de sistemas de publicidad específicos, ID de publicidad, ID de creatividad, URL de creatividad o formato creativo

  >Nota
  >
  >El Adobe añadirá reglas de lista de bloqueados cuando se encuentren proveedores de publicidad con valores dinámicos (por ejemplo, parámetro dinámico en URL) para el mismo anuncio. Estas reglas de lista de bloqueados se desactivarán después de que el componente dinámico se resuelva, ya sea por el proveedor o a través de una regla de normalización.

   * Si desea agregar una lista de bloqueados o regla de lista de permitidos para su zona, póngase en contacto con el administrador de cuentas técnico para obtener ayuda.

### Versión 19.1.1

**Cuándo:** Miércoles, 9 de enero de 2019 1:30 AM Hora del Este a miércoles, 9 de enero 3:30 AM Hora del Este

* Se ha corregido un problema en el cual la interpretación errónea de los encabezados keepalive HTTP puede provocar un error al validar recursos creativos entrantes alojados en total-stream.net.
* Se ha corregido un problema por el cual las comillas simples (&#39;) y dobles (&quot;) en el ID de anuncio, el ID creativo y otros campos para una solicitud de reempaquetado hacen que la solicitud falle.
* Se ha cambiado a Java long (tipo de datos) para resolver un problema en el que alcanzar el límite int de Java de 2 147 483 647 en los valores de ID de trabajo de transcodificación provocaría que todas las solicitudes de reempaquetado fallaran.
* Optimizaciones de base de datos.

## Problemas resueltos

Cuando la resolución está asociada con un problema informado, se muestra una referencia de Zendesk. Por ejemplo, ZD#xxxxx.

**PTAI 19.7.1**

ZD#37503: las respuestas JSON para las reglas CRS se almacenan en caché para evitar solicitudes duplicadas.

## Problemas y limitaciones conocidos

**PTAI 19.7.1**

No se ha añadido ninguna nueva limitación.
