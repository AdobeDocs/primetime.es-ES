---
title: Uso de la línea de comandos
description: Uso de la línea de comandos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---


# Uso de la línea de comandos {#command-line-usage}

Antes de usar el Administrador de políticas, asegúrese de cumplir los requisitos enumerados en Requisitos.

El Administrador de directivas se encuentra en el directorio [!DNL \Reference Implementation\Command Line Tools] del DVD. Para ejecutar la herramienta, utilice la siguiente sintaxis:

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

La siguiente tabla contiene descripciones de las acciones de línea de comandos que se muestran en la sintaxis anterior:

| Acción de línea de comandos | Descripción |
|---|---|
| `new` | Crea una directiva nueva. |
| `detail` | Describe una directiva existente. |
| `update` | Actualiza una directiva existente. |

En la tabla siguiente se describen las opciones de la línea de comandos que se pueden especificar junto con la sintaxis anterior:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción de línea de comandos </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica la ubicación del archivo de configuración. Si no se utiliza esta opción, el Administrador de directivas buscará <span class="filepath"> flashaccesstools.properties </span> en el directorio de trabajo. Las opciones especificadas en la línea de comandos tienen prioridad sobre las que están presentes en el archivo de configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si el archivo de destino ya existe, sobrescribirlo sin preguntar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si el archivo de destino debe sobrescribirse. Si el archivo de destino ya existe y <span class="codeph"> -o </span> no está configurado, se devuelve un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que la directiva tiene una licencia raíz. No se permiten actualizaciones. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e fecha  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha antes de la cual serán válidas las licencias. Especifique como <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span>. Por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008. El valor debe ser bueno que el valor de <span class="codeph"> -s </span>, si está presente. Esta opción no se puede usar con <span class="codeph"> -r </span>. Para eliminar la fecha de finalización al actualizar una directiva, utilice <span class="codeph"> -e </span> sin especificar una fecha. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minutos  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La duración (minutos) del contenido protegido con esta directiva es válida, comenzando cuando el contenido está protegido con el empaquetador. El valor debe ser no negativo. Esta opción no se puede usar con <span class="codeph"> -e </span>. Para eliminar la duración al actualizar una directiva, utilice <span class="codeph"> -r </span> sin especificar un número de minutos. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s fecha  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha después de la cual serán válidas las licencias. Especifique como <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span>. Por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008. El valor debe ser menor que el valor de <span class="codeph"> -e </span>, si está presente. Esta opción no se puede usar con <span class="codeph"> -r </span>. Para eliminar la fecha de inicio al actualizar una directiva, utilice <span class="codeph"> -s </span> sin especificar una fecha. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w minutos  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La ventana de reproducción (el número de minutos que puede verse el contenido, a partir de la primera reproducción). Si no se especifica esta opción o si se utiliza <span class="codeph"> -w </span> sin especificar el número de minutos, no hay limitación de la ventana de reproducción. El valor debe ser no negativo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minutos  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La duración del almacenamiento en caché de licencias en minutos, que es el tiempo en el que se permitirá que una licencia se almacene en caché en el almacén de licencias del cliente después de que el servidor haya emitido la licencia. El valor debe ser no negativo. Especifique <span class="codeph"> -l 0 </span> para indicar que el almacenamiento en caché de licencias no está permitido. Utilice <span class="codeph"> -l </span> sin especificar un número de minutos para el almacenamiento en caché de licencias ilimitado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha de finalización de la caché de licencias (la fecha después de la cual las licencias no se pueden almacenar en caché en el almacén de licencias del cliente, después de que el servidor haya emitido la licencia). Especifique como <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span><i class="+ topic/ph hi-d/i "> </i>o<i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span>. Por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008. Utilice <span class="codeph"> -l </span> sin especificar un número de minutos para el almacenamiento en caché de licencias ilimitado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El espacio de nombres de autenticación. Si se especifica, el cliente debe autenticarse con un nombre de usuario y una contraseña emitidos por la autoridad especificada. Esta opción no se puede usar con <span class="codeph"> -x </span>. No está permitido para actualizaciones. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Permitir acceso anónimo. Esta opción no se puede usar con <span class="codeph"> -authNS </span>. No está permitido para actualizaciones. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId  </span>[:  <span class="+ topic/ph pr-d/codeph codeph"> appId  </span>[:[  <span class="+ topic/ph pr-d/codeph codeph"> min  </span>]:[  <span class="+ topic/ph pr-d/codeph codeph"> max  </span>]]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lista de permitidos de aplicaciones de AIR permitidas para reproducir contenido protegido. Utilice esto para restringir qué editores, aplicaciones y versiones pueden acceder al contenido protegido con esta directiva. </p> <p class="- topic/p ">Si no se especifica <i class="+ topic/ph hi-d/i ">appId</i> , se permiten todas las aplicaciones para el editor <i class="+ topic/ph hi-d/i ">pubId</i>. </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Los números de </i> versión mínima de  <i class="+ topic/ph hi-d/i "></i> son opcionales. </p> <p class="- topic/p ">Se pueden especificar varias opciones <span class="codeph"> -air </span> para permitir varias aplicaciones. Si no se especifica ninguna aplicación AIR o SWF, todas las aplicaciones pueden acceder a este contenido. Durante una actualización, utilice -air sin los argumentos restantes para eliminar todas las entradas de la lista. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist nombre  </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> pares de  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> valor  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los clientes de DRM restringieron el acceso a contenido protegido. El valor consiste en pares de nombre:valor separados por comas con el siguiente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue  </span> </p> <p class="- topic/p ">Por ejemplo, <span class="codeph"> os=Win,release=2.0.1 </span>. Durante una actualización, utilice <span class="codeph"> -drmBlacklist </span> sin los argumentos restantes para eliminar todas las entradas de la lista. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que los clientes de DRM deben tener el nivel de seguridad mínimo especificado para acceder al contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | REQUERIDO | NO_PLAYBACK | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restricciones de protección de salida analógica. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | REQUERIDO | NO_PLAYBACK  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restricciones de protección de salida digital. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist nombre  </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> pares de  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> valor  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los tiempos de ejecución de la aplicación están restringidos para acceder a contenido protegido. El valor consiste en pares de nombre:valor separados por comas con el siguiente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | aplicación | release= stringValue  </span> </p> <p class="- topic/p ">Por ejemplo, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. Durante una actualización, utilice <span class="codeph"> -runtimeBlacklist </span> sin los argumentos restantes para eliminar todas las entradas de la lista. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que los tiempos de ejecución de la aplicación deben tener el nivel mínimo de seguridad especificado para acceder al contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url  </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf file= swf_file  </span>,  <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lista de permitidos de aplicaciones SWF permitidas para reproducir contenido protegido. Se pueden especificar varias opciones -swf para permitir varias aplicaciones. Si no se especifica ninguna aplicación AIR o SWF, todas las aplicaciones pueden acceder a este contenido. Durante una actualización, utilice -swf sin los argumentos restantes para eliminar todas las entradas de la lista. Para identificar un SWF por su valor hash, especifique el archivo SWF para el que desea calcular el hash y el tiempo máximo para permitir que se complete la verificación SWF (en segundos). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= value  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica las claves y los valores personalizados que se agregarán a la directiva. Se pueden especificar varias opciones <span class="codeph"> -k </span>. Durante la actualización, utilice <span class="codeph"> -k </span> sin los argumentos restantes para eliminar todas las propiedades. La interpretación o el manejo de estos datos depende completamente de la implementación del servidor de licencias de Adobe Access. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Agrega una propiedad personalizada que aparecerá en la licencia generada para cada cliente. Se pueden especificar varias opciones <span class="codeph"> -p </span> para agregar varias propiedades. Durante una actualización, utilice <span class="codeph"> -p </span> sin los argumentos restantes para eliminar todas las propiedades. La interpretación o gestión de estos datos depende completamente de la implementación de la aplicación cliente. </p> </td> 
  </tr> 
 </tbody> 
</table>

