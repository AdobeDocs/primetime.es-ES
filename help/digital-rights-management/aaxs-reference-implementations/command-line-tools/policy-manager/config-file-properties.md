---
title: Propiedades del archivo de configuración
description: Propiedades del archivo de configuración
copied-description: true
exl-id: 6405126d-4cf2-4ffc-821d-fbfdc00b60ef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# Propiedades del archivo de configuración {#configuration-file-properties}

El archivo de configuración especifica las siguientes propiedades. Para nombres de propiedades que incluyen `n`, `n` representa un entero que comienza por 1 y aumenta para cada instancia de la propiedad.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Propiedad/Opción de línea de comandos </th> 
   <th colname="2" class="- topic/entry entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> <i class="+ topic/ph hi-d/i ">nombre de política</i> </p> </td> 
   <td colname="2" class="- topic/entry "> El nombre legible en lenguaje natural de la directiva. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Si es true, se requiere un servidor de claves HTTPS para la entrega de claves a iOS. El valor predeterminado es false si no se especifica. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.forceJailbreak</span> <p class="- topic/p "><span class="codeph"> -forceJailbreak</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Si el valor es True, los dispositivos compatibles con la detección de jailbreak no permiten la reproducción si se ha detectado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -crítico</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Establecer la criticidad de la directiva. Si es true, el servidor debe comprender todas las partes de la directiva (este es el comportamiento predeterminado). Si es false, el servidor puede omitir los atributos de directiva que no comprende. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Certificado del servidor de licencias cuya clave pública se utiliza para cifrar la clave de cifrado raíz del <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"> Encadenamiento de licencias mejorado </a>
   Esta propiedad especifica un archivo que contiene solo el certificado (se acepta el formato PEM o DER). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">tecla de raíz</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Especifique la clave de cifrado raíz para el Encadenamiento de licencias mejorado. Si no se especifica ninguna clave y el encadenamiento de licencias mejorado está habilitado, se generará una clave aleatoria. La clave debe tener 16 bytes de longitud y especificarse como valores hexadecimales. El espacio en blanco entre los valores hexadecimales es opcional. Para las actualizaciones, la opción de línea de comandos no está permitida y la propiedad se omite. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry "> URL del servidor de dominio, si se requiere el registro del dominio. Para las actualizaciones, la opción de línea de comandos no está permitida y la propiedad se omite. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> Especifica si se permite el registro anónimo de dominios. Establezca la propiedad en true o incluya esta opción de línea de comandos para permitir el acceso anónimo. Esta opción no se puede usar con -domainAuthNS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">namespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> El área de nombres de autenticación para el registro de dominios. Si se especifica, el cliente debe autenticarse con un nombre de usuario y una contraseña emitidos por la autoridad especificada. Para las actualizaciones, la opción de línea de comandos no está permitida y la propiedad se omite. Esta opción no se puede utilizar con -domainAnon. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">Opción analógica</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Restricciones de protección de salida analógica. Se admiten los siguientes valores: 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> OBLIGATORIO</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> <i class="+ topic/ph hi-d/i ">pares de nombre/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Los clientes de DRM tienen restringido el acceso al contenido protegido. Esta opción especifica una lista de versiones de módulos DRM que no pueden utilizarse (lista de bloqueados). El valor está formado por pares nombre=valor separados por comas con el siguiente formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> so|release|arch|model|provider|env|screen=value</span> </p> <p class="- topic/p ">Los pares de nombre/valor adicionales deben estar separados por comas. Por ejemplo: <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">pares de nombre/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Los tiempos de ejecución de la aplicación restringieron el acceso al contenido protegido. Esta opción especifica una lista de versiones de módulos de tiempo de ejecución que no se pueden utilizar (lista de bloqueados). El valor está formado por pares nombre=valor separados por comas con el siguiente formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> so|release|application|arch|model|provider|env|screen=value</span> </p> <p class="- topic/p ">Los pares de nombre/valor adicionales deben estar separados por comas. Por ejemplo, <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">pares de nombre/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica las capacidades del dispositivo necesarias para acceder al contenido protegido. El valor está formado por pares nombre=valor separados por comas con el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Por ejemplo, <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. Durante la actualización, utilice <span class="codeph"> -devCapabilitiesV1</span> sin los argumentos restantes para quitar la restricción de capacidades del dispositivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">pares de nombre/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifique la frecuencia con la que los clientes deben enviar mensajes de sincronización al servidor. Si no se establece, los clientes no enviarán mensajes de sincronización al reproducir contenido protegido con esta directiva. El valor está formado por comas separadas <span class="codeph"> name=value</span> empareja con el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> start</span> (obligatorio): el intervalo de inicio especifica que el cliente debe iniciar la sincronización con el servidor esta cantidad de minutos desde la última sincronización. </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> forzar</span> (opcional): la probabilidad de sincronización forzada es la probabilidad (0-100) con la que el cliente debe forzar un mensaje de sincronización durante la reproducción. </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span> (opcional): El intervalo de parada grave es el tiempo en minutos tras el cual el cliente falla en la reproducción si no puede sincronizarse. Si se establece, debe ser bueno que el intervalo de inicio. </li> 
     </ul>Durante la actualización, utilice <span class="codeph"> -sync</span> sin los argumentos restantes para quitar los requisitos de sincronización. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Indica si esta directiva tiene una licencia de raíz (consulte <i class="+ topic/ph hi-d/i ">Encadenamiento de licencias mejorado</i> in <i class="+ topic/ph hi-d/i ">Uso del acceso al Adobe para proteger el contenido</i>). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">La fecha después de la cual el contenido es válido. Usar el formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> (por ejemplo, <span class="codeph"> 31-01-2009</span> representa el 31 de enero a las 12:00 a. m.) o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span> (por ejemplo, <span class="codeph"> 14-31-01-2009:30:00</span> representa el 31 de enero a las 2:30 p.m.). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha antes de la cual el contenido es válido. Ambos <span class="codeph"> policy.expiration.endDate</span> y policy.expiration.duration no se pueden especificar simultáneamente. Usar el formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span> (por ejemplo, 2009-01-31-14:30:00 representa el 31 de enero a las 2:30 p.m.). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Cantidad de tiempo que el contenido es válido (en minutos), a partir del momento en que se empaqueta. Ambos <span class="codeph"> policy.expiration.endDate</span> y <span class="codeph"> policy.expiration.duration</span> no se puede especificar al mismo tiempo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Cantidad de tiempo que se puede almacenar una licencia en caché en el cliente (en minutos). Establezca esta propiedad en 0 para impedir el almacenamiento en caché de licencias. El valor debe ser 0 o superior. Ambos <span class="codeph"> policy.licenseCaching.duration</span> y <span class="codeph"> policy.licenseCaching.endDate</span> no se puede usar simultáneamente. </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nota</b>: esta configuración de directiva se aplica solo al almacenamiento en caché de licencias en el disco. No controla la duración de la licencia en caché de la memoria. La licencia se puede almacenar en caché en la memoria incluso si la duración especificada por la directiva es cero. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha después de la cual las licencias no pueden almacenarse en caché. Ambos <span class="codeph"> policy.licenseCaching.duration</span> y <span class="codeph"> policy.licenseCaching.endDate</span> no se puede usar simultáneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica si se permite la adquisición de licencia anónima. El valor predeterminado es "false" (se requiere autenticación de nombre de usuario y contraseña) si no se especifica. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si se requiere autenticación de nombre de usuario y contraseña, esta propiedad especifica un calificador de nombre opcional para los nombres de usuario. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nombre/valor personalizados que el servidor utilizará durante la adquisición de la licencia. Utilice el siguiente formato para especificar propiedades: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">valor</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el periodo de reproducción (en minutos), que es la duración durante la cual la licencia es válida después de la primera vez que se utiliza para reproducir contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restricciones de protección de salida. Los valores deben ser uno de los siguientes: </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION, USE_IF_AVAILABLE, OBLIGATORIO, NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El módulo DRM debe tener el nivel de seguridad mínimo especificado, o superior, para acceder al contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El módulo de tiempo de ejecución de la aplicación debe tener el nivel de seguridad mínimo especificado, o superior, para acceder al contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Una lista de permitidos de aplicaciones de Adobe AIR o iOS permitidas para reproducir contenido protegido. La propiedad debe utilizar el siguiente formato: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Una lista de permitidos de aplicaciones de SWF permitidas para reproducir contenido protegido. Utilice el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">URL</span> o file=<span class="+ topic/ph pr-d/codeph codeph">swf_file</span>,time=<i class="+ topic/ph hi-d/i ">max_time_to_verify</i> <i class="+ topic/ph hi-d/i ">swf_file</i> es el archivo SWF para el que se calcula el hash y <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> es el tiempo máximo que permite la descarga y verificación del SWF para completarla (en segundos). </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nombre/valor personalizados que se incluirán en las licencias emitidas a los usuarios. Utilice el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">valor</span> </p> <p class="- topic/p ">Esta opción se puede definir varias veces para varias propiedades personalizadas. </p> </td> 
  </tr> 
 </tbody> 
</table>
