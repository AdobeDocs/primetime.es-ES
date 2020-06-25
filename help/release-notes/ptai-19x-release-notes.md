---
title: Notas de la versión de PTAI 19.11.1
description: Las notas de la versión de PTAI 19.11.1 describen las novedades o los cambios que se han producido en la inserción de publicidad dinámica de Primetime en el año 2019.
translation-type: tm+mt
source-git-commit: 369dc8d987f5d49467ec376d4df5ffc46ea6d36c
workflow-type: tm+mt
source-wordcount: '1974'
ht-degree: 0%

---


# Notas de la versión 19.11.1 de Primetime Dynamic Ad Insertion

Las notas de la versión de Inserción dinámica de publicidad 19.11.1 describen las novedades o los cambios, los problemas resueltos y los problemas conocidos en Inserción dinámica de publicidad en Primetime en el año 2019.

## Novedades de PTAI 19.11.1

**Cuando:** Lunes 4 de noviembre de 2019 a las 12:01 AM a la 01:00 AM ESTE

Actualizaciones de mantenimiento.

## Qué ha cambiado en versiones anteriores

### Versión 19.10.2

**Cuando:** Jueves 31 de octubre de 2019 de 01:00 a 03:00 AM Este

Actualizaciones de mantenimiento.

### Versión 19.10.1

**Cuando:**  Martes 22 de octubre a las 01:00 AM a las 02:00 AM ESTE

Actualizaciones de mantenimiento.

### Versión 19.9.1

**Cuando:** Martes 10 de septiembre de 2019 a las 12:30 AM a las 2:00 AM hora del Este

Actualizaciones de seguridad

### Versión 19.8.3

**Cuando:** Miércoles 28 de agosto de 2019, de las 12:30 a.m. a las 01:30 a.m.

Se corrigió un error en el cual los reproductores de Chromecast salieron inesperadamente de la reproducción cuando los segmentos de publicidad se desplegaban desde la ventana de DVR.

### Versión 19.8.2

**Cuando:** Miércoles 21 de agosto de 2019 de 2:00 a 3:00 AM hora del Este

* Panel de SSAI: Estadísticas de sesión. Puede exportar los eventos de sesión mediante la opción Descargar CSV.

* Actualizaciones de mantenimiento

### Versión 19.8.1

**Cuando:** Martes 6 de agosto de 2019 a las 2:30 AM hora del Este hasta el martes 6 de agosto de 2019 a las 4:30 AM hora del Este

* Panel de SSAI: Nueva sección Añadida, Estadísticas de sesión, al Panel de SSAI
   * Si tiene el ID de sesión para una sesión SSAI que tenía habilitado el modo de depuración (ptdebug=true), podrá buscar la siguiente actividad que se produjo en esa sesión:
      * Solicitudes de publicidad/respuestas
      * Publicidades insertadas
      * Señalizaciones activadas (solo seguimiento del lado del servidor)
   * Puede buscar una actividad para una ID de sesión específica hasta 30 días después de que se haya celebrado esa sesión de SSAI
   * Puede exportar los eventos
* Base de datos: Actualizaciones de seguridad

### Versión 19.7.1

**Cuando:** Miércoles, 10 de julio

* SSAI: Para valores ptcueformat que admiten la señalización de interrupción y salida EXT-X-CUE-OUT en flujos en directo, se ha añadido una macro genérica para pasar datos de atributos en el ejemplo de etiqueta EXT-X-ASSET: Etiqueta que acompaña a la etiqueta #EXT-X-CUE-OUT: #EXT-X-ASSET:CAID=75BCD15,GENRE=Noticias,Programa=Macros de NewsAt10: # se puede utilizar para pasar Noticias (desde el atributo GENRE) a una dirección URL de llamada de publicidad # para pasar NewsAt10 (desde el atributo Programa) a una excepción de dirección URL de llamada de publicidad: Para la compatibilidad con versiones anteriores, # y # tienen la misma funcionalidad. Ambas macros pueden utilizarse para pasar el valor del atributo CAID, después de convertir el valor de hex a long. El valor long es 123456789 para el valor hex, 75BCD15, en el ejemplo anterior. Ambas macros se utilizarían para pasar 123456789 a una dirección URL de llamada de publicidad. La macro siempre inicio con #. La macro distingue entre mayúsculas y minúsculas, pero el atributo de la etiqueta EXT-X-ASSET no lo hace. Es decir, tanto el PROGRAMA como el Programa están permitidos en la etiqueta EXT-X-ASSET
* SSAI: Cambios de configuración para un cliente específico para lo siguiente:
   * Duración de la ventana deslizante (lista de reproducción activa) de cuatro minutos
   * Si se produce una excepción de tiempo de espera de socket cuando el servidor de manifiesto obtiene el contenido de origen, el servidor de manifiesto devolverá el código de respuesta HTTP (404) en lugar de 500
