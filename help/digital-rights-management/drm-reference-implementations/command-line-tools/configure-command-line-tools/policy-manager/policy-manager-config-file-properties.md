---
keywords: parada forzada
title: Propiedades de configuración
description: Propiedades de configuración
copied-description: true
exl-id: f88c57d6-d951-4d7a-8de1-44cd1aa8e5f7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---

# Propiedades de configuración {#configuration-properties}

<!--<a id="section_20A96CDCC5C340DEAF455C6E300E5712"></a>-->

>[!NOTE]
>
>Para nombres de propiedades que incluyen `.n`, el `n` representa un entero que comienza con 1 y aumenta para cada instancia de la propiedad. Por ejemplo: `policy.license.customProp.n`.

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
   <td colname="2" class="- topic/entry "> El nombre de la política de DRM legible en lenguaje natural. </td> 
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
   <td colname="2" class="- topic/entry "> En el caso de dispositivos compatibles con la detección de jailbreak, si el valor es True, no permitir la reproducción cuando se detecte un jailbreak. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -crítico</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Define la importancia de la política de DRM: 
    <ul id="ul_63F1994798894233A67AC4F8220AB642"> 
     <li id="li_D05DD9AD70464D6B9DB9DFF95846E589">Si es true, el servidor debe comprender todas las partes de la directiva DRM, que representa el comportamiento predeterminado. </li> 
     <li id="li_0211473DAF1F426787CC4A68F47643C6">Si es false, el servidor puede ignorar los atributos de directivas DRM que no reconoce. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Certificado del servidor de licencias cuya clave pública se utiliza para cifrar la clave de cifrado raíz del <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> Encadenamiento de licencias mejorado</a>. Esta propiedad especifica un archivo que solo incluye el certificado. <p>Nota: Se admiten los formatos PEM o DER. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">tecla de raíz</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Especifica la clave de cifrado raíz para <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> Encadenamiento de licencias mejorado</a>. Si no se especifica ninguna clave y el encadenamiento de licencias mejorado está habilitado, se genera automáticamente una clave aleatoria. </p> <p>La clave debe tener 16 bytes de longitud y especificarse como valores hexadecimales. El espacio en blanco entre los valores hexadecimales es opcional. Para las actualizaciones, la opción de la línea de comandos no está disponible y la propiedad se omite. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Si se requiere el registro del dominio, <i>url</i> especifica la dirección URL de un servidor de dominio. Para las actualizaciones, la opción de la línea de comandos no está disponible y la propiedad se omite. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry ">Especifica si se permite el registro anónimo de dominios. Establece la propiedad en true o incluye esta opción de la línea de comandos para permitir el acceso anónimo. <p>Nota: Esta opción no se puede utilizar con <span class="codeph"> -domainAuthNS</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">namespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>El área de nombres de autenticación para el registro de dominios. Si se especifica, el cliente debe autenticarse con un nombre de usuario y una contraseña emitidos por la autoridad especificada. </p> <p>Para las actualizaciones, la opción de la línea de comandos no está disponible y la propiedad se omite. </p> <p>Nota: Esta opción no se puede utilizar con <span class="codeph"> -domainAnon</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">Opción analógica</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Se admiten restricciones de protección de salida analógica y los siguientes valores: 
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
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> <i class="+ topic/ph hi-d/i ">pares de nombre/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Los clientes de DRM con restricciones de acceso al contenido protegido. Esta opción especifica una lista de versiones de módulos DRM que no pueden utilizarse (lista de bloqueados). </p> <p>El valor está formado por comas separadas <span class="codeph"> name=value</span> pares en el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> so|release|arch|model|provider|env|screen=value</span> </p> <p class="- topic/p ">Los pares de nombre/valor adicionales deben estar separados por comas. Por ejemplo, <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">pares de nombre/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Los tiempos de ejecución de las aplicaciones están restringidos para acceder al contenido protegido. Esta opción especifica una lista de versiones de módulos de tiempo de ejecución que no se pueden utilizar (lista de bloqueados). </p> <p>El valor está formado por comas separadas <span class="codeph"> name=value</span> pares en el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> so|release|application|arch|model|provider|env|screen=value</span> </p> <p class="- topic/p ">Los pares de nombre/valor adicionales deben estar separados por comas. Por ejemplo, <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">pares de nombre/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica las funciones del dispositivo necesarias para acceder al contenido protegido. El valor está formado por comas separadas <span class="codeph"> name=value</span> pares en el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Por ejemplo, <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. </p> <p>Durante una actualización, debe realizar la solicitud <span class="codeph"> -devCapabilitiesV1</span> sin los argumentos restantes que quitan la restricción de capacidades del dispositivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">pares de nombre/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica la frecuencia con la que los clientes deben enviar mensajes de sincronización al servidor. </p> <p>Si no se define la propiedad, los clientes no enviarán mensajes de sincronización cuando reproduzcan contenido protegido con una directiva DRM. El valor está formado por comas separadas <span class="codeph"> name=value</span> pares en el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force=numberValue</span> </p> <p class="- topic/p ">La siguiente lista proporciona información adicional sobre las opciones: 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_FD2C0C6DA19E455AA1917A56E09A7F84">(obligatorio) <span class="codeph"> start</span> especifica que el cliente debe iniciar la sincronización con el servidor en los minutos especificados desde la última sincronización. </li> 
      <li id="li_9DEBC57385A442C3929AE3D0E3FA8992">(opcional) <span class="codeph"> forzar</span> es la probabilidad (0-100) con la que el cliente necesita forzar un mensaje de sincronización durante la reproducción. </li> 
     </ul>Durante la actualización, utilice <span class="codeph"> -sync</span> sin los argumentos restantes para quitar los requisitos de sincronización. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Indica si esta directiva DRM tiene una licencia raíz. <p>Para obtener más información, consulte <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> Encadenamiento de licencias mejorado</a>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">Fecha a partir de la cual se valida el contenido. Puede aplicar uno de los siguientes formatos: 
    <ul id="ul_6610B44D0C16485098F6F45DE3F151D7"> 
     <li id="li_986707D4C6164C44B3CCBE2EEB4C09B6"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> <p>Por ejemplo, <span class="codeph"> 31-01-2009</span> significa 31 de enero a las 12:00 AM. </p> </li> 
     <li id="li_E15B782716124F6EAEFB04D16E5280DB"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span> <p>Por ejemplo, <span class="codeph"> 14-31-01-2009:30:00</span> significa 31 de enero a las 2:30 PM. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha antes del contenido deja de ser válida. </p> <p>Nota: No se puede especificar <span class="codeph"> policy.expiration.endDate</span> y <span class="codeph"> policy.expiration.duration</span> simultáneamente. </p> <p>Por ejemplo, 2009-01-31-14:30:00 significa que el contenido caducará el 31 de enero a las 2:30 p. m. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Tiempo en minutos en minutos que el contenido deja de ser válido. La hora comienza cuando empaqueta contenido. </p> <p>Nota: No se puede especificar <span class="codeph"> policy.expiration.endDate</span> y <span class="codeph"> policy.expiration.duration</span> simultáneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Tiempo en minutos que se puede almacenar una licencia en caché en el cliente. Puede establecer esta propiedad en 0 para evitar el almacenamiento en caché de licencias. El valor debe ser 0 o superior. </p> <p>Nota: No se puede especificar <span class="codeph"> policy.licenseCaching.duration</span> y <span class="codeph"> policy.licenseCaching.endDate</span> simultáneamente. </p> <p class="- topic/p ">Esta configuración de directiva DRM se aplica sólo al almacenamiento en caché de licencias en el disco y no controla la duración de las licencias en caché de memoria. La licencia se puede almacenar en caché en la memoria incluso si no se especifica una directiva DRM con una duración de cero. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La fecha a partir de la cual ya no puede almacenar las licencias en caché. </p> <p>Nota: No se puede especificar <span class="codeph"> policy.licenseCaching.duration</span> y <span class="codeph"> policy.licenseCaching.endDate</span> simultáneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica si se permite la adquisición de licencia anónima. El valor predeterminado es <span class="codeph"> false</span>, lo que significa que se requiere un nombre de usuario y una contraseña. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si se requiere un nombre de usuario y una contraseña, esta propiedad especifica un calificador de nombre opcional para los nombres de usuario. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nombre/valor personalizados que el servidor utilizará durante la adquisición de la licencia. Puede aplicar el siguiente formato para especificar propiedades: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">valor</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el periodo de reproducción en minutos. Este valor representa cuánto tiempo es válida la licencia después de la primera vez que se reproduce el contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restricciones de protección de salida, que deben tener uno de los valores siguientes: 
     <ul id="ul_wsb_kfp_fs"> 
      <li id="li_FE012306F22F4F3FB981FE167C7A8B94"><span class="codeph"> NO_PROTECTION</span> </li> 
      <li id="li_A5591DC8983848FE9823C2A261BF7713"><span class="codeph"> USE_IF_AVAILABLE</span> </li> 
      <li id="li_74102C36ADE841C4B9ED71156E0A4C2C"><span class="codeph"> OBLIGATORIO</span> </li> 
      <li id="li_769E15C85B4E4DD48213DBD019D60BA7"><span class="codeph"> NO_PLAYBACK</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.ota</span> </td> 
   <td colname="2" class="- topic/entry ">Especifica los tipos de conexión aérea (OTA) que deben permitirse en la lista. Los tipos de conexión válidos incluyen: 
    <ul id="ul_iz5_4fp_fs"> 
     <li id="li_FB07519EFEFE4B95B3B1F5BFD4DE6591"><span class="codeph"> MIRACAST</span> </li> 
     <li id="li_51E7DE83679F4630B01264407DAD0E84"><span class="codeph"> JUEGO AÉREO</span> </li> 
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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el nivel de seguridad mínimo para permitir que el módulo DRM acceda al contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El módulo de tiempo de ejecución de la aplicación debe tener al menos el nivel de seguridad mínimo especificado para acceder al contenido protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Una lista de permitidos de aplicaciones que no son de Flash (Adobe AIR, iOS, Android, etc.) que pueden reproducir contenido protegido. La propiedad debe utilizar el siguiente formato: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Una lista de permitidos de aplicaciones de SWF permitidas para reproducir contenido protegido. La propiedad debe utilizar el siguiente formato: </p> <p class="- topic/p "> 
     <ul id="ul_EC20F52AD95C4BE3B7F703048A43CDF0"> 
      <li id="li_3E4A47D925C24834A2C25BC5943279D4"><span class="+ topic/ph pr-d/codeph codeph">URL</span> </li> 
      <li id="li_9A7CAF081C5F488FB5CDA6D38C5552F6"><span class="+ topic/ph pr-d/codeph codeph">file=swf_file</span> </li> 
      <li id="li_E10EA4223137489CBE4015DE999F7154"><span class="codeph">time=max_time_to_verify</span> </li> 
     </ul> <i class="+ topic/ph hi-d/i ">swf_file</i> es el archivo SWF que se utiliza para calcular el hash y <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> es el tiempo máximo en segundos permitido para descargar y comprobar que el SWF finalice. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nombre/valor personalizados que deben incluirse en las licencias cuando estas se emiten a los usuarios. Debe especificar el siguiente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n=name</span> </p> <p class="- topic/p ">Puede definir esta opción varias veces para varias propiedades personalizadas. </p> </td> 
  </tr> 
 </tbody> 
</table>
