---
title: Uso de línea de comandos
description: Uso de línea de comandos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# Uso de línea de comandos {#command-line-usage}

Antes de usar el Administrador de directivas, asegúrese de cumplir los requisitos enumerados en Requisitos.

El Gestor de políticas se encuentra en [!DNL \Reference Implementation\Command Line Tools] en el DVD. Para ejecutar la herramienta, utilice la siguiente sintaxis:

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

La siguiente tabla contiene descripciones de las acciones de la línea de comandos mostradas en la sintaxis anterior:

| Acción de línea de comandos | Descripción |
|---|---|
| `new` | Crea una directiva nueva. |
| `detail` | Describe una directiva existente. |
| `update` | Actualiza una directiva existente. |

En la tabla siguiente se describen las opciones de línea de comandos que se pueden especificar junto con la sintaxis anterior:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción de línea de comandos </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c archivoDeConfiguración </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica la ubicación del archivo de configuración. Si no se utiliza esta opción, el Administrador de directivas buscará <span class="filepath"> flashaccesstools.properties </span> en el directorio de trabajo. Las opciones especificadas en la línea de comandos tienen prioridad sobre las presentes en el archivo de configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si el archivo de destino ya existe, sobrescribirlo sin preguntar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si el archivo de destino debe sobrescribirse. Si el archivo de destino ya existe y <span class="codeph"> -o </span> no se ha configurado, se devolverá un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que la directiva tiene una licencia de raíz. No se permite para las actualizaciones. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e fecha </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha antes de la cual las licencias serán válidas. Especificar como <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span>. Por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008. El valor debe ser mayor que el valor de <span class="codeph"> -s </span>, si está presente. Esta opción no se puede utilizar con <span class="codeph"> -r </span>. Para eliminar la fecha de finalización al actualizar una directiva, utilice <span class="codeph"> -e </span> sin especificar una fecha. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minutos </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La duración (en minutos) de la protección del contenido con esta política es válida, a partir del momento en que el contenido se protege con el empaquetador. El valor no debe ser negativo. Esta opción no se puede utilizar con <span class="codeph"> -e </span>. Para eliminar la duración al actualizar una directiva, utilice <span class="codeph"> -r </span> sin especificar un número de minutos. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s fecha </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha a partir de la cual las licencias serán válidas. Especificar como <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span>. Por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008. El valor debe ser menor que el valor de <span class="codeph"> -e </span>, si está presente. Esta opción no se puede utilizar con <span class="codeph"> -r </span>. Para eliminar la fecha de inicio al actualizar una directiva, utilice <span class="codeph"> -s </span> sin especificar una fecha. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w minutos </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La ventana de reproducción (el número de minutos que se puede ver el contenido desde la primera reproducción). Si no se especifica esta opción o si <span class="codeph"> -w </span> se utiliza sin especificar el número de minutos, no hay limitación de ventana de reproducción. El valor no debe ser negativo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minutos </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La duración del almacenamiento en caché de licencias en minutos, que es el tiempo que se permitirá que una licencia se almacene en caché en el almacén de licencias del cliente después de que el servidor haya emitido la licencia. El valor no debe ser negativo. Especificar <span class="codeph"> -l 0 </span> para indicar que no se permite el almacenamiento en caché de licencias. Uso <span class="codeph"> -l </span> sin especificar un número de minutos para el almacenamiento en caché de licencias ilimitado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate fecha </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha de finalización del almacenamiento en caché de licencias (la fecha a partir de la cual las licencias no se pueden almacenar en caché en el almacén de licencias del cliente, después de que el servidor haya emitido la licencia). Especificar como <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span><i class="+ topic/ph hi-d/i "> </i>o<i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span>. Por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008. Uso <span class="codeph"> -l </span> sin especificar un número de minutos para el almacenamiento en caché de licencias ilimitado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El área de nombres de autenticación. Si se especifica, el cliente debe autenticarse con un nombre de usuario y una contraseña emitidos por la autoridad especificada. Esta opción no se puede utilizar con <span class="codeph"> -x </span>. No se permiten las actualizaciones. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Permitir acceso anónimo. Esta opción no se puede utilizar con <span class="codeph"> -authNS </span>. No se permiten las actualizaciones. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> min </span>]:[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Una lista de permitidos de aplicaciones de AIR permitidas para reproducir contenido protegido. Use esto para restringir qué editores, aplicaciones y versiones pueden acceder al contenido protegido con esta directiva. </p> <p class="- topic/p ">If <i class="+ topic/ph hi-d/i ">appId</i> no se ha especificado, todas las aplicaciones de publisher <i class="+ topic/ph hi-d/i ">pubId</i> están permitidas. </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">min</i> y <i class="+ topic/ph hi-d/i ">max</i> los números de versión son opcionales. </p> <p class="- topic/p ">Múltiple <span class="codeph"> -air </span> se pueden especificar opciones para permitir varias aplicaciones. Si no se especifica ninguna aplicación de AIR o de SWF, todas las aplicaciones pueden acceder a este contenido. Durante una actualización, utilice -air sin los argumentos restantes para quitar todas las entradas de la lista. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist name </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> valor </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pares </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los clientes de DRM tienen restringido el acceso al contenido protegido. El valor está formado por pares nombre:valor separados por comas con el siguiente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> so | release= stringValue </span> </p> <p class="- topic/p ">Por ejemplo, <span class="codeph"> os=Win,release=2.0.1 </span>. Durante una actualización, utilice <span class="codeph"> -drmBlacklist </span> sin los argumentos restantes para quitar todas las entradas de la lista. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que los clientes de DRM deben tener el nivel de seguridad mínimo especificado para acceder al contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | OBLIGATORIO | NO_PLAYBACK | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restricciones de protección de salida analógica. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | OBLIGATORIO | NO_PLAYBACK </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restricciones de protección de salida digital. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> Nombre de -runtimeBlacklist </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> valor </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pares </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los tiempos de ejecución de la aplicación restringieron el acceso al contenido protegido. El valor está formado por pares nombre:valor separados por comas con el siguiente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> so | aplicación | release= stringValue </span> </p> <p class="- topic/p ">Por ejemplo, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. Durante una actualización, utilice <span class="codeph"> -runtimeBlacklist </span> sin los argumentos restantes para quitar todas las entradas de la lista. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que los tiempos de ejecución de la aplicación deben tener el nivel de seguridad mínimo especificado para tener acceso al contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf archivo= archivo_swf </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lista de permitidos de aplicaciones de SWF permitidas para reproducir contenido protegido. Se pueden especificar varias opciones -swf para permitir varias aplicaciones. Si no se especifica ninguna aplicación de AIR o de SWF, todas las aplicaciones pueden acceder a este contenido. Durante una actualización, utilice -swf sin los argumentos restantes para eliminar todas las entradas de la lista. Para identificar un SWF por su valor hash, especifique el archivo SWF para el que se va a calcular el hash y el tiempo máximo que se debe permitir para completar la verificación del SWF (en segundos). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k nombre= valor </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica las claves y los valores personalizados que se van a agregar a la directiva. Múltiple <span class="codeph"> -k </span> se pueden especificar opciones. Durante la actualización, utilice <span class="codeph"> -k </span> sin los argumentos restantes para quitar todas las propiedades. La interpretación o el manejo de estos datos depende completamente de la implementación del servidor de licencias de Acceso a Adobe. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p nombre= valor </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Agrega una propiedad personalizada, que aparecerá en la licencia generada para cada cliente. Múltiple <span class="codeph"> -p </span> se pueden especificar opciones para agregar varias propiedades. Durante una actualización, utilice <span class="codeph"> -p </span> sin los argumentos restantes para quitar todas las propiedades. La interpretación o el manejo de estos datos depende completamente de la implementación de la aplicación del cliente. </p> </td> 
  </tr> 
 </tbody> 
</table>