* Actualizaciones de seguridad

### Versión 19.6.1

**Cuando:** Miércoles 12 de junio de 2019 11:30 PST a jueves 13 de junio de 2019 12:30 PST

* CRS: Regla de normalización para elementos creativos de RevJet
   * Regla de normalización de URL creativa Añadida para RevJet, utilizada por CRS y SSAI
   * TVSDK: Si proporciona o planea ofrecer anuncios de RevJet, será necesario agregar reglas de normalización al JSON de reglas de CRS para poder usar CRS con sus elementos creativos. Póngase en contacto con el administrador de cuentas técnicas para obtener ayuda
* CRS: Regla de normalización para los creativos de Innovid
   * Regla de normalización de URL creativa Añadida para Innovid, utilizada por SSAI
   * La regla de normalización utilizada por CRS se agregó en una versión anterior
   * TVSDK: La regla de normalización que se agregará en las reglas de CRS JSON se proporcionó después de una versión anterior, pero para ser seguro, comuníquese con el administrador técnico de cuentas para revisar todas las reglas de normalización que haya establecido.
      >[!NOTE]
      >
      >La mayoría de las direcciones URL creativas de Innovid se transcodificarán y vincularán correctamente sin la regla de normalización. Sin embargo, en ocasiones se encuentran las direcciones URL creativas Innovid con parámetros dinámicos. La regla de normalización es necesaria para gestionar estas instancias.

### Versión 19.5.2

**Cuando:** Miércoles 22 de mayo 2:30 AM Hora del Este a miércoles 22 de mayo 4:30 AM Hora del Este

* Compatibilidad Añadida con CMAF (contenido HLS/fMP4)
   * SSAI: Gestión de manifiestos CMAF
   * SSAI: Inicie solicitudes de transcodificación y recupere recursos de CRS según el formato de contenido (HLS/ts y HLS/fMP4)
   * CRS: Flujo de trabajo Añadido para volver a empaquetar anuncios en formato CMAF (HLS/fMP4)
* SSAI: Se ha corregido un problema que impedía que se insertaran anuncios sin muestrear en contenido no mixto cuando tanto el contenido como la publicidad no tenían flujos de solo audio (EXT-X-STREAM-INF)
* SSAI: Compatibilidad Añadida con tokens de autenticación CDN de Limelight (LLNW) para segmentos de contenido
   * Cuando `pttoken=limelight` o `pttoken=llnw` se agregue a la URL de arranque, agregaremos un encabezado secreto al recuperar la lista de reproducción maestra de origen y, a continuación, anexaremos los parámetros de consulta del encabezado X-Adobe-Sig de LLNW a los segmentos de contenido
* SSAI: Se Añadió otro valor pttoken (`pttoken=centurylink`) para la compatibilidad con autentificadores CDN CenturyLink, que se publicó el 30 de julio de 2018
   * `pttoken=centurylink` tiene el mismo comportamiento que `pttoken=level3`, y ambos valores son válidos

### Versión 19.5.1

**Cuando:** Jueves, 9 de mayo 2:30 AM hora del Este a jueves 9 de mayo 4:30 AM hora del Este

* SSAI: Actualizaciones de seguridad
* Panel CRS: Se ha truncado la cadena &quot;Ejemplo de FqAdId&quot; a 255 caracteres debido a restricciones de almacenamiento de datos (8 bits)
   * La cadena &quot;Ejemplo de FqAdId&quot; incluye el sistema de publicidad y la ID de publicidad de cada respuesta XML en la cadena de envoltorio de la publicidad para insertar todas las publicidades de CRS con SSAI (sección Estadísticas creativas del Panel de CRS)
* Paneles de SSAI y CRS: Actualizaciones de versiones de software

### Versión 19.4.1

**Cuando:** Miércoles 10 de abril 2:30 AM Hora del Este hasta miércoles 10 de abril 4:30 AM Hora del Este

* CRS: La API de reempaquetado de CRS ya no admitirá comandos HTTP POST. La API de reempaquetado de CRS redireccionará automáticamente (301) comandos HTTP POST a HTTPS
   * A partir del 20 de mayo, se desactivará la redirección HTTP->HTTPS para los comandos HTTP POST
   * Si utiliza la API de reempaquetado de CRS para volver a empaquetar anuncios con antelación, cambie los comandos POST a HTTPS antes del 20 de mayo
