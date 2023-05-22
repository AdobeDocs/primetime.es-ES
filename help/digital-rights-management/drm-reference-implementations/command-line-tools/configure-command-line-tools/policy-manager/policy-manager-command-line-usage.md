---
title: Uso de la línea de comandos del Administrador de directivas
description: Uso de la línea de comandos del Administrador de directivas
copied-description: true
exl-id: 888be282-7eaa-4101-b4b1-4f8df99a967a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 0%

---

# Uso de la línea de comandos del Administrador de directivas {#policy-manager-command-line-usage}

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

**Tabla 1: Comandos**

| Comando | Descripción |
|---|---|
| `new` | Crea una nueva directiva DRM |
| `detail` | Describe una directiva DRM existente |
| `update` | Actualiza una directiva DRM existente |

**Tabla 2: Opciones**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción de la línea de comandos </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c archivoDeConfiguración </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el nombre y la ubicación del archivo de configuración. </p> <p class="- topic/p ">Si no se especifica un nombre o una ubicación, el Gestor de políticas de DRM busca <span class="filepath"> flashaccesstools.properties </span> en el directorio de trabajo actual. </p> <p>Nota: Las opciones que especifique en la línea de comandos tienen prioridad sobre las opciones especificadas en el fichero de configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si existe el archivo de destino, puede sobrescribirlo sin que se le pregunte. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si el archivo de destino debe sobrescribirse. Si el archivo de destino existe y <span class="codeph"> -o </span> no se ha configurado, se produce un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que la directiva DRM tiene una licencia raíz. </p> <p class="- topic/p ">Esta opción no está disponible para actualizaciones. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e fecha </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha antes de que las licencias sean válidas. </p> <p>Puede especificar la fecha en <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span> formato. Por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008. </p> <p> 
     <ul id="ul_D5DB5044756D4BD6A734813971598425"> 
      <li id="li_B6BD62A524384060A9DDA14FF50936FA">El valor debe ser bueno al valor de <span class="codeph"> -s </span> si está presente. </li> 
      <li id="li_C3C5AD0231A240EC9AC57685B9206E8D">No puede aplicar esta opción con <span class="codeph"> -r </span>. </li> 
      <li id="li_3790E2F829A149979BF44E0914CFF431">Para eliminar la fecha de finalización al actualizar una directiva DRM, aplique <span class="codeph"> -e </span> sin especificar una fecha. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minutos </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Duración en minutos durante la cual el contenido protegido es válido. </p> <p class="- topic/p ">La política de DRM se vuelve válida cuando el contenido se protege con el empaquetador. </p> <p> 
     <ul id="ul_4690A0E4677A4DF6A006B7FCBD46F1BE"> 
      <li id="li_D1F098D44B494EE7A8647C0B62D5ACFA">El valor no debe ser negativo. </li> 
      <li id="li_ADFDCB01EEE04B37AFA42886AAEF47EB">No puede aplicar esta opción junto con <span class="codeph"> -e </span>. </li> 
      <li id="li_E80563E68BEB43FC9E29A694594CAE01">Para quitar o eliminar la duración al actualizar una directiva DRM, aplique <span class="codeph"> -r </span> sin especificar minutos. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s fecha </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha en la que las licencias pasan a ser válidas. </p> <p>Puede especificar la fecha en la variable <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span> formato. Por ejemplo, <span class="codeph"> 12-2008 </span> o <span class="codeph"> 12-1-00-2008:00:00 </span> para la medianoche del 1 de diciembre de 2008. </p> <p> 
     <ul id="ul_D52B337F547F4E7AB87FE025236CA930"> 
      <li id="li_DBAE380972434DB1A4EF20D399038AB8">El valor debe ser menor que el valor de <span class="codeph"> -e </span>, si está presente. </li> 
      <li id="li_2899EC5559CF44319A4AC4ECD90A5B9A">No puede aplicar esta opción junto con <span class="codeph"> -r </span>. </li> 
      <li id="li_19861B1A64E44B95B649948EAB3E4085">Para quitar o eliminar la fecha de inicio al actualizar una directiva DRM, utilice <span class="codeph"> -s </span> sin especificar una fecha. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w [&lt;minutes&gt;[,enableHS|disableHS]] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Ventana de reproducción, que es el número de minutos que se puede ver el contenido desde la primera reproducción. </p> <p>Si no se especifica, o si <span class="codeph"> -w </span> se utiliza sin especificar un número de minutos, no hay limitación de ventana de reproducción. El valor no debe ser negativo. </p> <p>El opcional <span class="codeph"> enableHS </span> o <span class="codeph"> disableHS </span> El indicador señala si se debe habilitar o deshabilitar la detención del hardware. El indicador indica si el contexto de descifrado se destruye al final de la ventana de reproducción (activada) o no se destruye (desactivada). </p> <p>Por ejemplo, para especificar que el contenido solo se pueda ver durante 60 minutos y requiera una detención forzada: 
     <codeblock>
       -w&amp;nbsp;60,habilitarHS 
     </codeblock> </p> <p>Nota:  <i>Parada dura</i> actualmente no es compatible con Flash Player, Android y iOS. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minutos </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La duración del almacenamiento en caché de licencias es el tiempo en minutos que una licencia se puede almacenar en caché en el almacén de licencias del cliente después de que el servidor haya emitido la licencia. El valor no debe ser negativo. </p> <p>Puede especificar <span class="codeph"> -l 0 </span> para indicar que no se permite el almacenamiento en caché de licencias. Para un almacenamiento en caché de licencias ilimitado, especifique <span class="codeph"> -l </span> sin minutos. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate fecha </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Fecha de finalización del almacenamiento en caché de licencias. </p> <p class="- topic/p ">Indica la fecha final en la que el cliente puede almacenar las licencias en caché en el almacén de licencias del cliente después de que el servidor DRM de Primetime haya emitido la licencia. </p> <p>Puede especificar la fecha en los siguientes formatos: 
     <ul id="ul_112DE7248A9C48B19520A3AA9E5D1F03"> 
      <li id="li_01C5400E78B84A3B8955972FBA875AAC"> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> </li> 
      <li id="li_AA13B1EFA07A4542A3DB41FA3320B143"> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span> </li> 
     </ul>Por ejemplo, <span class="codeph"> 12-2008 </span> o <span class="codeph"> 12-1-00-2008:00:00 </span> para la medianoche del 1 de diciembre de 2008. Debe realizar la solicitud <span class="codeph"> -l </span> sin especificar minutos para el almacenamiento en caché de licencias ilimitado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El área de nombres de autenticación. </p> <p class="- topic/p ">Si aplica esta opción, el cliente debe introducir un nombre de usuario y una contraseña emitidos por la autoridad especificada. </p> <p>No puede aplicar esta opción junto con <span class="codeph"> -x </span>. </p> <p>Esta opción no está permitida para actualizaciones. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Permitir acceso anónimo. </p> <p class="- topic/p ">No puede aplicar esta opción junto con <span class="codeph"> -authNS </span>. </p> <p class="- topic/p ">Esta opción no está permitida para actualizaciones. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> min </span>]:[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Una lista de permitidos de aplicaciones de AIR que pueden reproducir contenido protegido. </p> <p class="- topic/p ">Puede aplicar esta opción para restringir qué editores, aplicaciones y versiones pueden acceder al contenido protegido con esta directiva DRM. </p> <p class="- topic/p ">Si no especifica lo siguiente <i class="+ topic/ph hi-d/i ">appId</i>, todas las aplicaciones para publicador <i class="+ topic/ph hi-d/i ">pubId</i> están permitidas. </p> <p>Nota:  <i class="+ topic/ph hi-d/i ">min</i> y <i class="+ topic/ph hi-d/i ">max</i> los números de versión son opcionales. </p> <p class="- topic/p ">Puede especificar varias <span class="codeph"> -air </span> opciones para permitir varias aplicaciones. Si no especifica una aplicación AIR o de SWF, todas las aplicaciones podrán acceder a este contenido. Durante una actualización, para eliminar o eliminar todas las entradas de la lista, aplique <span class="codeph"> -air </span> sin los argumentos restantes </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist name </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> valor </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pares </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los clientes de DRM que tienen restringido el acceso al contenido protegido. </p> <p class="- topic/p ">El valor admite pares nombre:valor separados por comas en el siguiente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> so | release= stringValue </span> </p> <p class="- topic/p ">Por ejemplo, <span class="codeph"> os=Win,release=2.0.1 </span>. Durante una actualización, para eliminar todas las entradas de la lista, aplique <span class="codeph"> -drmBlacklist </span> sin los argumentos restantes. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que los clientes de DRM deben tener un nivel de seguridad mínimo asignado para obtener acceso al contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | OBLIGATORIO | NO_PLAYBACK | REQUIRED_ACP | REQUIRED_CGMSA | USE_IF_AVAILABLE_ACP | USE_IF_AVAILABLE_CGMSA </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restricciones de protección de salida analógica </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | OBLIGATORIO | NO_PLAYBACK </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restricciones de protección de salida digital </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> Nombre de -runtimeBlacklist </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> valor </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pares </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los tiempos de ejecución de la aplicación que están restringidos para acceder al contenido protegido. </p> <p class="- topic/p ">El valor admite pares nombre:valor separados por comas en el siguiente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> so | aplicación | release= stringValue </span> </p> <p class="- topic/p ">Por ejemplo, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. Durante una actualización, para eliminar todas las entradas de la lista, aplique <span class="codeph"> -runtimeBlacklist </span> sin los argumentos restantes </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que los tiempos de ejecución de la aplicación deben tener un nivel de seguridad mínimo especificado para tener acceso al contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf archivo= archivo_swf </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Una lista de permitidos de aplicaciones de SWF permitidas para reproducir contenido protegido. </p> <p class="- topic/p ">Puede especificar varias <span class="codeph"> -swf </span> opciones para permitir varias aplicaciones. Si no especifica ninguna aplicación de AIR o de SWF, todas las aplicaciones podrán acceder a este contenido. </p> <p>Durante una actualización, para eliminar todas las entradas de la lista, aplique <span class="codeph"> -swf </span> sin los argumentos restantes Si desea identificar un SWF por su valor de hash, debe especificar el archivo de SWF para el que desea calcular el hash y el tiempo máximo para permitir que se complete la verificación del SWF (en segundos). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k nombre= valor </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica los valores o claves personalizados que desea añadir a una directiva DRM. </p> <p class="- topic/p ">Puede especificar varias <span class="codeph"> -k </span> opciones. Durante la actualización, puede solicitar <span class="codeph"> -k </span> sin los argumentos restantes si desea quitar todas las propiedades. El servidor de licencias DRM de Primetime administra la interpretación o la gestión de los datos. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p nombre= valor </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Agrega una propiedad personalizada que aparece en la licencia generada para cada cliente. </p> <p class="- topic/p ">Puede especificar varias <span class="codeph"> -p </span> opciones para agregar varias propiedades. Durante una actualización, debe realizar la solicitud <span class="codeph"> -p </span> sin los argumentos restantes si desea quitar todas las propiedades. La interpretación o la gestión de estos datos se gestionan mediante la implementación de la aplicación cliente. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> <span class="codeph"> -opOTA whitelist=&lt;connection types=""&gt; </span> </span> </td> 
   <td colname="2" class="- topic/entry "> Restricciones de protección de salida sobre el aire (OTA). El <span class="codeph"> lista blanca </span> El campo especifica qué tipos de conexión se van a lista de permitidos y el formato de &lt;connection types=""&gt; es <span class="codeph"> [tipo(,tipo)*] </span>, donde type puede ser cualquiera de los siguientes: MIRACAST, AIRPLAY, WIDI, DLNA </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opResolution &lt;filename&gt; </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Restricciones de protección de salida basadas en resolución tal como se definen en el archivo especificado. </p> <p>La codificación de este archivo es JSON. La gramática para el formato se encuentra en <i>Acerca de la protección de salida basada en resolución</i>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Ejemplos**

Para crear una directiva que permita el acceso anónimo al contenido, utilizando su propio archivo de propiedades de configuración:

```
java -jar libs\AdobePolicyManager.jar new policy_test.pol -x -c my_configuration.properties
```
