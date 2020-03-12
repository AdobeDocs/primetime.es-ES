---
description: 'null'
keywords: hard stop
seo-description: 'null'
seo-title: Propiedades de configuración
title: Propiedades de configuración
uuid: 216921d1-a9c1-4650-9dce-c025836986e5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Propiedades de configuración{#configuration-properties}

<!--<a id="section_20A96CDCC5C340DEAF455C6E300E5712"></a>-->

>[!NOTE]
>
>Para los nombres de propiedad que incluyen `.n`, el `n` representa un entero que comienza por 1 y aumenta para cada instancia de la propiedad. Por ejemplo: `policy.license.customProp.n`.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opción de línea de comandos/propiedad </th> 
   <th colname="2" class="- topic/entry entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> nombre <i class="+ topic/ph hi-d/i ">de política</i> </p> </td> 
   <td colname="2" class="- topic/entry "> El nombre de la directiva DRM legible en lenguaje natural. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Se aplican las siguientes condiciones: 
    <ul id="ul_AF4EBD6C19DC4DFAAB4756EF24BAC57D"> 
     <li id="li_6CC48ABF78EC426E9FC51458BD946BC9">Si es true, se requiere un servidor de claves HTTPS para la entrega de claves a iOS. </li> 
     <li id="li_63046A4ED7354C1E9E823B475E4AEFF7">Si no se especifica, el valor predeterminado es false. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.forceJailbreak</span> <p class="- topic/p "><span class="codeph"> -forceJailbreak</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> En el caso de los dispositivos que admiten la detección de saltos de cárcel, si es true, no permiten la reproducción cuando se detecta un salto de cárcel. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -crítico</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Define la importancia de la directiva DRM: 
    <ul id="ul_63F1994798894233A67AC4F8220AB642"> 
     <li id="li_D05DD9AD70464D6B9DB9DFF95846E589">Si es true, el servidor debe comprender todas las partes de la directiva DRM, que representa el comportamiento predeterminado. </li> 
     <li id="li_0211473DAF1F426787CC4A68F47643C6">Si es false, el servidor puede ignorar los atributos de directiva DRM que no reconoce. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chings.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Certificado de servidor de licencias cuya clave pública se utiliza para cifrar la clave de cifrado raíz para el Encadenado <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"></a>de licencias mejorado. Esta propiedad especifica un archivo que solo incluye el certificado. <p>Nota:  Se admiten formatos PEM o DER. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chinning.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">root-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Especifica la clave de cifrado raíz para el Encadenado <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"></a>de licencias mejorado. Si no se especifica ninguna clave y el Encadenado de licencias mejorado está habilitado, se genera automáticamente una clave aleatoria. </p> <p>La clave debe tener una longitud de 16 bytes y debe especificarse como valores hexadecimales. El espacio en blanco entre los valores hexadecimales es opcional. Para las actualizaciones, la opción de línea de comandos no está disponible y se omite la propiedad. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Si se requiere el registro de dominio, <i>url</i> especifica la dirección URL de un servidor de dominio. Para las actualizaciones, la opción de línea de comandos no está disponible y se omite la propiedad. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anónima</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry ">Especifica si se permite el registro de dominios anónimos. Establece la propiedad en true o incluye esta opción de línea de comandos para permitir el acceso anónimo. <p>Nota: Esta opción no se puede usar con <span class="codeph"> -domainAuthNS</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> , <i class="+ topic/ph hi-d/i ">espacio de nombres</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>El espacio de nombres de autenticación para el registro de dominios. Si se especifica, el cliente debe autenticarse con un nombre de usuario y una contraseña emitidos por la autoridad especificada. </p> <p>Para las actualizaciones, la opción de línea de comandos no está disponible y se omite la propiedad. </p> <p>Nota: Esta opción no se puede usar con <span class="codeph"> -domainAnon</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">AnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Se admiten restricciones de protección de salida analógicas y los siguientes valores: 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_F920EC01159C4231AFBE579D487C8770"><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </li> 
     <li class="- topic/li " id="li_2DE0494AF8C446EB9E4567915F5E97C3"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </li> 
     <li class="- topic/li " id="li_207D2D6256D6423FBDABA7A8627A9B7D"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </li> 
     <li class="- topic/li " id="li_E17D944BED5F403FAE94708EE6AE4BBE"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </li> 
     <li class="- topic/li " id="li_66D5A0C8FE154445A522D91EFB05B7ED"><span class="+ topic/ph pr-d/codeph codeph"> OBLIGATORIO</span> </li> 
     <li class="- topic/li " id="li_AF2024F212A249ED99AEECCF3E844A11"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </li> 
     <li class="- topic/li " id="li_FFF9B7DAE77740EE895EC35D1606A527"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </li> 
     <li class="- topic/li " id="li_52DED572F3AE495EB6A6450C611B440E"><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> pares <i class="+ topic/ph hi-d/i ">nombre/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Los clientes de DRM que tienen restricciones para acceder a contenido protegido. Esta opción especifica una lista de versiones de módulos DRM que no se pueden utilizar (lista negra). </p> <p>El valor consiste en pares <span class="codeph"> name=value</span> separados por comas en el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Los pares de nombre y valor adicionales deben separarse con comas. Por ejemplo, <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.RuntimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -RuntimeBlacklsit</span> <i class="+ topic/ph hi-d/i ">nombre/pares de valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Los tiempos de ejecución de la aplicación están restringidos para acceder al contenido protegido. Esta opción especifica una lista de versiones de módulos de tiempo de ejecución que no se pueden utilizar (lista negra). </p> <p>El valor consiste en pares <span class="codeph"> name=value</span> separados por comas en el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Los pares de nombre y valor adicionales deben separarse con comas. Por ejemplo, <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">nombre/pares de valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica las capacidades del dispositivo necesarias para acceder al contenido protegido. El valor consiste en pares <span class="codeph"> name=value</span> separados por comas en el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Por ejemplo, <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. </p> <p>Durante una actualización, debe aplicar <span class="codeph"> -devCapabilitiesV1</span> sin los argumentos restantes que quitan la restricción de capacidades del dispositivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> pares <i class="+ topic/ph hi-d/i ">nombre/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica la frecuencia con la que los clientes deben enviar mensajes de sincronización al servidor. </p> <p>Si no se establece la propiedad, los clientes no enviarán mensajes de sincronización cuando reproduzcan contenido protegido con una directiva DRM. El valor consiste en pares <span class="codeph"> name=value</span> separados por comas en el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force=numberValue</span> </p> <p class="- topic/p ">La siguiente lista proporciona información adicional sobre las opciones: 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_FD2C0C6DA19E455AA1917A56E09A7F84">(obligatorio) <span class="codeph"> start</span> especifica que el cliente debe empezar a sincronizar con el servidor en los minutos especificados desde la última sincronización. </li> 
      <li id="li_9DEBC57385A442C3929AE3D0E3FA8992">(opcional) <span class="codeph"> force</span> es la probabilidad (0-100) con la que el cliente necesita forzar un mensaje de sincronización durante la reproducción. </li> 
     </ul>Durante la actualización, utilice <span class="codeph"> -sync</span> sin los argumentos restantes para eliminar los requisitos de sincronización. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Indica si esta directiva DRM tiene una licencia raíz. <p>Para obtener más información, consulte <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> Encadenado</a>de licencias mejorado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">La fecha después de la cual el contenido pasa a ser válido. Puede aplicar uno de los siguientes formatos: 
    <ul id="ul_6610B44D0C16485098F6F45DE3F151D7"> 
     <li id="li_986707D4C6164C44B3CCBE2EEB4C09B6"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> <p>Por ejemplo, <span class="codeph"> 2009-01-31</span> significa 31 de enero a las 12:00 AM. </p> </li> 
     <li id="li_E15B782716124F6EAEFB04D16E5280DB"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:seg</span> <p>Por ejemplo, <span class="codeph"> 2009-01-31-14:30:00</span> significa 31 de enero a las 2:30 p.m. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha antes de que el contenido no sea válido. </p> <p>Nota: No puede especificar <span class="codeph"> policy.expiration.endDate</span> y <span class="codeph"> policy.expiration.duration</span> de forma simultánea. </p> <p>Por ejemplo, 2009-01-31-14:30:00 significa que el contenido caducará el 31 de enero a las 2:30 p.m. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Tiempo en minutos en el que el contenido se vuelve no válido. El tiempo comienza cuando se empaqueta contenido. </p> <p>Nota: No puede especificar <span class="codeph"> policy.expiration.endDate</span> y <span class="codeph"> policy.expiration.duration</span> de forma simultánea. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Tiempo en minutos en el que una licencia se puede almacenar en caché en el cliente. Puede establecer esta propiedad en 0 para evitar el almacenamiento en caché de licencias. El valor debe ser 0 o superior. </p> <p>Nota: No puede especificar <span class="codeph"> policy.licenseCaching.duration</span> y <span class="codeph"> policy.licenseCaching.endDate</span> de forma simultánea. </p> <p class="- topic/p ">Esta configuración de directiva DRM se aplica solamente al almacenamiento en caché de licencias en el disco y no controla la duración de la licencia en caché de memoria. La licencia se puede almacenar en la memoria caché aunque no especifique una directiva DRM con una duración de cero. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Fecha después de la cual ya no puede almacenar en caché las licencias. </p> <p>Nota: No puede especificar <span class="codeph"> policy.licenseCaching.duration</span> y <span class="codeph"> policy.licenseCaching.endDate</span> de forma simultánea. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anónima</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica si se permite la adquisición anónima de licencias. El valor predeterminado es <span class="codeph"> false</span>, lo que significa que se requiere un nombre de usuario y una contraseña. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si se requiere un nombre de usuario y una contraseña, esta propiedad especifica un calificador de nombre opcional para los nombres de usuario. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nombre y valor personalizados que usará el servidor durante la adquisición de licencias. Puede aplicar el siguiente formato para especificar propiedades: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playWindow </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica la ventana de reproducción en minutos. Este valor representa cuánto tiempo es válida la licencia después de la primera vez que se reproduce contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restricciones de protección de salida, que deben ser uno de los siguientes valores: 
     <ul id="ul_wsb_kfp_fs"> 
      <li id="li_FE012306F22F4F3FB981FE167C7A8B94"><span class="codeph"> NO_PROTECTION</span> </li> 
      <li id="li_A5591DC8983848FE9823C2A261BF7713"><span class="codeph"> USE_IF_AVAILABLE</span> </li> 
      <li id="li_74102C36ADE841C4B9ED71156E0A4C2C"><span class="codeph"> OBLIGATORIO</span> </li> 
      <li id="li_769E15C85B4E4DD48213DBD019D60BA7"><span class="codeph"> NO_PLAYBACK</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.ota</span> </td> 
   <td colname="2" class="- topic/entry ">Especifica los tipos de conexión a través del aire (OTA) que se deben incluir en la lista blanca. Los tipos de conexión válidos incluyen: 
    <ul id="ul_iz5_4fp_fs"> 
     <li id="li_FB07519EFEFE4B95B3B1F5BFD4DE6591"><span class="codeph"> MIRACAST</span> </li> 
     <li id="li_51E7DE83679F4630B01264407DAD0E84"><span class="codeph"> AIRPLAY</span> </li> 
     <li id="li_D499A0487AAC409CB2CEA6164265D3CF"><span class="codeph"> DLNA</span> </li> 
     <li id="li_4FCC0EC4A0FC48F99A13EC8A1B78D6A1"><span class="codeph"> WIDI</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.resolution</span> </td> 
   <td colname="2" class="- topic/entry "> Especifica el archivo de configuración en el que se definen las restricciones basadas en resolución. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el nivel de seguridad mínimo para permitir que el módulo DRM tenga acceso al contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.RuntimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El módulo de tiempo de ejecución de la aplicación debe tener al menos el nivel de seguridad mínimo especificado para acceder al contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lista blanca de aplicaciones que no son Flash (Adobe AIR, iOS, Android, etc.) que pueden reproducir contenido protegido. La propiedad debe utilizar el siguiente formato: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">máx</span>]]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lista blanca de aplicaciones SWF con permiso para reproducir contenido protegido. La propiedad debe utilizar el siguiente formato: </p> <p class="- topic/p "> 
     <ul id="ul_EC20F52AD95C4BE3B7F703048A43CDF0"> 
      <li id="li_3E4A47D925C24834A2C25BC5943279D4"><span class="+ topic/ph pr-d/codeph codeph">URL</span> </li> 
      <li id="li_9A7CAF081C5F488FB5CDA6D38C5552F6"><span class="+ topic/ph pr-d/codeph codeph">file=swf_file</span> </li> 
      <li id="li_E10EA4223137489CBE4015DE999F7154"><span class="codeph">time=max_time_to_verify</span> </li> 
     </ul> <i class="+ topic/ph hi-d/i ">swf_file</i> es el archivo SWF que se utiliza para calcular el hash, y <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> es el tiempo máximo en segundos que se permite descargar y verificar que se complete el SWF. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nombre y valor personalizados que debe incluir en las licencias cuando éstas se expidan a los usuarios. Debe especificar el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n=name</span> </p> <p class="- topic/p ">Puede definir esta opción varias veces para varias propiedades personalizadas. </p> </td> 
  </tr> 
 </tbody> 
</table>