* CRS: Se ha rediseñado la arquitectura y el flujo de trabajo para cargar recursos de CRS en los orígenes de CDN de los clientes
   * Los procesos de trabajo por origen CDN están separados, por lo que los cuellos de botella de carga para un origen CDN no afectarán a las cargas a otros orígenes CDN
   * Otras ventajas: Se han mejorado los tiempos de procesamiento de trabajos de CRS y las tasas de carga en los orígenes de CDN de los clientes
* SSAI: Direcciones URL Añadidas de ClickThrough y ClickTracking para anuncios de vídeo al formato JSON v2 sidecar
   * Una nueva propiedad de matriz JSON, &quot;videoClicks&quot;, seguirá la propiedad &quot;trackingURLs&quot;
   * Los nombres de los valores &quot;evento&quot; serán &quot;clickThrough&quot; y &quot;clickTracking&quot;, y no tendrán un valor startTime
* SSAI: Para los recursos de CRS, se ha agregado la funcionalidad de ampliar la caducidad de un registro de búsqueda de recursos de CRS 30 días cada vez que se inserta
   * Comportamiento anterior: Los registros de búsqueda de recursos CRS se almacenan en memcache en cada pod. Los registros de búsqueda de recursos CRS se eliminan automáticamente 30 días después de agregarlos a memcache. Para volver a rellenar el registro de búsqueda de recursos CRS de un elemento creativo en un pod después de eliminarlo de la memoria caché, dicho elemento creativo debe encontrarse tres veces en ese pod
   * Nuevo comportamiento: Cuando un pod accede a un registro de búsqueda de recursos CRS para insertar el recurso CRS, la caducidad del registro de búsqueda de recursos CRS se ampliará 30 días en ese pod. Como resultado, los recursos de CRS que se utilizan con frecuencia no se eliminarán de la memoria caché de un pod hasta 30 días después de su uso más reciente
   * El nuevo comportamiento se aplica a todo el sistema y se puede desactivar si se detecta una caída de rendimiento
* SSAI: Se ha actualizado el comportamiento de manipulación de manifiestos de WebVTT solo para transmisiones en directo
   * Comportamiento anterior: Solo en el manifiesto WebVTT, elimine las etiquetas EXT-X-DISCONTINUITY que se insertarían antes de cada anuncio insertado y después del último segmento de la pausa publicitaria insertada
   * Nuevo comportamiento: Se ha Añadido un nuevo parámetro, vttdisk, con valores aceptados de true y false, en la URL de arranque de SSAI.
      * vttdisk=true: Las etiquetas EXT-X-DISCONTINUITY se insertarán en el manifiesto WebVTT antes de cada anuncio insertado y después del último segmento de la pausa publicitaria insertada, coincidiendo con el comportamiento de los manifiestos de solo audio/vídeo y audio
      * vttdisk=false (igual que el comportamiento anterior): Solo en el manifiesto WebVTT, elimine las etiquetas EXT-X-DISCONTINUITY que se insertarían antes de cada anuncio insertado y después del último segmento de la pausa publicitaria insertada
      * Si se omite el parámetro vttdisk o tiene un valor distinto de true/false, vttdisk pasará a ser true de forma predeterminada
* SSAI: Actualizaciones de seguridad y de versiones de software
   * Java: Se ha actualizado la versión de Java para admitir conjuntos de cifrado adicionales para llamadas de publicidad activadas a través de TLS 1.2 (HTTPS)

### Versión 19.2.1

**Cuando:** Miércoles 20 de febrero de 2019 1:30 AM Hora del Este hasta miércoles 20 de febrero de 2019 3:30 AM Hora del Este

* SSAI: Direcciones URL Añadidas de ClickThrough y ClickTracking para anuncios de vídeo al formato JSON v2 sidecar
   * Bajo la propiedad &quot;trackingURLs&quot;, sus nombres de valor &quot;evento&quot; serán &quot;pulsaciones&quot; y &quot;clickTracking&quot;
   * Sus valores startTime serán el comienzo de la publicidad
