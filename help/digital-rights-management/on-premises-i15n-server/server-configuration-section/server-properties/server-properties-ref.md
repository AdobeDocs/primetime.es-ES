---
title: Referencia de propiedades del servidor
description: Referencia de propiedades del servidor
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---


# Referencia de propiedades del servidor{#server-properties-reference}

<!--<a id="section_EC8810492A454BDBA6013FE376360F4E"></a>-->

## Servidor de personalización

<table id="table_ats_tk2_jr">  
 <thead> 
  <tr> 
   <th class="entry"> Configuración </th> 
   <th class="entry"> Descripción </th> 
   <th class="entry"> Ejemplo </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Credencial de transporte </td> 
   <td>La credencial de transporte se utiliza para descifrar solicitudes recibidas del cliente y firmar las respuestas enviadas. Asegúrese de configurar el archivo <span class="filepath"> AdobeInitial.properties</span> apropiadamente con la ruta al archivo de credenciales de transporte, así como la contraseña PKCS12 cifrada. </td> 
   <td> 
    <ul id="ul_itx_fl2_jr"> 
     <li id="li_A2E65253F37245268A41E6B9C958C8DF"><span class="codeph"> cert.i15n.transport.file =  </span> [Archivo PKCS12 que contiene el certificado de transporte de individualización y la clave] </li> 
     <li id="li_28CDFC0B3D684795AF4708B6D26DF83F"><span class="codeph"> cert.i15n.transport.password =</span> [Contraseña cifrada para el archivo PKCS12] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Credencial de CA de Individualización </td> 
   <td>El servidor de Individualización utiliza la credencial de CA de Individualización para firmar los certificados de equipo que emite. Asegúrese de configurar el archivo <span class="filepath"> AdobeInitial.properties</span> apropiadamente con la ruta al archivo de credenciales de CA I15N, así como la contraseña PKCS12 cifrada. </td> 
   <td> 
    <ul id="ul_xsj_nl2_jr"> 
     <li id="li_5A770D8A482F41A4A9AB63CA52C2EB90"><span class="codeph"> cert.i15n.ica.file =</span> [Archivo PKCS12 que contiene el certificado y la clave de CA de Individualización] </li> 
     <li id="li_C3C4A2D9AA2A4F86B6DDCFFD9CB55CBB"><span class="codeph"> cert.i15n.ica.password =</span> [Contraseña cifrada para el archivo PKCS12] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Credencial de codificación de la persona </td> 
   <td> El servidor de Individualización utiliza la credencial de Cifrado para cifrar archivos confidenciales que deben transmitirse a los servidores de Individualización. Por ejemplo, este certificado admite la migración de licencias y también se utiliza para cifrar las claves privadas DRM para los servidores de Individualización. </td> 
   <td> 
    <ul id="ul_nbr_kpd_w5"> 
     <li id="li_4226AD6CC85740669DAF467EFD00BBBE"><span class="codeph"> cert.i15n.decryption.file=i15n_transport.pfx</span> </li> 
     <li id="li_F51BDD94F4724FA58CEF9470B6FEE33B"><span class="codeph"> cert.i15n.decryption.password=password</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Caché de contenido </td> 
   <td>Estos ajustes controlan la ubicación desde la que el servidor de Individualización descarga contenido y donde el contenido se almacena en caché en el disco. El servidor de Individualización comprobará si hay contenido nuevo en el servidor de contenido una vez al inicio y, a continuación, en la frecuencia y hora especificadas por estas propiedades. <p>Para el servidor de individualización On Premies, hemos incluido un conjunto inicial de datos de caché de contenido. Asegúrese de copiar el <i>CONTENTS</i> de la carpeta de caché (no la propia carpeta de caché) en la ubicación <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> contentServer.localDirectory</span> configurada. </p> </td> 
   <td> 
    <ul id="ul_r4n_1r2_jr"> 
     <li id="li_CA5F562577B04B4A9966EF46E039A137"><span class="codeph"> contentServer.localDirectory =</span> [Directorio en el que almacenar contenido local (normalmente tomcat/temp)] </li> 
     <li id="li_9A78FBD6C54D47708226378340B46E8E"><span class="codeph"> contentServer.server =</span> [Servidor web en contacto para obtener información de ECI (<i>no admitido en esta versión</i>)] </li> 
     <li id="li_4E7D7F76085D411688B5003E855F860B"><span class="codeph"> contentServer.timeout =</span> [Tiempo de espera de conexión, en segundos] </li> 
     <li id="li_4B751F238A1643A7AC730CD9354887B6"><span class="codeph"> contentServer.pollFrequency =</span> [Con qué frecuencia sondear el servidor, en días (el mínimo es 1 día)] </li> 
     <li id="li_8E23C3C6E7EF46B0AFDD7993DE79F142"><span class="codeph"> contentServer.pollTime =</span> [Hora del día para sondear el servidor, en minutos desde medianoche] </li> 
    </ul> <p>Asegúrese de leer la sección <i>CRL y archivos ECI</i> sobre cómo mantener la caché actualizada. </p> </td> 
  </tr> 
  <tr> 
   <td> Clasificación CRL de CA por separado </td> 
   <td> <p>Este punto de distribución Lista de revocación de certificados (CRL) se incluye en cada certificado de equipo emitido por el servidor de individualización. Durante la validación del certificado del equipo en el servidor de licencias, la CRL se descargará desde el punto de distribución indicado en el certificado (o se leerá desde la caché si ya se ha descargado) y se comprobará para asegurarse de que el certificado no se haya revocado. Se recomienda realizar este cambio en la configuración del servidor después de pasar por el proceso de creación e implementación de la CRL de CA de Individualización. Reinicie el servidor de Individualización después de cualquier cambio de configuración. </p> <p>Para establecer la URL del punto de distribución CRL, deberá establecer el campo <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> cert.machine.crldp</span>. </p> </td> 
   <td> 
    <ul id="ul_eq3_lv2_jr"> 
     <li id="li_5E37A9E318D742B6A5E1035120888819"><span class="codeph"> cert.machine.crldp =</span> [punto de distribución CRL] </li> 
    </ul> <p>Por ejemplo: </p>
    <p> <code>
      cert.machine.crldp__DEV=<span>tps://onprem-individualization.com</span>CRL/onprem-individualization-ca.crl
     </code></p>
     <p>El servidor de licencias debe descargar automáticamente esta CRL, una vez que se gestiona una solicitud de licencia. </p> <p importance="high">Nota: Este punto de distribución es <i>not</i> verificado por Primetime DRM para su validez. Debe verificar que esta dirección URL sea válida. Los errores resultantes de una dirección URL no válida no aparecerán hasta que aparezcan los errores de validación del servidor de licencias. </p> </td> 
  </tr> 
  <tr> 
   <td> Registro </td> 
   <td>Configure el <span class="filepath"> AdobeInitial.properties</span> para iniciar sesión según sea necesario. </td> 
   <td> 
    <ul id="ul_j1v_kw2_jr"> 
     <li id="li_B60002B33A3042FCBE1F694454966469"><span class="codeph"> adobe.weblogs.loc =</span> [Directorio donde se crearán los archivos de registro] </li> 
     <li id="li_2DD4406FBBF047589BAAAE1C9082D8B3"><span class="codeph"> log.Level =</span> [El nivel más bajo de mensajes de registro que puede aparecer en los registros  <span class="codeph"> [DEBUG | INFO]</span> ] </li> 
     <li id="li_610FAF239A554CE59DAC455174F0CF0A"><span class="codeph"> log.FileName =</span> [Prefijo para archivos de registro. Fecha/hora y la extensión ".log" se agregarán al nombre del archivo] </li> 
     <li id="li_1F2913B209BE4A0E8207FAAD052D1764"><span class="codeph"> log.RollInterval =</span> [Especifica con qué frecuencia se rompen los registros.] </li> 
     <li id="li_3F46C15488114BB5B41035F710E7A19F"><span class="codeph"> log.RollSize =</span> [Roll the logs cuando alcancen este tamaño (Los registros se rompen cuando se alcance el  <span class="codeph"> </span> RollIntervalor  <span class="codeph"> </span> RollSize, lo que suceda primero)] </li> 
     <li id="li_DA32E862F7B0413885DA20633B682484"><span class="codeph"> log.ReportLogging.Enabled =</span>[ [true | false ] Especifica si se debe generar un archivo independiente que contenga datos utilizados por el Adobe para generar informes de Individualización.] </li> 
     <li id="li_465CC6D81B8A484CBF4E7A39F7AF86AA"><span class="codeph"> log.ReportLogging.FileName =</span> [Prefijo para los archivos de registro de informes. Se agregarán la extensión de fecha/hora y <span class="filepath"> .log</span> al nombre del archivo. La propiedad l<span class="codeph"> og.Level</span> no se aplica a este archivo de registro, pero <span class="codeph"> log.RollInterval</span> y <span class="codeph"> log.RollSize</span> sí.] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Otro </td> 
   <td></td> 
   <td> 
    <ul id="ul_b3b_g1f_jr"> 
     <li id="li_FACF07CB332D416E91FD34DE48152FAA"><span class="codeph"> deviceinfo.key =</span> [Clave codificada Base64 utilizada para la información del dispositivo HMAC antes de incluirla en el token del equipo. La clave puede ser diferente para los entornos de desarrollo/ensayo/producción, pero debe ser la misma para todos los servidores de un entorno en particular. ] </li> 
     <li id="li_B19C77FD6F91496294DBF836A1922EE1"><span class="codeph"> keys.kgs.server =</span> [Ubicación del servidor de generación de claves (un solo host/puerto que representa un grupo de servidores clave)] </li> 
     <li id="li_5DA3C89770804B148EF6FAF01A5AD958"><span class="codeph"> keys.MinQueueSize =</span> [Recupere otro lote de claves de KGS cuando queden tantas claves en la cola] </li> 
     <li id="li_0C2E5F2FDB824182A6BE418B041D2F28"><span class="codeph"> status.Timeout =</span> [La página de estado hará ping en el KGS para determinar si puede llegar al servidor. Se agotará el tiempo de espera si no se devuelve una respuesta en el tiempo especificado.] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Servidor de generación de claves {#section_37FA8EEBA258461F8CFA3ADF37714577}

<table id="table_ats_tk2_js"> 
 <thead> 
  <tr> 
   <th class="entry"> Configuración </th> 
   <th class="entry"> Descripción </th> 
   <th class="entry"> Ejemplo </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Generación de claves </td> 
   <td></td> 
   <td> 
    <ul id="ul_nlj_ydf_jr"> 
     <li id="li_E4347D572F004BF0B237A662BFE7F3ED"><span class="codeph"> kgs.Threads =</span> [Número de subprocesos que se utilizarán para generar claves (debe ser igual al número de procesadores disponibles en el equipo)] </li> 
     <li id="li_EDBC2535D48E4A66AEB240DB337187FC"><span class="codeph"> kgs.BatchSize =</span> [Número de claves que se van a generar por lote] </li> 
     <li id="li_07B41546D94F42349103BF8AF4605E14"><span class="codeph"> kgs.KeyDirectory =</span> [Directorio en el que almacenar archivos por lotes de claves] </li> 
     <li id="li_F4962C97DC3D491DA7FAC826E38A4459"><span class="codeph"> kgs.MaxQueueSize =</span> [Número máximo de archivos por lotes clave que se van a generar] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Registro </td> 
   <td></td> 
   <td> 
    <ul id="ul_kwq_12f_jr"> 
     <li id="li_5E5D34FE5EB44BB898090494C7DDEBD8"><span class="codeph"> adobe.weblogs.loc =</span> [Directorio donde se crearán los archivos de registro] </li> 
     <li id="li_0E34CD32CD5E47729B69B50414F93678"><span class="codeph"> log.FileName =</span> [Prefijo para archivos de registro. Se agregarán la fecha/hora y la extensión <span class="filepath"> .log</span> al nombre del archivo] </li> 
     <li id="li_8AB15ACEC39041A2A04C7301154C6EDB"><span class="codeph"> log.Level =</span> [El nivel más bajo de mensajes de registro que puede aparecer en los registros] </li> 
     <li id="li_A17E84DA3ED243F381FF3A6184A3CAA0"><span class="codeph"> log.RollInterval =</span> [Especifica con qué frecuencia se rompen los registros.] </li> 
     <li id="li_C2B3D111608945DA9D1428BE98D61664"><span class="codeph"> log.RollSize =</span> [Roll the logs cuando alcancen este tamaño (Los registros se rompen cuando se alcance el  <span class="codeph"> </span> RollIntervalor  <span class="codeph"> </span> RollSize, lo que suceda primero)] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
