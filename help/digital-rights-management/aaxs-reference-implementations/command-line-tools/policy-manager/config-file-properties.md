---
title: Propiedades del archivo de configuración
description: Propiedades del archivo de configuración
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---


# Propiedades del archivo de configuración {#configuration-file-properties}

El archivo de configuración especifica las siguientes propiedades. Para los nombres de propiedad que incluyen `n`, `n` representa un entero que comienza con 1 y aumenta para cada instancia de la propiedad.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opción Propiedad/Línea de comandos </th> 
   <th colname="2" class="- topic/entry entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">npolicy name</i> </p> </td> 
   <td colname="2" class="- topic/entry "> El nombre de la directiva legible en lenguaje natural. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requiredKeyServer</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">keyServerboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Si es true, se requiere un servidor de claves HTTPS para el envío de claves a iOS. El valor predeterminado es false, si no se especifica lo contrario. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.forceJailbreak</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">forceJailbreakboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Si es true, en el caso de los dispositivos que admiten la detección de saltos de cárcel, no permitan la reproducción si se ha detectado una pausa de cárcel. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">crialboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Establezca la criticidad de las políticas. Si es true, el servidor debe comprender todas las partes de la directiva (este es el comportamiento predeterminado). Si es false, el servidor puede ignorar los atributos de directiva que no entienda. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Certificado de servidor de licencias cuya clave pública se utilice para cifrar la clave de cifrado raíz para el <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"> encadenado de licencias mejorado </a>
   Esta propiedad especifica un archivo que contiene solo el certificado (se acepta el formato PEM o DER). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">rootKeyroot-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Especifique la clave de cifrado raíz para el encadenado de licencias mejorado. Si no se especifica ninguna clave y el Encadenado de licencias mejorado está habilitado, se genera una clave aleatoria. La clave debe tener una longitud de 16 bytes y especificarse como valores hexadecimales. El espacio en blanco entre los valores hexadecimales es opcional. Para las actualizaciones, no se permite la opción de línea de comandos y se omite la propiedad. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">domainURLurl</i> </p> </td> 
   <td colname="2" class="- topic/entry "> URL del servidor de dominio, si es necesario registrar el dominio. Para las actualizaciones, no se permite la opción de línea de comandos y se omite la propiedad. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> Especifica si se permite el registro de dominio anónimo. Establezca la propiedad en true o incluya esta opción de línea de comandos para permitir el acceso anónimo. Esta opción no se puede usar con -domainAuthNS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">domainAuthNSnamespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> El espacio de nombres de autenticación para el registro de dominios. Si se especifica, el cliente debe autenticarse con un nombre de usuario y una contraseña emitidos por la autoridad especificada. Para las actualizaciones, no se permite la opción de línea de comandos y se omite la propiedad. Esta opción no se puede usar con -domainAnon. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">opAnalogAnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Restricciones de protección de salida analógica. Se admiten los siguientes valores: 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUERIDO</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">drmBlacklistname/value-pares</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Los clientes de DRM no tienen acceso a contenido protegido. Esta opción especifica una lista de versiones de módulos DRM que no se pueden utilizar (lista de bloqueados). El valor consiste en pares nombre=valor separados por comas con el siguiente formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|provider|env|screen=value</span> </p> <p class="- topic/p ">Los pares de nombre/valor adicionales deben separarse con comas. Por ejemplo: <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">runtimeBlacklsitname/value-pares</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Los tiempos de ejecución de la aplicación están restringidos para acceder a contenido protegido. Esta opción especifica una lista de versiones de módulos de tiempo de ejecución que no se pueden utilizar (lista de bloqueados). El valor consiste en pares nombre=valor separados por comas con el siguiente formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|provider|env|screen=value</span> </p> <p class="- topic/p ">Los pares de nombre/valor adicionales deben separarse con comas. Por ejemplo, <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">pares nombre/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica las capacidades del dispositivo necesarias para acceder al contenido protegido. El valor consiste en pares nombre=valor separados por comas con el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Por ejemplo, <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. Durante la actualización, utilice <span class="codeph"> -devCapabilitiesV1</span> sin los argumentos restantes para eliminar la restricción de capacidades del dispositivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">syncname/value-pares</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifique con qué frecuencia se requiere que los clientes envíen mensajes de sincronización al servidor. Si no se configura, los clientes no enviarán mensajes de sincronización al reproducir contenido protegido con esta directiva. El valor consiste en pares <span class="codeph"> name=value</span> separados por comas con el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> start</span>  (obligatorio): El intervalo de inicio especifica que el cliente debe empezar a sincronizarse con el servidor en estos minutos desde la última sincronización. </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> force</span>  (opcional): la probabilidad de sincronización forzada es la probabilidad (0-100) con la que el cliente debe forzar un mensaje de sincronización durante la reproducción. </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span>  (opcional): el intervalo de parada dura es el tiempo, en minutos, después del cual el cliente fallará en la reproducción si no puede sincronizarse. Si se configura, debe ser bueno que el intervalo de inicio. </li> 
     </ul>Durante la actualización, utilice <span class="codeph"> -sync</span> sin los argumentos restantes para eliminar los requisitos de sincronización. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Indica si esta directiva tiene una licencia raíz (consulte <i class="+ topic/ph hi-d/i ">Encadenado de licencias mejorado</i> en <i class="+ topic/ph hi-d/i ">Uso del acceso de Adobe para proteger contenido</i>). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">La fecha después de la cual es válido el contenido. Utilice el formato <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> (por ejemplo, <span class="codeph"> 2009-01-31</span> representa el 31 de enero a las 12:00 AM) o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:sec</span> (por ejemplo, <span class="codeph">&gt; 2009-01-31-14:30:00</span> representa el 31 de enero a las 2:30 pm). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha antes de la cual es válido el contenido. Puede que tanto <span class="codeph"> policy.expiration.endDate</span> como policy.expiration.duration no se especifiquen simultáneamente. Utilice el formato <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> o <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> (por ejemplo, 2009-01-31-14:30:00 representa el 31 de enero a las 2:30 p. m). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Cantidad de tiempo que el contenido es válido (en minutos), a partir del momento en que se empaqueta. Es posible que <span class="codeph"> policy.expiration.endDate</span> y <span class="codeph"> policy.expiration.duration</span> no se especifiquen al mismo tiempo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Cantidad de tiempo que una licencia puede almacenarse en caché en el cliente (en minutos). Establezca esta propiedad en 0 para no permitir el almacenamiento en caché de licencias. El valor debe ser 0 o superior. Puede que <span class="codeph"> policy.licenseCaching.duration</span> y <span class="codeph"> policy.licenseCaching.endDate</span> no se utilicen simultáneamente. </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nota</b>: Esta configuración de directiva solo se aplica al almacenamiento en caché de licencias en el disco. No controla la duración de la licencia en caché de memoria. La licencia se puede almacenar en caché en la memoria aunque la duración especificada de la directiva sea cero. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha después de la cual no se podrán almacenar en caché las licencias. Puede que <span class="codeph"> policy.licenseCaching.duration</span> y <span class="codeph"> policy.licenseCaching.endDate</span> no se utilicen simultáneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica si se permite la adquisición de licencia anónima. El valor predeterminado es "false" (se requiere autenticación de nombre de usuario/contraseña) si no se especifica lo contrario. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si se requiere autenticación de nombre de usuario/contraseña, esta propiedad especifica un calificador de nombre opcional para nombres de usuario. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nombre/valor personalizados que usará el servidor durante la adquisición de licencia. Utilice el siguiente formato para especificar propiedades: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica la ventana de reproducción (en minutos), que es la duración durante la cual la licencia es válida tras la primera vez que se utiliza para reproducir contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restricciones de protección de salida. Los valores deben ser uno de los siguientes: </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION, USE_IF_AVAILABLE, REQUERIDO, NO_PLAYBACK</i> </p> </td> 
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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lista de permitidos de aplicaciones de Adobe AIR o iOS que pueden reproducir contenido protegido. La propiedad debe utilizar el siguiente formato: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lista de permitidos de aplicaciones SWF permitidas para reproducir contenido protegido. Utilice el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"></span> URLor file=<span class="+ topic/ph pr-d/codeph codeph">swf_file</span>, time=<i class="+ topic/ph hi-d/i ">max_time_to_</i> <i class="+ topic/ph hi-d/i ">verifyswf_</i> es el archivo SWF para el que se calcula el hash y  <i class="+ topic/ph hi-d/i ">max_time_to_</i> verifyes el tiempo máximo para permitir la descarga y verificación del SWF que se completará (en segundos). </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nombre/valor personalizados que se incluirán en las licencias otorgadas a los usuarios. Utilice el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> <p class="- topic/p ">Esta opción se puede definir varias veces para varias propiedades personalizadas. </p> </td> 
  </tr> 
 </tbody> 
</table>