* SSAI: Para los recursos de CRS, se ha agregado la funcionalidad de ampliar la caducidad de un registro de búsqueda de recursos de CRS 30 días cada vez que se inserta
   * Comportamiento anterior: Los registros de búsqueda de recursos CRS se almacenan en memcache en cada pod. Los registros de búsqueda de recursos CRS se eliminan automáticamente 30 días después de agregarlos a memcache. Para volver a rellenar el registro de búsqueda de recursos CRS de un elemento creativo en un pod después de eliminarlo de la memoria caché, dicho elemento creativo debe encontrarse tres veces en ese pod
   * Nuevo comportamiento: Cuando un pod accede a un registro de búsqueda de recursos CRS para insertar el recurso CRS, la caducidad del registro de búsqueda de recursos CRS se ampliará 30 días en ese pod. Como resultado, los recursos de CRS que se utilizan con frecuencia no se eliminarán de la memoria caché de un pod hasta 30 días después de su uso más reciente
   * El nuevo comportamiento se aplica a todo el sistema y se puede desactivar si se detecta una caída de rendimiento

* SSAI: Actualizaciones de versiones de software para NGINX y Kafka
   * NGINX y Kafka se utilizan para activar direcciones URL de seguimiento de anuncios en el servidor y para enviar datos a los Paneles SSAI y CRS
* CRS: Mejoras en el rendimiento del Panel de CRS

### Versión de la interfaz de usuario web

**Cuando:** Miércoles 13 de febrero, 4:00 AM - 4:30 AM Pacífico

**Qué:** Componente de interfaz de usuario web de Primetime y Decisioning

* Se corrigió el problema de la interfaz de usuario del calendario en el cual el usuario no podía seleccionar una fecha posterior al 31 de diciembre de 2018 desde el componente de calendario mientras se enviaba una campaña o se extraía un informe.

### Versión 19.1.2

**Cuando:** Miércoles 30 de enero de 2019 1:30 AM Hora del Este hasta miércoles 30 de enero 3:30 AM Hora del Este

* SSAI: Se ha actualizado la estructura de clave de búsqueda que utiliza SSAI para almacenar y recuperar recursos de CRS, con el fin de controlar escenarios en los que los proveedores de publicidad tienen un ID de publicidad dinámico o un ID creativo para la misma publicidad
   * Nueva estructura de clave de búsqueda: Parámetros de zona, URL creativa y formato (duración del destinatario, formato de salida, CDN de destino)
   * Estructura de clave de búsqueda antigua: Zona, sistema de publicidad, ID de publicidad, ID creativo, URL creativa y parámetros de formato (duración del destinatario, formato de salida, CDN de destino)
   * Las claves de búsqueda de recursos CRS existentes se actualizarán para que coincidan con la nueva estructura antes de la versión de producción, pero tenga en cuenta que los nuevos recursos transcodificados entre la actualización de las claves de búsqueda y la versión de producción podrían perderse. En caso afirmativo, iniciarían una nueva solicitud de CRS la próxima vez que se encuentren después del lanzamiento

* CRS: Se ha Añadido la capacidad de bloquear/permitir solicitudes de CRS de lista de sistemas de publicidad específicos, ID de publicidad, ID creativos, URL creativas y/o formato creativo

   >Nota
   >
   >Adobe agregará reglas de lista de bloques cuando se encuentren proveedores de publicidad con valores dinámicos (por ejemplo, parámetro dinámico en la dirección URL) para la misma publicidad. Estas reglas de lista de bloques se desactivarán una vez resuelto el componente dinámico, ya sea por el proveedor o a través de una regla de normalización.

   * Si desea agregar una lista de bloques o permitir una regla de lista para su zona, comuníquese con el administrador técnico de cuentas para obtener ayuda.

### Versión 19.1.1

**Cuando:** Miércoles, 9 de enero de 2019 1:30 AM Hora del Este hasta miércoles, 9 de enero 3:30 AM Hora del Este

* Se corrigió un problema en el cual la interpretación errónea de los encabezados HTTP keep-live podía resultar en un error al validar los recursos creativos entrantes alojados en total-stream.net.
* Se corrigió un problema en el cual las comillas simples (&#39;) y las comillas de doble (&quot;) en ID de publicidad, ID creativo y otros campos para una solicitud de reempaquetado ocasionaban que la solicitud de reempaquetado fallara.
* Se ha cambiado a Java long (tipo de datos) para abordar un problema en el que si se alcanza el límite de Java int de 2.147.483.647 en la transcodificación de los valores de ID de trabajo, todas las solicitudes de reempaquetado fallarían.
* Optimizaciones de la base de datos.

## Problemas resueltos

Cuando la resolución está asociada a un problema informado, se muestra una referencia de Zendesk. Por ejemplo, ZD#xxxxx.

**PTAI 19.7.1**

ZD#37503 - Las respuestas de Json para las reglas de CRS se almacenan en caché para evitar las solicitudes de duplicado.

## Problemas y limitaciones conocidos

**PTAI 19.7.1**

No se ha agregado ninguna nueva limitación.
