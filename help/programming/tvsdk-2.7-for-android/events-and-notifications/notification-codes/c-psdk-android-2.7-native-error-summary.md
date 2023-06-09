---
title: Detalles de la notificación NATIVE_ERROR
description: Detalles de la notificación NATIVE_ERROR
copied-description: true
exl-id: 51c75349-0fa8-405d-9e09-b51b425fe21b
source-git-commit: 1bc2f6c230c262babf2958c32fee31afcad04c2f
workflow-type: tm+mt
source-wordcount: '6868'
ht-degree: 2%

---

# Detalles de la notificación NATIVE_ERROR {#details-for-the-native-error-notification}

Cuando TVSDK administra un error nativo, devuelve algunos o todos los valores de clave de metadatos siguientes como cadenas.

<table id="table_7F713B7A56024D8DA3C84E449D09CC91"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Nombre de clave de metadatos </th> 
   <th colname="col2" class="entry"> Valor de metadatos </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR_CODE</span> </td> 
   <td colname="col2"> <p>Código de error nativo del AVE. </p> <p>Estos códigos representan lo siguiente: 
     <ul id="ul_1F33D523DDFE4CE8B4F0DC279FF7E4F8"> 
      <li id="li_07A2D9BEE6364935A61EF3BD4AB6DE27">Errores de DRM (códigos 3300 a 3367). Son los mismos que los códigos de error de Flash Player equivalentes </li> 
      <li id="li_433BA22DE3504AEEB623598BB4F939FA">Errores de reproducción de vídeo (-1 a 89) </li> 
      <li id="li_B347CB151DB94DE0A1DDEB1B33D2DABA">Errores de criptografía (300 a 307) </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR</span> </td> 
   <td colname="col2">Descripción breve de la notificación (por ejemplo, <span class="codeph"> Cupón AXS_Invalid</span> o <span class="codeph"> DECODER_FAILED</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESCRIPCIÓN</span> </td> 
   <td colname="col2"> Descripción larga de la notificación (por ejemplo, error en la operación de resolución de publicidad). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR_CODE</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> valor numérico como cadena (por ejemplo, "13"). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> como una cadena (por ejemplo, <span class="codeph"> kECNetworkError</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ADVERTENCIA</span> </td> 
   <td colname="col2"> Descripción de la advertencia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ERROR</span> </td> 
   <td colname="col2"> Descripción del error. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>DRM</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_SUBERROR_CODE</span> </td> 
   <td colname="col2"> Error menor del módulo DRM. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_STRING</span> </td> 
   <td colname="col2"> Descripción del error. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_SERVER_URL</span> </td> 
   <td colname="col2"> URL del servidor DRM con el que TVSDK intentó hablar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Error de carga de manifiesto de anuncio</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_URL</span> </td> 
   <td colname="col2"> URL del contenido que no se ha podido cargar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_TYPE</span> </td> 
   <td colname="col2">Tipo de anuncio (una constante del <span class="codeph"> MediaResource.Type</span> enum). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_DURATION</span> </td> 
   <td colname="col2"> Duración del anuncio en milisegundos. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_ID</span> </td> 
   <td colname="col2"> ID asignado al anuncio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errores de archivo</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="col2"> Descripción del error durante la descarga del archivo multimedia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> URL</span> </td> 
   <td colname="col2"> URL del archivo que se está descargando. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MANIFEST_ERROR</span> </td> 
   <td colname="col2"> Descripción del error durante la descarga del archivo de manifiesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="col2">Descripción del error durante el fragmento (por ejemplo, <span class="codeph"> ts</span>) descargar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errores de pista de audio</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_NAME</span> </td> 
   <td colname="col2"> Nombre de la pista de audio que no se pudo cargar, como se especifica en el manifiesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_LANGUAGE</span> </td> 
   <td colname="col2"> Idioma de la pista de audio, tal como se especifica en el manifiesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Buscar errores</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_PERIOD</span> </td> 
   <td colname="col2"> ID del periodo (entero). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_POSITION</span> </td> 
   <td colname="col2"> <p>Posición (en milisegundos) buscada (doble). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Varios</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDITUDE_ERROR_CODE</span> </td> 
   <td colname="col2"> Código de error de audiencia (número). </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Valores DRM {#section_D240082B93D34902A18C3923C1C717B3}

La interfaz del Codificador de vídeo del motor de vídeo de Adobe devuelve estas notificaciones DRM en la `NATIVE_ERROR` objeto de metadatos.

Cuando se comuniquen errores de DRM al Adobe, asegúrese de incluir el `NATIVE_SUBERROR_CODE` y `DRM_ERROR_STRING` para obtener ayuda sobre solución de problemas.

>[!TIP]
>
>Esta lista proporciona información específica de TVSDK sobre los errores. Para obtener descripciones completas, consulte [ActionScript Errores en tiempo de ejecución Referencia de ActionScript para Adobe Flash Platform](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#3300).

<table id="table_CD59A859865F4FFDBAA249C89C74770A"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Valor de la clave de metadatos NATIVE_- ERROR_CODE </th> 
   <th colname="col2" class="entry"> Valor de la clave de metadatos NATIVE_ERROR_NAME </th> 
   <th colname="col3" class="entry"> Significado </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 3300 </td> 
   <td colname="col2"><span class="codeph"> Cupón AXS_Invalid</span> </td> 
   <td colname="col3"> 
    <ul id="ul_516E4CB32D624B22892DDB9266CB04CA"> 
     <li id="li_348FC0F38B11417994119B61C9244076">Qué debe hacer el software del distribuidor: 
      <ul id="ul_7AFD45CF92454BA4927783FAA628FBC4"> 
       <li id="li_0D9CCE61612643648C12DCDDD252E52A">Si utiliza Google Chrome, está en modo incógnito y la versión de Flash Player es inferior a 11.6, puede que se produzca este error. <p>Recomendamos que el reproductor compruebe el número de versión del navegador y aconseje al usuario que salga del modo Incognito. </p> </li> 
       <li id="li_1DC6B755BD0840D48BEC92568FD330BA">Vuelva a solicitar la licencia. <p>Si la solicitud se realiza correctamente, no es necesario que registre ni escale. Si la solicitud no se ha realizado correctamente, registre el contenido que provocó el error. <span class="codeph"> subErrorId</span> contiene un error de línea si está presente. </p> </li> 
      </ul> </li> 
     <li id="li_060B5D60C9BB419CBFA7B062FBCF2632">Qué debe hacer el distribuidor: 
      <ul id="ul_FADB29DBF0DA4A0E8E54134AEB7DCD8A"> 
       <li id="li_FC5B1C04D21E4AECB0EBD9ADD3198504">Si los reintentos no tienen éxito en configuraciones que no sean Chrome con un Flash inferior a la versión 11.6, es posible que se haya producido un error en el paquete. </li> 
       <li id="li_A720ECE591254021879B335B81B1F76D">Compruebe si el problema es específico de cierto contenido y vuelva a empaquetar. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3301 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthenticationFailed</span> </td> 
   <td colname="col3"> <p>El servidor no pudo autenticar ni autorizar al cliente. </p> 
    <ul id="ul_BE77AC1848FB4C09B6318359ACF1B8EE"> 
     <li id="li_6FB37D317D174E8488C5070D20CD241C">El software del distribuidor debe realizar todas las acciones necesarias para restablecer las credenciales del usuario o guiar al usuario para adquirir acceso al contenido. </li> 
     <li id="li_BE071D59805B42D38E3E7650BC936417">El distribuidor debe confirmar que el mecanismo de autorización y autenticación del distribuidor funciona correctamente. <p>Si los distribuidores no planean utilizar las funciones de autenticación o autorización, deben comprobar si la directiva del contenido infractor requiere autenticación y ver Diagnóstico de discrepancias de directiva/licencia. </p> </li> 
    </ul> <p>Para obtener más información sobre este código de error, consulte <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> Causas y resolución del error 3301 de DRM</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3302 </td> 
   <td colname="col2"><span class="codeph"> AAXS_RequireSSL</span> </td> 
   <td colname="col3"> <p>En Access 4.0 y versiones posteriores, este error se produce en iOS cuando la dirección URL de clave remota no utiliza HTTPS como esquema. Se requiere HTTPS. </p> 
    <ul id="ul_3D47777BBCA14B67B107FBBE3E37E40C"> 
     <li id="li_7F7BBB27AE754CC39ABAAF9269739C49">Si el distribuidor utiliza una versión anterior a Access v4 o la versión al menos 4 pero la plataforma no es iOS, el software del distribuidor debe registrar el error. <p>El error solo se produce en iOS. </p> </li> 
     <li id="li_D83C427D2A0D47408F723EF7195070B6">Si el software del distribuidor es al menos la versión 4 de Adobe Access y la plataforma es iOS, los distribuidores deben cambiar la URL del servidor de claves remotas que están utilizando a HTTPS. <p>Si solo utilizaran HTTP, es posible que los distribuidores tengan que configurar un servidor HTTPS. De lo contrario, los distribuidores deben enviar la información registrada al Adobe y escalar el problema. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3303 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentExpired</span> </td> 
   <td colname="col3"> <p>El contenido que está viendo ha caducado según las reglas establecidas por el proveedor de contenido. subErrorId contiene un error específico del cliente o un error de línea. </p> <p> 
     <ul id="ul_1E4B3B8AE87A4E79997553BB2A0E52B9"> 
      <li id="li_EE3F2EEBF73743B9A38E4FCB7531E275">El software del distribuidor debe intentar volver a adquirir la licencia del servidor una vez para determinar si hay una nueva licencia no caducada disponible. <p>Si no hay ninguna licencia disponible o la licencia ha caducado, permita al usuario adquirir una nueva o informe al usuario de que el contenido no se puede ver.Si el contenido se ha empaquetado con una directiva que tiene una fecha de caducidad/finalización vencida, el servidor de licencias registra un <span class="codeph"> PolicyEvaluationException</span> y que la fecha de finalización de la directiva ha caducado (código de error del servidor 303). Compruebe los archivos de registro del servidor para comprobarlos. </p> <p>Si es posible, los clientes deben comprobar la directiva que utilizaron durante el empaquetado para ver si ha caducado. La herramienta de línea de comandos de Java es: 
        <code>
         java&nbsp;-jar&nbsp;libs/AdobePolicyManager.jar&nbsp;&nbsp;&nbsp;detail&nbsp;demo.pol
        </code> </p> </li> 
      <li id="li_50DBE680D8F04E7DA3E29C65A93188E7">El distribuidor debe confirmar si las fechas de caducidad de la licencia están configuradas según lo previsto. </li> 
     </ul> </p> <p>Para obtener más información sobre este código de error, consulte <a href="https://forums.adobe.com/thread/1300813" format="https" scope="external"> 3303 (Contenido caducado) con AMS/FMS mediante una emisión en directo?</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3304 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthorizationFailed</span> </td> 
   <td colname="col3">Para obtener más información sobre este código de error, consulte <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> Causas y resolución del error 3301 de DRM</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3305 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerConnectionFailed</span> </td> 
   <td colname="col3"> <p>Se agotó el tiempo de espera de la conexión a los servidores de licencias o de dominio, ya sea debido a un retraso de la red o a que el cliente estaba sin conexión. Normalmente subErrorId contiene código de retorno HTTP. </p> 
    <ul id="ul_938C7D8F07F64B4FA71A09DDF37E2E64"> 
     <li id="li_6648EA0049094E369BD9AE9CCA6B148D">El software del distribuidor debe intentar establecer una conexión de red con un servidor correcto. <p>Si el intento falla, solicite al usuario que vuelva a conectarse a la red. Si el intento se realiza correctamente, regístrelo. </p> </li> 
     <li id="li_2ECA2C04BA08449DA3AD79A52EFAA229">El distribuidor debe comprobar que todos los servidores de licencias y de dominio en uso están en línea y son visibles desde la red del cliente. </li> 
    </ul> <p>Para obtener más información sobre este código de error, consulte <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> Causas y resolución de DRM 3305 [ServerConnectionFailed]</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3306 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClientUpdateRequire</span> </td> 
   <td colname="col3"> Utilice una versión más reciente de TVSDK para Android. <p>El cliente actual no puede completar la acción solicitada, pero es posible que un cliente actualizado pueda completar la solicitud. </p> <p>Esto puede tener varias causas: 
     <ul id="ul_2EC4D42D5273439FA1AFDA1A2578B3D6"> 
      <li id="li_FCA926F5FAED4E7190BE855545AB6ACF">Se ha utilizado un dominio compartido que no está disponible en este cliente. Probablemente este sea el caso cuando la reproducción funciona en Chrome, pero no en cualquier otro navegador y viceversa. <p> <p>Sugerencia: Chrome utiliza una clave PHDS/PHLS diferente a la de los demás exploradores. Para obtener más información, consulte <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </p> </li> 
      <li id="li_3B633FB699234DCEA136E9BE3CC3386D">La aplicación intenta agregar varias sesiones de DRMS cuando se ejecuta en una versión de iOS anterior a la 5.0. </li> 
      <li id="li_F7ED993AF0B941A7A27216B4D587A999">Los metadatos tienen una versión de 3 o superior cuando solo se admite la versión 2. </li> 
     </ul> </p> 
    <ul id="ul_EE4AE6AD4F1745A5B5623E53B599DB62"> 
     <li id="li_7A83869D4262443DA35FA1DF8D3097DD">El software del distribuidor debe alertar al usuario y cancelar la operación. <p>Si el software tiene alguna forma de determinar si hay una actualización disponible, dirija al usuario a esa actualización de la manera adecuada para la plataforma. </p> </li> 
     <li id="li_AF9C2711FDE54DA196EB9D2864632000">Si el problema se produce debido a un dominio compartido, el distribuidor deberá comprobar con el Adobe si hay un tiempo de ejecución o una biblioteca actualizados. <p>Para el tiempo de ejecución del Flash, el distribuidor puede forzar la actualización directamente en su aplicación. En el caso de una biblioteca, el distribuidor deberá obtener una biblioteca actualizada, volver a compilar su aplicación e implementarla para sus usuarios. </p> <p>Si el problema se produce debido a varias sesiones de DRMS, el distribuidor deberá actualizar su aplicación para comprobar el número de versión de iOS antes de añadir varias sesiones de DRMS. O pueden restringir la distribución de su aplicación a iOS v5 o posterior. </p> <p>si el problema se produce porque la versión de los metadatos es superior a la versión 2, es probable que los metadatos estén dañados. Pueden intentar reconstruir los metadatos y ver los resultados. Si el problema persiste, registre el problema y vuelva a los Adobes. </p> </li> 
    </ul> <p>Para obtener más información sobre este código de error, consulte <a href="https://forums.adobe.com/thread/1266675" format="https" scope="external"> Cómo corregir un código de error 3306 DRMErrorEvent</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3307 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InternalFailure</span> </td> 
   <td colname="col3"> <p>Esto generalmente representa un error en el código de acceso de Adobe y es inesperado, a menos que haya un error conocido, como se muestra a continuación. subErrorId contiene un error específico del cliente o un error de línea. </p> 
    <ul id="ul_79F4A9655A2148519B1E9509C41F78C3"> 
     <li id="li_0E093AB4D6BD489B852279E6C1525A15">Si el navegador es Chrome en Windows y la versión de Flash es 11.6 (versión de SWF 19 o buena), el software del distribuidor debe suponer que el usuario pulsó <span class="uicontrol"> Denegar</span> en la barra de información y tratar lo mismo que un 3368. </li> 
     <li id="li_0215D1089B344861A2C0A73E1067CFEF">Si 3307 se produce cuando el explorador no es Chrome o la versión de Flash no es 11.6, el distribuidor debe escalar a Adobe. </li> 
    </ul> <p>Importante: <span class="codeph"> 3307:1107296344 (FailedToGetBrokerHandle)</span> puede ocurrir con las versiones 24-28 del explorador Chrome. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3308 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WrongLicenseKey</span> </td> 
   <td colname="col3"> <p>Este error se produce siempre que la licencia que se está utilizando contiene la clave incorrecta para descifrar el contenido. subErrorId contiene un error específico del cliente o un error de línea. </p> <p>Parece que solo hay dos formas de generar este error: 
     <ul id="ul_1C955BD74C7843809D1B5A0CDCA5ED7B"> 
      <li id="li_18F0A7FDA6584887AD9DB3EDE54080D8">El cliente ha modificado la herramienta de Adobe estándar para generar licencias (por ejemplo, el módulo Java del servidor de licencias). <p>En este caso, la licencia contiene una clave incorrecta que podría no corresponder a ningún contenido. </p> </li> 
      <li id="li_21D04ED1F1FA464785BC297D385766FF">El cliente ha emitido varias licencias con el mismo ID de licencia. <p>En este caso, hay varias licencias disponibles en el cliente que coinciden con los metadatos de contenido y el código de acceso ha seleccionado la incorrecta para usarla. </p> </li> 
     </ul> </p> 
    <ul id="ul_64AEE62BE36946F290067CF475A36ECA"> 
     <li id="li_9EEB2B11A4DA41E78C5840D8FAA81F0D">El software del distribuidor debe intentar volver a adquirir la licencia del servidor. 
      <ul id="ul_ACADC5518B054D0A853AEED2B675DB23"> 
       <li id="li_394835C8731048A5BF7D9370AC12448C">Si no hay ninguna licencia disponible o la licencia ha caducado, proporcione un flujo de trabajo para que el usuario adquiera una nueva licencia o informe al usuario de que el contenido no se puede ver y registrar el problema. </li> 
       <li id="li_3FE50518BE53405F9563FA620F7EAD5F">Si se trata de contenido enlazado a un dominio (para AIR), proporcione un medio para que el usuario se una al dominio. </li> 
      </ul> </li> 
     <li id="li_C80B353C1AEA4E9398241420CB491E84">El distribuidor debe: 
      <ul id="ul_B5C50009374C4EED9B2B050B48F5F0F6"> 
       <li id="li_D5E6B760E0BC4B5C949ED1544B398838">Compruebe que no ha personalizado las partes de emisión de licencias del servidor de licencias de acceso. </li> 
       <li id="li_AA8F4E4B6DDD40BA8807C0920A92186B">Compruebe que están emitiendo ID de licencia únicos para todas las licencias. </li> 
       <li id="li_A2C53FE779AC4FDDB65E00A2C4F43EC4">Solucione el problema con el Adobe. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3309 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedAdditionalHeader </span> </td> 
   <td colname="col3"> <p>Esto ocurrirá si el encabezado tiene más de 65536 bytes. </p> 
    <ul id="ul_82C0F688519B4F43A764D59A891F1903"> 
     <li id="li_E66AC9149A0649E88A79C5289C12C395">El software del distribuidor debe registrar qué fragmento de contenido provocó el error. </li> 
     <li id="li_1C5916A33E7B4DC9968105B9BD20A727">El distribuidor debe confirmar que el error es reproducible con fragmentos de contenido específicos. Volver a empaquetar contenido dañado. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3310 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppIDMismatch </span> </td> 
   <td colname="col3">La aplicación de Android no coincide con la utilizada. <p>No se está utilizando la aplicación AIR o el SWF de Flash correctos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3311 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppVersionMismatch </span> </td> 
   <td colname="col3"> No está en uso. Este problema podría seguir generándose por la pila de la versión 1.x en AIR. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3312 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LicenseIntegrity </span> </td> 
   <td colname="col3"> Para solucionarlo, vuelva a descargar la licencia desde el servidor. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3313 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WriteMicrosafeFailed </span> </td> 
   <td colname="col3"> <p>Este problema se produce cuando el sistema no puede escribir en el sistema de archivos. <span class="codeph"> subErrorId</span> contiene un error específico del cliente o un error de línea. </p> <p>En Microsoft Windows, el error 3313 puede ser producido por Active X o NPAPI plug flash player cuando el contenido cifrado tiene un ID de licencia o un ID de directiva que es demasiado largo. Esto se debe a la longitud máxima de la ruta en Windows. (El complemento Pepper no tiene este problema). </p> <p>Consulte Watson 3549660 </p> 
    <ul id="ul_DFD527D1E1224A439766DF7BED878E3B"> 
     <li id="li_FAF8FD98A4E8478CA7A92F770676ADFC">El software del distribuidor debe pedir al usuario que confirme que su directorio de usuario no está bloqueado ni en un volumen que esté lleno o bloqueado. </li> 
     <li id="li_6D1136EA750A459BBECEEE5F73F527BB">Si el distribuidor utiliza AIR, en lugar de Flash, el problema puede deberse a una limitación de longitud de ruta. <p>Los distribuidores deben reducir el nombre de su aplicación de AIR a algo razonable. Además, vuelva a publicar el contenido con un más corto <span class="codeph"> licenseID</span> y una <span class="codeph"> policyID</span>. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3314 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedDRMetadata </span> </td> 
   <td colname="col3"> <p>Este error suele indicar que el contenido se empaquetó con certificados PKI de prueba y que el reproductor se creó con PKI de producción o viceversa. subErrorId contiene un error específico del cliente o un error de línea. </p> 
    <ul id="ul_A122EF304CAF48A8B4DA1E3F4413E29B"> 
     <li id="li_A9A1A5B23E884C22A71E2DE7535FEB3B">El software del distribuidor debe registrar qué fragmento de contenido provocó el error. </li> 
     <li id="li_7AD7F13A4B1B4998A7E49664E7645815">El distribuidor debe confirmar que el error se puede reproducir con fragmentos de contenido específicos. <p>Es posible que tenga que volver a empaquetar el contenido dañado. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3315 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PermissionDenied </span> </td> 
   <td colname="col3"> <p>Hay errores conocidos en los que se produce este código de error cuando se pretende un 3305. Para obtener más información, consulte <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> Causas y resolución de DRM 3305 [ServerConnectionFailed]</a>. </p> <p>El SWF remoto cargado por AIR no tiene permiso para acceder a la funcionalidad de Flash Access. Este código de error también se puede generar si se produce un error de seguridad durante el acceso a la red. Algunos ejemplos son que el servidor de destino no envía al cliente la conexión mediante cross-domain.xml o que no se puede acceder a cross-domain.xml. </p> <p>Para obtener más información, consulte <a href="https://forums.adobe.com/thread/1266592" format="https" scope="external"> Error de DRM 3315 posible causa raíz y resolución</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3316 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NOTUSED_MOVED </span> </td> 
   <td colname="col3"> Era <span class="codeph"> ADOBECPSHIM_MinorErr_MissingAdobeCPModule</span>. Se ha movido a 3344 debido a un conflicto con el código de error de Flash. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3317 </td> 
   <td colname="col2"><span class="codeph"> Error de AAXS_LoadAdobeCPFail </span> </td> 
   <td colname="col3"> <p>Importante: Se trata de un error poco frecuente que no suele producirse en un entorno de producción. </p> <p>Si se produce el error, puede realizar una de las siguientes acciones: 
     <ul id="ul_BC435E61623444BB98A86216531DC892"> 
      <li id="li_FA433D0758B642D2AFDCF04906B3FE18">Si utiliza AIR, vuelva a instalarlo. </li> 
      <li id="li_F08D9AAFF46244F8842DEE5FD9CBBE0A">Si utiliza el Flash Player, descargue el <span class="codeph"> AdobeCP</span> módulos de nuevo. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3318 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncompatibleAdobeCPVersion </span> </td> 
   <td colname="col3"> No aplicable a Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3319 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPGetAPI </span> </td> 
   <td colname="col3"> No aplicable a Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3320 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HostAuthenticateFailed </span> </td> 
   <td colname="col3"> No aplicable a Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3321 </td> 
   <td colname="col2"><span class="codeph"> AAXS_I15nFailed </span> </td> 
   <td colname="col3"> <p>Error en el proceso de aprovisionamiento del cliente con claves. subErrorId contiene un error de línea, específico del servidor o específico del cliente. </p> 
    <ul id="ul_98D919B9060A441AACB6106F6D8E8DA7"> 
     <li id="li_DCAB00A8AC4A426CBBD377374B3F71AE">El software del distribuidor debe reintentar la operación al menos una vez. <p>Si utiliza Google Chrome en Windows, proporcione una explicación sobre cómo permitir el acceso a complementos que no están en una zona protegida. Acceso denegado a la zona protegida de Google Chrome</a>. </p> </li> 
     <li id="li_7FB7681FE32D444BB1BDBA3E5953A2C3">El distribuidor debe realizar una de las siguientes tareas: 
      <ul id="ul_486B64F187C44AE3B4775953A6142836"> 
       <li id="li_095B1D4CD051427CB2BFA7082B454056">Si el error es consistente entre plataformas, debe escalar el problema con Adobe. </li> 
       <li id="li_0C6EB7B912FA41E59657216498DA3515">Si el error está limitado a Chrome en Windows, guíe al usuario para permitir el acceso al complemento sin zona protegida. </li> 
      </ul> <p>Los distribuidores deben actualizar su SWF a la versión 19 o posterior y, si se produce el error 3321 específico de Chrome, se generará un error 3368. El software del distribuidor puede gestionar el error 3368 de forma más específica. Este cambio se introdujo en la versión 26.0.1410.43 del canal Chrome Stable. </p> <p>Sugerencia: Error <span class="codeph"> 3321:1090519056</span> puede ocurrir con las versiones de Flash Player 11.1 a 11.6. Le recomendamos que actualice a la última versión de Flash Player. </p> </li> 
    </ul> <p>Para obtener más información, consulte <a href="https://forums.adobe.com/thread/1277138" format="https" scope="external"> Error DRM 3321 Causas y resolución</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errores de corrupción del almacén global</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3322 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DeviceBindingFailed </span> </td> 
   <td colname="col3"> <p>El dispositivo no parece coincidir con la configuración que estaba presente cuando se inicializó. subErrorId contiene un error de línea o específico del cliente. </p> <p>El software del distribuidor debe completar una de las siguientes tareas: 
     <ul id="ul_444401051A2E407B95BC44491E9BB71C"> 
      <li id="li_93493EA05DB44CB1AEC368663F1ABA8D"> <p>Si el dispositivo no utiliza el Flash Player y AIR, iOS, etc., llame a <span class="codeph"> DRManager.resetDRMVouchers()</span>. </p> <p>Si el problema se produce en iOS en una fase de desarrollo, pida al desarrollador que confirme si el problema se observa al cambiar entre compilaciones descargadas de sistemas de distribución de versiones anteriores al lanzamiento de terceros (por ejemplo, HockeyApp) y una compilación local de Xcode. Los atributos de una instalación anterior no se sobrescriben por completo al cambiar entre una compilación distribuida desde HockeyApp y una compilación de Xcode. Esta situación podría almacenar en déclencheur el error 3322. </p> <p>Para resolver este problema, el desarrollador debe eliminar la compilación anterior del dispositivo antes de instalar la nueva compilación. </p> </li> 
      <li id="li_A5C9633F11584C788A2D9A23CC18FA6D">Si el dispositivo utiliza Flash Player y no se puede utilizar a partir de los códigos de error 3322 o 3346, consulte las instrucciones del Adobe sobre cómo restablecer mediante programación el almacén de licencias DRM en <a href="https://forums.adobe.com/message/5535907#5535907" format="https" scope="external"> Error DRM 3322/3346/3368 en Chrome (problemas de la barra de información)</a>. </li> 
     </ul> </p> <p>No se espera que este error se produzca con frecuencia. En entornos corporativos que utilizan perfiles móviles, si un usuario estaba viendo contenido protegido por DRM, la probabilidad de que se produzca el error 3322 aumenta a medida que el usuario inicia sesión desde diferentes equipos. Si es posible, el distribuidor debe intentar obtener esta información del usuario. </p> <p>Si el error se produce con frecuencia, escale al Adobe. Debe notificar al Adobe si el restablecimiento del almacén de licencias ha resuelto (o no) el problema e indicar al Adobe en qué exploradores se está produciendo el error. </p> <p>Para obtener más información, consulte los siguientes artículos: 
     <ul id="ul_C468409D1EA046178CA7F54DCDCB84EA"> 
      <li id="li_20C8CA3853574CE486F21E7A3667DAB9"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> https://forums.adobe.com/message/5520902</a> </li> 
      <li id="li_6E6F1BD6FE7843449B3E2F06F342EFF7"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> https://forums.adobe.com/message/5535911</a> </li> 
      <li id="li_2BE40E513A0C4BAD900C7B69FEF5D690"><a href="https://forums.adobe.com/message/5748618" format="https" scope="external"> https://forums.adobe.com/message/5748618</a> </li> 
      <li id="li_9C2BD122E3874E2893DD43E082A877E0"><a href="https://forums.adobe.com/message/6061165" format="https" scope="external"> https://forums.adobe.com/message/6061165</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3323 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptGlobalStateStore </span> </td> 
   <td colname="col3"> <p>Los ficheros utilizados por el cliente DRM se han modificado inesperadamente. subErrorId contiene un error de línea o específico del cliente. </p> 
    <ul id="ul_96EA771046CA4B2B9FAE24D493F43FF2"> 
     <li id="li_D2693CD8EFEF46108828BA17E3F54FF6">El software del distribuidor debe guiar al usuario para restablecer de la misma manera que para 3322. </li> 
     <li id="li_0149B82436B64E28AC2B8C9B0EB09898">Si el GlobalStore está fallando a una velocidad buena a la tasa de fallo esperada de los discos duros de su base de usuarios, escale el problema al Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3324 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MachineTokenInvalid </span> </td> 
   <td colname="col3"> Restablecer el almacenamiento local de DRM para esta aplicación. Llame a DRManager.resetDRM. <p>Es posible que el servidor de licencias no pueda conectarse al servidor de lista de revocación de certificados (CRL) para actualizar sus archivos CRL o que el equipo cliente solicite una licencia o autenticación revocada por el servidor de licencias. </p> <p>En los registros del servidor, un código de error 111 es MachineTokenInvalid. Sin embargo, en el nivel de cliente, el código de error 111 se traduce en el código de error 3324. </p> <p>El administrador del servidor de licencias DRM debe comprobar si el servidor de licencias del cliente ha podido recuperar alguna vez los archivos CRL de Adobe. Si el cliente utiliza Tomcat, puede comprobar el<span class="filepath"> tomcat/temp/</span> para ver si hay 4 archivos CRL. </p> 
    <ul id="ul_23B7F1A104AF49E79EA87DB8E15E337E"> 
     <li id="li_855D87F251184FE688A8D5FA0F6C9EF5">Si los archivos se encuentran en este directorio, haga doble clic en los archivos del Explorador de Windows y, en la aplicación de visor de CRL, determine si alguno de los archivos ha caducado. </li> 
     <li id="li_58EC4EDA2B5146188A0FF7B33C91E2FD">Si no hay archivos en tomcat/temp/, se puede suponer que este servidor de licencias nunca ha podido acceder al servidor CRL de Adobe debido a un problema de firewall/enrutamiento. </li> 
    </ul> <p>Para obtener más información, consulte <a href="https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_secure_deployment_guidelines.pdf" format="http" scope="external"> Reglas del cortafuegos</a>. </p> <p>Si los archivos CRL no están disponibles o han caducado, debe confirmar si se puede contactar con el servidor de licencias. Abra un detector de red en el servidor de licencias del cliente, reinicie el servidor e intente que un cliente solicite una licencia al servidor. Puede observar el tráfico de red para ver si las llamadas a los siguientes extremos de URL se realizan correctamente: <p>Sugerencia: También puede introducir las siguientes direcciones URL de CRL en un explorador para ver si puede descargar manualmente cada archivo. </p> 
     <ul id="ul_9B65C7ABBDEC4AC9BF3755FFD3587971"> 
      <li id="li_6867A9050E8D421C9138AC853D1784C9"><a href="https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl</a> </li> 
      <li id="li_6431689260554EAFAFDA2EC31798DCB5"><a href="https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl</a> </li> 
      <li id="li_2939674D0F854ADEB67E45FD216288A2"><a href="https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessRootCA.crl</a> </li> 
      <li id="li_96386E00BE9D4CB99D100057A5F7C6DD">crl3.adobe.com/AdobeSystemsIncorporated FlashAccessRuntime/LatestCRL.crl</li> 
     </ul> </p> <p>Si las reglas del firewall están abiertas y no hay errores actuales de 3324, es posible que haya un problema de red temporal. Compruebe los registros del servidor del cliente, que probablemente están en la <span class="codeph"> /tomcat/logs/</span> , para determinar si se produjo un error cuando el servidor de licencias intentó recuperar las listas de revocación de certificados. <p>Importante: Se puede producir un error cuando un gran número (o una ráfaga) de clientes informan de un error 3324 a un problema temporal de red al renovar un archivo CRL. Cuando se resolvió el problema de red, también se resolvieron los problemas 3324. </p> </p> <p>Si los 4 archivos CRL existen en el <span class="filepath"> tomcat/temp/</span> y los clientes siguen obteniendo códigos de error 3324, puede haber problemas de acceso a los archivos CRL. Para resolver este problema, es posible que desee revisar los registros y purgar los archivos de CRL existentes. </p> <p>Si no hay problemas con el servidor, pida al usuario que se restablezca en como se describe en 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errores de corrupción del almacén del servidor</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3325 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptServerStateStore </span> </td> 
   <td colname="col3"> <p>Los ficheros utilizados por el cliente DRM se han modificado inesperadamente. <span class="codeph"> subErrorId</span> contiene un error de línea o específico del cliente. </p> 
    <ul id="ul_860D2402DA61460AB0D938F1116F6D64"> 
     <li id="li_CF368C43452B4265B62ADA3E223894BA">El software del distribuidor debe volver a intentar la operación, ya que AdobeCP ha eliminado internamente el almacén del servidor infractor y se debe realizar un reintento correctamente. Si el reintento falla, registre el problema. </li> 
     <li id="li_51A5803A1F754970BB4EBD6494F5DC96">Si los reintentos fallan a una tasa buena a la tasa de errores esperada en los discos duros de su base de usuarios, escale el problema al Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3326 </td> 
   <td colname="col2"><span class="codeph"> AAXS_StoreTamperingDetected </span> </td> 
   <td colname="col3"> Llamada <span class="codeph"> DRManager.resetDRM</span>. <p>El almacén de licencias se ha manipulado o dañado y ya no se puede utilizar. </p> <p>El software del distribuidor debe guiar al usuario para restablecer de la misma manera que se describe en 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3327 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClockTamperingDetected </span> </td> 
   <td colname="col3"> Corregir el reloj o adquirir <span class="codeph"> Autor/Lic/Dominio</span> Licencia de nuevo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errores del servidor de autenticación/licencia/dominio</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3328 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerErrorTryAgain </span> </td> 
   <td colname="col3"> <p>Se trata de un error del lado del servidor en el que el servidor no pudo completar la solicitud del cliente. Este error se puede producir cuando, por ejemplo, el servidor está ocupado, HTTP/500, el servidor no tiene la clave necesaria para descifrar la solicitud, etc. </p> <p>En el cliente, no hay forma de determinar qué ha fallado. El cliente debe revisar los registros del servidor de acceso a Adobe, a los que se suele llamar <span class="codeph"> AdobeFlashAccess.log</span>, para determinar qué ha fallado. Siempre hay un seguimiento de pila descriptivo en el registro para indicar el problema. <span class="codeph"> subErrorId</span> contiene un error de línea o específico del servidor. </p> <p>El distribuidor debe consultar los registros del servidor para identificar qué servidor envía este error. Para errores 3328 con un código de suberror 101, el servidor no puede descifrar la solicitud. El cliente debe comprobar que los certificados de servidor de licencias/transporte instalados en el servidor de licencias coinciden y se corresponden con los certificados utilizados durante el empaquetado. </p> <p>Además, si los clientes utilizan la Implementación de referencia, deben asegurarse de que no haya errores tipográficos en la <span class="codeph"> flashaccess-refimpl.properties</span> archivo donde se especifican los certificados principales y adicionales. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3329 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ApplicationSpecificError </span> </td> 
   <td colname="col3"> <p>El código de suberror específico de la aplicación no se conoce para el Flash Access. <span class="codeph"> subErrorId</span> contiene un error específico del servidor procedente del servidor de licencias personalizado de los editores. El servidor devolvió un error en el espacio de nombres específico de la aplicación. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3330 </td> 
   <td colname="col2"><span class="codeph"> AXS_NeedAuthentication </span> </td> 
   <td colname="col3"> <p>Este error se produce cuando el contenido se configura para pedir a los clientes que se autentiquen antes de obtener las licencias. </p> 
    <ul id="ul_712D29B8B5A6401FB014C4A283918E32"> 
     <li id="li_2D56905EB50D4FDEAD69CA8EAE38AD1A">El software del distribuidor debe autenticar al usuario y, a continuación, adquirir la licencia de nuevo. <p>Si el servicio no tiene intención de utilizar la autenticación, registre la identificación del contenido que causa este error. </p> </li> 
     <li id="li_B3BCF899B8BE41C7A4F7CF84B0503483">Este error no debería requerir una escalación, a menos que no se suponga que el contenido debe configurarse para requerir autenticación. <p>En este caso, vuelva a empaquetar el contenido ofensivo con la política adecuada. Si el contenido se empaqueta correctamente, consulte Diagnóstico de discrepancias de directivas/licencias. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Errores de aplicación de licencias no cubiertos anteriormente</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3331 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentNotyetValid </span> </td> 
   <td colname="col3"> <p>La licencia adquirida aún no es válida. Para resolver este problema, compruebe si el reloj del cliente no está configurado correctamente. Para configurar el reloj del cliente, vuelva a empaquetar el contenido o modifique la configuración del servidor de licencias. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3332 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CachedLicenseExpired </span> </td> 
   <td colname="col3"> Vuelva a adquirir la licencia del servidor. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3333 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PlaybackWindowExpired </span> </td> 
   <td colname="col3"> <p>Debe notificar a los usuarios que no pueden reproducir este contenido hasta que caduque la directiva. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3334 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMPlatform </span> </td> 
   <td colname="col3"> <p>Esta plataforma no tiene permiso para reproducir el contenido porque, por ejemplo, el proveedor de contenido ha configurado el acceso de Adobe para denegar el contenido al acceso de Adobe en una plataforma o una licencia compartida enlazada a un dominio está enlazada a un token de dominio compartido que está pensado para una partición diferente. </p> <p>CDM podría generar este error si el contenido no se ha empaquetado mediante una certificación de empaquetador adecuada (con puerta de funciones CDM). </p> <p>Si el contenido está empaquetado con un certificado PHDS/PHLS incorrecto, el contenido puede funcionar en Chrome pero no en otros navegadores (o viceversa). <p>Sugerencia: Esto se debe a que Chrome utiliza diferentes certificados PHDS/PHLS. </p>Para confirmar qué certificado se está utilizando, volque los detalles de los metadatos de contenido y busque <i>certificados de destinatario</i>. Para obtener más información, consulte <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3335 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMVersion </span> </td> 
   <td colname="col3"> Actualice a la última versión de TVSDK para Android. <p>Para resolver este problema, complete una de las siguientes tareas: 
     <ul id="ul_BF1742948BC9461CB8686DE70124D3CD"> 
      <li id="li_690D440C94CC45A0AE55EC319B1C4C23">Actualizar AIR </li> 
      <li id="li_CDD20251C881466E88BE7BBB53D61EBC">Para Flash Player, actualice el módulo AdobeCP e intente la reproducción de nuevo. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3336 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimePlatform </span> </td> 
   <td colname="col3"> <p>Esta plataforma no tiene permiso para reproducir el contenido porque, por ejemplo, el proveedor de contenido ha configurado Access para denegar contenido a FP/AIR en una plataforma. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3337 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimeVersion </span> </td> 
   <td colname="col3"> Actualice a la última versión de TVSDK para Android. <p>Esto ocurre si el contenido o el servidor están configurados para denegar la reproducción a una versión concreta de los tiempos de ejecución de Flash o AIR. </p> 
    <ul id="ul_B0732D941256483CABBDD30C9BF43249"> 
     <li id="li_72782B1D638F48C0B87084689FB9C798">Si el usuario se encuentra en un sistema operativo en el que se puede actualizar el Flash, el software del distribuidor debe solicitar al usuario que actualice el Flash e intentarlo de nuevo. De lo contrario, aconseje al usuario que utilice un equipo diferente. </li> 
     <li id="li_1E3FD93CE39E43F2B7D961299B1211DA">Si se sospecha el error 3337, identifique si se está produciendo para un contenido específico y vuelva a empaquetar ese contenido. Si el contenido está empaquetado correctamente, consulte Diagnóstico de discrepancias de directivas/licencias </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3338 </td> 
   <td colname="col2"><span class="codeph"> AXS_UnknownConnectionType </span> </td> 
   <td colname="col3"> <p>No se puede detectar el tipo de conexión y la directiva requiere que active la protección de salida. Este problema solo se produce si el contenido está empaquetado para requerir protección de salida digital o analógica. </p> <p>Un problema en las versiones de Flash Player anteriores a la versión 11.8.800.168 provocaba que se produjera el error 3338 ocasionalmente en contenido para el que la directiva indicaba que la protección de contenido es <span class="codeph"> USAR SI ESTÁ DISPONIBLE</span>. Este problema se corrige en la versión 11.8.800.168 y posteriores de. </p> 
    <ul id="ul_4B6CA26A53F84838B5B95400925464D4"> 
     <li id="li_CBD890F467E449EBB5116E1561252058">El software del distribuidor selecciona una variante del contenido que no requiere protección de salida (por ejemplo, la variante SD de un flujo HD). <p>Si el error 3338 se produce el <span class="codeph"> USE_IF_AVAILABLE </span> contenido, compruebe el número de versión del reproductor. Si la versión del reproductor es inferior a 11.8.800.168, aconseje al usuario que actualice el Flash Player. Si el error 3338 se produce en versiones superiores a 11.8.800.168, registre qué contenido provocó el error. </p> </li> 
     <li id="li_62886C1D96264B129928A7E29E6C70E1">El distribuidor debe comprobar qué contenido está causando este error y validar que la directiva del contenido está establecida <span class="codeph"> NO_PROTECTION</span> o <span class="codeph"> USE_IF_AVAILABLE</span> para salidas analógicas y digitales. <p>Si el contenido se empaqueta inadvertidamente con <span class="codeph"> NO_OUTPUT</span> o <span class="codeph"> OBLIGATORIO</span>, vuelva a empaquetar el contenido. Si el contenido está empaquetado correctamente, consulte Diagnóstico de discrepancias de directivas/licencias. De lo contrario, escalar al Adobe. </p> </li> 
    </ul> <p>Para obtener más información, consulte <a href="https://forums.adobe.com/message/5518688" format="https" scope="external"> ¿Se están obteniendo errores 3338 inesperados cuando la directiva DRM está configurada en USE_IF_AVAILABLE?</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3339 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogPlaybackAllowed </span> </td> 
   <td colname="col3"> No se puede reproducir en el dispositivo analógico. Para resolver el problema, conecte un dispositivo digital. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3340 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogProtectionAvail </span> </td> 
   <td colname="col3"> No se puede reproducir contenido porque el dispositivo de visualización externo analógico conectado (monitor/TV) no tiene las capacidades correctas (por ejemplo, el dispositivo no tiene Macrovision o ACP). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3341 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalPlaybackAllowed </span> </td> 
   <td colname="col3"> No se puede reproducir contenido en un dispositivo digital. <p>Importante: Este problema no debería producirse en un entorno de producción, ya que los editores de contenido no deberían impedir la reproducción digital. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3342 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalProtectionAvail </span> </td> 
   <td colname="col3"> El dispositivo de visualización externo digital (monitor/TV) conectado no tiene las funciones correctas. Por ejemplo, el dispositivo no tiene HDCP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3343 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IntegrityVerificationFailed </span> </td> 
   <td colname="col3"> <p>No aplicable a Android. </p> <p>Actualmente se sabe que este error ocurre inicialmente después de que se publique una nueva versión de Flash. Se produce porque el Flash se actualizó mientras el Flash estaba abierto, lo que pone el Flash en un estado incorrecto hasta que se reinicia el explorador. </p> 
    <ul id="ul_A0AC4A77550E40409A04BD33748EA987"> 
     <li id="li_F41C1ABD838D41ABB0DF65093E664A29">El software del distribuidor debe completar las siguientes tareas: 
      <ul id="ul_79B2AB1372074D448F129851AA24F985"> 
       <li id="li_B93EDD263D78434FAF198A01938D3508">Se recomienda que el usuario cierre o cierre todos los exploradores y vuelva a abrirlos. </li> 
       <li id="li_ADFBCFA66AD849E18DB390455458528E">Compruebe si la versión del Flash es la actual. <p>Si la versión no es la actual, indique al cliente que actualice, cierre todas las pestañas del explorador y vuelva a abrir. </p> </li> 
      </ul> </li> 
     <li id="li_281B54582B5949AEA7D166246917EE41">Si parece que se produce un error después de que se reinicie correctamente el explorador, escale al Adobe. <p>Cuando se publique una versión nueva, le recomendamos que se ponga en contacto con el Soporte técnico de Adobe para ver si el problema de las actualizaciones en segundo plano se ha corregido. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3344 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPModule </span> </td> 
   <td colname="col3"> No aplicable a Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3345 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DRMNoAccessError </span> </td> 
   <td colname="col3"> <p>No aplicable a Android. </p> <p>Este error se produce cuando parte del Flash o AIR no se instaló correctamente. </p> <p>El software del distribuidor debe realizar una de las siguientes acciones: 
     <ul id="ul_D1188E2D4FDF4BD89A04F5629D75D981"> 
      <li id="li_B33FBCA5D4534D668B86A5E93DB3A809">Pida al usuario que desinstale y vuelva a instalar AIR. </li> 
      <li id="li_B7D2388E9FA84C26AF1C87B48AF9EF16">Para el Flash Player, llame a <span class="codeph"> System.update</span>. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3346 </td> 
   <td colname="col2"><span class="codeph"> AXS_MigrationFailed </span> </td> 
   <td colname="col3"> 
    <ul id="ul_518AD4931CC64EB3A962DD451E6C5067"> 
     <li id="li_3C44F0740B08490E9C62D89C40B57DC2">El software del distribuidor debe realizar una de las siguientes acciones: 
      <ul id="ul_7D90526684BF4EB2BBADCF598AA13086"> 
       <li id="li_D15B4BEDAF7340F6B9BC886DF6E346EC">Si AIR, llame a <span class="codeph"> DRManager.resetDRMVouchers()</span> </li> 
       <li id="li_40A51D35408249CFA28DBC49FDA3408B">Si el Flash tiene un código de error 3322 o 3346 que no se puede utilizar, los usuarios deben ir a <a href="https://forums.adobe.com/message/5535907#5535907" format="http" scope="external"> https://forums.adobe.com/message/5535907#5535907</a> y siga las instrucciones del artículo Adobe para restablecer mediante programación su almacén de licencias DRM. </li> 
      </ul> </li> 
     <li id="li_0464471E4A094C80BF2986694341921A">Si este error se produce con frecuencia, el distribuidor debe proporcionar los detalles sobre la versión del reproductor de frecuencias y la versión del navegador para el Adobe. </li> 
    </ul> <p>Para obtener más información, consulte los siguientes artículos de foros: 
     <ul id="ul_44E0077FEAA749CC9549BF3846065304"> 
      <li id="li_2BE3B2443380415DA73B7AA3B6547B31"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Error DRM 3322/3346/3368 en Chrome (problemas de la barra de información)</a> </li> 
      <li id="li_4E5C7414756644E1AB78BE7B8112228C"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> Error 3322 o 3346 tras el cambio de hardware</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3347 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InsuficienteDeviceCapabilites </span> </td> 
   <td colname="col3"> <p>El significado principal de este error es que la licencia tiene una restricción que el certificado DRM del cliente indica que no puede satisfacer. Las siguientes "capacidades de hardware" se definen cuando se emite el certificado DRM de cliente: 
     <ul id="ul_1EB6F1469C244CF0BA52C212495C053D"> 
      <li id="li_646043CE045C4DE2BBC939E1F4963DFE"><b>Bus no accesible para el usuario</b>. If <b>true</b>Sin embargo, los medios descifrados nunca fluyen a través de un bus ni a la memoria principal donde una aplicación puede acceder a ellos. <p>If <b>false</b>, el contenido puede ser accesible para la aplicación después del descifrado. </p> </li> 
      <li id="li_02AAECAF4D35447BA10554541B46DE67"><b>Raíz de confianza de hardware</b>. If <b>true</b>, todo el software que se carga en el momento del inicio en el dispositivo se validó con una clave o compendio que solo está disponible en el hardware. <p>Ambas restricciones se comprueban en el lado del cliente cuando la licencia se abre con el certificado DRM para el cliente y el error es inmediato. Estas restricciones también se pueden comprobar en el servidor antes de emitir la licencia. </p> </li> 
     </ul> </p> <p>El significado secundario de este error es que la licencia tiene la directiva "Aplicación del jailbreak" establecida y que se ha detectado un jailbreak en el dispositivo. Esta comprobación se realiza periódicamente en el lado del cliente y no se puede comprobar en el lado del servidor. </p> <p>Los distribuidores pueden actualizar las políticas y eliminar las restricciones. Para las directivas de capacidad del dispositivo, emita el comando de actualización de la directiva con la variable <span class="codeph"> -devCapabilitiesV1</span> indicador y sin argumentos. Para la aplicación de jailbreak, establezca <span class="codeph"> policy.forceJailbreak=false</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3348 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HardStopIntervalExpired </span> </td> 
   <td colname="col3"> Intervalo de detención grave caducado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3349 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooHigh </span> </td> 
   <td colname="col3"> El servidor se está ejecutando en una versión superior a la versión más alta admitida por el cliente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3350 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooLow </span> </td> 
   <td colname="col3"> El servidor se está ejecutando en una versión inferior a la versión mínima admitida por el cliente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3351 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenInvalid </span> </td> 
   <td colname="col3"> Token de dominio no válido. Para resolver este problema, regístrese de nuevo en el dominio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3352 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenToOld </span> </td> 
   <td colname="col3"> El token de dominio es anterior al token requerido por la licencia. Para resolver el problema, regístrese de nuevo en el dominio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3353 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenToNew </span> </td> 
   <td colname="col3"> El token de dominio es más reciente que el token requerido por la licencia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3354 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenExpired </span> </td> 
   <td colname="col3"> El token de dominio ha caducado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3355 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainJoinFailed </span> </td> 
   <td colname="col3"> Error de unión de dominio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3356 </td> 
   <td colname="col2"><span class="codeph"> AXS_NoCorrespondingRoot </span> </td> 
   <td colname="col3"> No se ha encontrado una licencia de raíz para una licencia de hoja V3. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3357 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoValidEmbeddedLicense </span> </td> 
   <td colname="col3"> No se ha encontrado ninguna licencia incrustada válida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3358 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoACPProtectionAvail </span> </td> 
   <td colname="col3"> No se puede reproducir porque el dispositivo analógico conectado no tiene protección ACP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3359 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCGMSAProtectionAvail </span> </td> 
   <td colname="col3"> No se puede reproducir porque el dispositivo analógico conectado no tiene protección CGMS-A. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3360 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainRegistrationRequired </span> </td> 
   <td colname="col3"> El contenido requiere el registro del dominio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3361 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NotRegisteredToDomain </span> </td> 
   <td colname="col3"> El equipo no está registrado en el dominio para los metadatos especificados. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3362 </td> 
   <td colname="col2"><span class="codeph"> AAXS_OperationTimeoutError </span> </td> 
   <td colname="col3"> La operación asincrónica tardó más de <span class="codeph"> maxOperationTimeout</span>. Solo lo devuelve iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3363 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnsupportedIOSPlaylistError </span> </td> 
   <td colname="col3"> La lista de reproducción de M3U8 pasada tenía contenido no compatible. Solo lo devuelve iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3364 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDeviceId </span> </td> 
   <td colname="col3"> <p>El marco de trabajo solicitó el ID del dispositivo, pero el valor devuelto estaba vacío. </p> <p>El usuario no debe seleccionar <span class="uicontrol"> Permitir identificadores para contenido protegido</span> en la configuración de Chrome. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3365 </td> 
   <td colname="col2"><span class="codeph"> AXS_IncognitoModeNotAllowed </span> </td> 
   <td colname="col3"> <p>Esta combinación de navegador y plataforma no permite la reproducción protegida mediante DRM en modo incógnito. </p> <p>El software del distribuidor debe aconsejar al usuario que salga del modo Incognito o utilice un navegador diferente. Para obtener más información, consulte <a href="https://forums.adobe.com/thread/1266622" format="https" scope="external"> Causa y resolución del error DRM 3365</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3366 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadParameter </span> </td> 
   <td colname="col3"> <p>El tiempo de ejecución del host llamó a la biblioteca de Access con un parámetro incorrecto. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3367 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadSignature </span> </td> 
   <td colname="col3"> Error de firma de manifiesto de m3u8. Solo lo devuelve iOS DRMNative Framework o AVE. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3368 </td> 
   <td colname="col2"><span class="codeph"> AXS_UserSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>El usuario ha cancelado la operación o ha introducido opciones que no permiten el acceso al sistema. </p> <p>Este error solo se produce cuando la versión del SWF es 19 o posterior. Para la compatibilidad con versiones anteriores, se produce 3321 cuando el SWF es de la versión 18 o anterior. </p> <p>El software del distribuidor debe guiar al usuario hasta una explicación de cómo permitir el acceso al complemento sin zona protegida. Acceso denegado a la zona protegida de Google Chrome</a> y <a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Error DRM 3322/3346/3368 en Chrome (problemas de la barra de información)</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3369 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InterfaceNotAvailable</span> </td> 
   <td colname="col3"> <p>No hay disponible una interfaz de explorador requerida. Este problema solo se produce en Pepper. Puede haber una discrepancia entre el complemento de Flash y la versión del explorador. </p> <p>El software del distribuidor debe guiar al usuario para asegurarse de que tiene instalada la última versión del navegador. </p> <p> Si las incidencias de este error aumentan y corresponde a una actualización del explorador que se está publicando, escale a Adobe. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3370 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentIdSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>El usuario ha desactivado la <span class="uicontrol"> Permitir identificadores para contenido protegido</span> configuración. </p> <p>Sugerencia: Este error apareció en las versiones 13.0.0.x o buenas de Pepper. </p> <p>El software del distribuidor debe guiar al usuario para habilitar la <span class="uicontrol"> Permitir identificadores para contenido protegido</span> configuración. </p> <p>El equipo de operaciones del distribuidor debe guiar al usuario para habilitar la <span class="uicontrol"> Permitir identificadores para contenido protegido</span> configuración. </p> <p>Para obtener más información, consulte <a href="https://forums.adobe.com/message/6518323#6518323" format="https" scope="external"> https://forums.adobe.com/message/6518323#6518323</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3371 </td> 
   <td colname="col2"><span class="codeph"> AXS_NoOPConstraintInPixel</span><span class="codeph"> Restricciones</span> </td> 
   <td colname="col3"> <p>Resolución mal formada basada en restricciones de protección de salida en la licencia. </p> <p>El software del distribuidor debe mostrar un mensaje de error. Pida al usuario que informe del problema al distribuidor con un título de contenido. </p> <p>El distribuidor debe volver a empaquetar el contenido con una política válida. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3372 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ResolutionLargerThanMaxResolution</span> </td> 
   <td colname="col3"> <p>La resolución del contenido es mayor que la resolución máxima especificada en la restricción de protección de salida. </p> <p>Si el equipo de operaciones del distribuidor ve este error en sus registros, debe revisar la política de protección de salida basada en la resolución y, si es necesario, volver a empaquetar el contenido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3373 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_DisplayResolutionLargerThanConstrain</span> </td> 
   <td colname="col3"> <p>La resolución del contenido es mayor que la resolución especificada por la restricción de protección de salida activa actualmente. </p> <p>Si el equipo de operaciones del distribuidor ve este error en sus registros, debe revisar la política de protección de salida basada en la resolución y, si es necesario, volver a empaquetar el contenido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3374 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_ClientCommProcessFailed</span> </td> 
   <td colname="col3"> <p>Error durante el procesamiento de comunicaciones del lado del cliente, por ejemplo, generación de solicitudes, procesamiento de respuestas, token de autenticación incorrecto, etc. </p> <p>Si el equipo de operaciones del distribuidor ve este error en sus registros, debe revisar la política de protección de salida basada en la resolución y, si es necesario, volver a empaquetar el contenido. </p> </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Valores de reproducción de vídeo {#section_7079501250C2487499639F92EC774525}

La interfaz Video Encoder del AVE devuelve estas notificaciones de reproducción de vídeo en el `NATIVE_ERROR` objeto de metadatos.

<table id="table_5EEB1F60E5854452A8B0BABBE9B32651"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Valor de la clave de metadatos NATIVE_ERROR_CODE </th> 
   <th colname="col2" class="entry"> Valor de la clave de metadatos NATIVE_ERROR_NAME </th> 
   <th colname="col3" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> END_OF_PERIOD</span> </td> 
   <td colname="col3"> Fin de período. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> SUCCESS</span> </td> 
   <td colname="col3"> Operación correcta. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> Operación asincrónica. Se ha realizado la solicitud de operación. La información sobre éxito o error estará disponible más adelante. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> Operación no posible debido a la condición de fin de archivo (EOF). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> DECODER_FAILED</span> </td> 
   <td colname="col3"> Error del decodificador durante la ejecución. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> No se pudo abrir el descodificador de hardware. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> FILE_NOT_FOUND </span> </td> 
   <td colname="col3"> No se encuentra el recurso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> GENERIC_ERROR </span> </td> 
   <td colname="col3"> Error genérico. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> IRRECUPERABLE_ERROR </span> </td> 
   <td colname="col3"> Condición de error desde la que el motor de vídeo no se puede recuperar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERABLE </span> </td> 
   <td colname="col3"> Error de red al intentar recuperarse. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE </span> </td> 
   <td colname="col3"> No se puede determinar el tamaño del recurso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> NOT_IMPLEMENTED </span> </td> 
   <td colname="col3"> Función no implementada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> MEMORIA_INSUFICIENTE </span> </td> 
   <td colname="col3"> Memoria insuficiente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR </span> </td> 
   <td colname="col3"> Error al analizar el archivo multimedia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> SIZE_UNKNOWN </span> </td> 
   <td colname="col3"> El recurso tiene un tamaño, pero se desconoce. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> UNDER_FLOW </span> </td> 
   <td colname="col3"> Condición de desbordamiento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_CONFIG </span> </td> 
   <td colname="col3"> No se admite la configuración. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_OPERATION </span> </td> 
   <td colname="col3"> No se admite la operación. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT </span> </td> 
   <td colname="col3"> Aún no se ha inicializado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER </span> </td> 
   <td colname="col3"> Parámetro no válido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19 </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> Operación no permitida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20 </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> La operación solo se permite mientras está en pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> El funcionamiento no se puede utilizar en ficheros de sólo audio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> La operación de búsqueda anterior aún está en curso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> ORIGEN_NO_ESPECIFICADO </span> </td> 
   <td colname="col3"> Recurso no especificado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> RANGE_ERROR</span> </td> 
   <td colname="col3"> El valor especificado está fuera del intervalo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> INVALID_SEEK_TIME</span> </td> 
   <td colname="col3"> Hora de búsqueda no válida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> El archivo especificado no se ajusta a la sintaxis esperada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAILURE</span> </td> 
   <td colname="col3"> No se ha podido crear un componente esencial. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> Error al crear el contexto DRM. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> El tipo de contenedor no es compatible. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> SEEK_FAILED</span> </td> 
   <td colname="col3"> Error de búsqueda. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Códec no compatible. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_UNAVAILABLE</span> </td> 
   <td colname="col3"> La red no está disponible. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_ERROR</span> </td> 
   <td colname="col3"> Error al obtener datos de la red. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> DESBORDAMIENTO</span> </td> 
   <td colname="col3"> Desbordamiento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Perfil de vídeo no compatible. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> Se ha intentado una operación en un periodo HOLD o en un periodo que aún no se ha cargado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> La duración de reemplazo especificada no es válida o se extiende más allá del final del flujo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> LLAMADO_DESDE_SUBPROCESO_INCORRECTO</span> </td> 
   <td colname="col3"> No se puede llamar a la API desde el subproceso incorrecto. Principalmente, para elementos de API a los que solo se debe llamar desde el subproceso Principal. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> Error de lectura de fragmento. No hay failover. El motor intentará leer el siguiente fragmento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> ANULADO</span> </td> 
   <td colname="col3"> La operación se anuló mediante una llamada explícita a Abort o Destroy. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> No se puede reproducir esta versión de medios HLS. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> No se puede conmutar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> La descarga HTTP ha expirado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_DOWN </span> </td> 
   <td colname="col3"> La conexión de red del usuario está inactiva. La reproducción puede detenerse en cualquier momento y se reanudará cuando la conexión esté disponible. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> No se ha encontrado ningún perfil de velocidad de bits utilizable en el flujo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> El manifiesto tiene una firma incorrecta. No pasó la prueba de firma de manifiesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> No se puede cargar una lista de reproducción. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> El reemplazo especificado en una API de inserción no se pudo realizar correctamente. Esto significa que la inserción se realizó correctamente pero el reemplazo no. La sustitución podría fallar si el manifiesto que se va a reemplazar se ha eliminado de la cronología. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ASYMETRIC_PROFILE</span> </td> 
   <td colname="col3"> DRM está cambiando a un perfil asimétrico. Se espera que todos los perfiles se alineen en la duración. Si no es así, se generará esta advertencia y es posible que se produzcan saltos en la reproducción. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> Se espera que la ventana activa solo avance. Si no es así, se generará esta advertencia y no se leerá la ventana. Debido a esto, puede haber saltos (o detención/pausa prolongada) en la reproducción. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> La ventana activa se ha movido más allá del periodo actual. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> La longitud del contenido informada por el servidor HTTP no coincide con el tamaño real del medio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> El lector de medios no puede leer más porque ha alcanzado el tiempo establecido por la API setHoldAt. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD </span> </td> 
   <td colname="col3">El lector de medios no puede cargar segmentos porque ha llegado al final de la ventana en directo. La carga de segmentos se reanudará cuando el servidor añada nuevos medios a la ventana en directo. Este estado se suele alcanzar si: 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">El <span class="codeph"> bufferTime</span> es demasiado alto (igual o superior a la duración de la ventana activa). </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">Una combinación de uno o más de API de inserción/eliminación reemplazó más medios de los que agregó. </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">El siguiente periodo es un periodo activo con un reemplazo de medios pendiente (debido a una llamada de API InsertBy) </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEAVING </span> </td> 
   <td colname="col3"> La intercalación de audio y vídeo en los medios no se realiza correctamente. Esto es un error de empaquetado. La advertencia se envía cuando la diferencia supera los dos segundos. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> No se ha habilitado la reproducción de HLS en el Flash Player. Consulte AuthorizedFeatures.enableHLSPlayback. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> El descodificador recibió una muestra incorrecta que no se puede descodificar. Este no suele ser un error grave, pero indica que puede haber fallos en el audio o el vídeo. Demasiadas instancias de este error indican una codificación incorrecta o un archivo incorrecto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> Una vez iniciada la reproducción, la gama Insert/Replace no debe contener el cabezal de lectura. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> No se permiten las inserciones posteriores a la emisión en medios en directo. Sin embargo, se permiten después de que el servidor marque los medios como completos. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> INTERNAL_ERROR</span> </td> 
   <td colname="col3"> Un asunto muy raro que nunca debería suceder. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> El flujo no sigue la recomendación de empaquetado de colocar siempre H264 SPS/PPS en un AVCC. Pueden verse problemas de búsqueda/reproducción. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> PARTIAL_REPLACEMENT</span> </td> 
   <td colname="col3"> El reemplazo especificado en una API de inserción solo se realizó parcialmente. Esto sucede cuando replaceDuration se extiende sobre la duración de la escala de tiempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> Error al cargar la lista de reproducción de la representación. Esto es solo para AVE, no para FlashPlayer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> La operación no hace nada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKIPPED_ON_FAILURE</span> </td> 
   <td colname="col3"> El segmento no se puede reproducir y se omitirá si se produce un error. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> INCOMPATIBLE_RENDER_MODE</span> </td> 
   <td colname="col3"> Modo de procesamiento no compatible. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOLO_NO_ADMITIDO </span> </td> 
   <td colname="col3"> No se admite el protocolo web utilizado en la dirección URL. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPATIBLE_VERSION</span> </td> 
   <td colname="col3"> Error al analizar el archivo multimedia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UNEXPECTEDLY_CHANGED</span> </td> 
   <td colname="col3"> El archivo de manifiesto se ha cambiado de forma inesperada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> No se puede realizar una operación de división en una cronología. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> No se puede realizar una operación de borrado en una cronología. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> No se obtuvo el siguiente fragmento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> No hay ninguna cronología en una estructura de datos interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> No se ha encontrado ningún oyente en una estructura de datos interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> No se puede iniciar el audio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> No hay ningún receptor de audio en una estructura de datos interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> No se puede abrir el archivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> No se puede escribir en un archivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> No se puede leer de un archivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> Se ha producido un error al analizar los datos de ID3. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> SECURITY_ERROR </span> </td> 
   <td colname="col3"> Error al cargar el contenido debido a restricciones de seguridad. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> CRONOLOGÍA_DEMASIADO_CORTA</span> </td> 
   <td colname="col3"> La duración de la cronología es demasiado corta. Si se trata de una emisión en directo, puede producirse un almacenamiento en búfer frecuente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> El flujo se ha cambiado a un flujo de solo audio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> El flujo ha cambiado de solo audio a un flujo con vídeo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> KEY_NOT_FOUND </span> </td> 
   <td colname="col3"> No se encuentra la clave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> INVALID_KEY</span> </td> 
   <td colname="col3"> La clave no es válida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> El servidor de claves no devuelve una clave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> No se puede administrar la actualización del manifiesto principal. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> UNREPORTED_TIME_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Discontinuidad de tiempo no notificado (PTS) encontrada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> UNATCHED_AV_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Se encontró una discontinuidad de audio y vídeo sin coincidencias. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3">Se ha producido un error al reproducir el contenido en <i>juego de trucos</i> modo. El modo de reproducción engañosa finaliza y el flujo se detiene. Llamada <span class="codeph"> Play()</span> para reproducir el contenido en modo normal. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_AHEAD</span> </td> 
   <td colname="col3"> El jugador está fuera de la ventana en vivo y debe buscar hacia adelante para ponerse al día. </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Valores criptográficos {#section_39365E545CAC49B9A4D4678657BB2155}

El módulo criptográfico del motor de vídeo de Adobe devuelve estas notificaciones en el `NATIVE_ERROR` objeto de metadatos.

| Valor de la clave de metadatos NATIVE_ERROR_CODE | Valor de la clave de metadatos NATIVE_ERROR_NAME | Significado |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | El algoritmo que se está utilizando no es compatible. |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | Los datos están dañados. |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | Búfer demasiado pequeño. |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | Certificado incorrecto. |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | Actualización del resumen. |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | Fin de resumen. |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | Parámetro incorrecto. |
