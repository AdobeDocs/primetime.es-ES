---
title: Referencia de propiedades del servidor
description: Referencia de propiedades del servidor
copied-description: true
exl-id: 8724d097-7cba-4ca9-b597-df56f80b2e9c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# Referencia de propiedades del servidor{#server-properties-reference}

<!--<a id="section_EC8810492A454BDBA6013FE376360F4E"></a>-->

## Servidor de individualización

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
   <td>La credencial de transporte se utiliza para descifrar solicitudes recibidas del cliente y firmar las respuestas enviadas. Asegúrese de configurar la variable <span class="filepath"> AdobeInitial.properties</span> archivo correctamente tanto con la ruta de acceso al archivo de credenciales de transporte como con la contraseña PKCS12 cifrada. </td> 
   <td> 
    <ul id="ul_itx_fl2_jr"> 
     <li id="li_A2E65253F37245268A41E6B9C958C8DF"><span class="codeph"> cert.i15n.transport.file = </span> [archivo PKCS12 que contiene el certificado y la clave de transporte de individualización] </li> 
     <li id="li_28CDFC0B3D684795AF4708B6D26DF83F"><span class="codeph"> cert.i15n.transport.password =</span> [Contraseña cifrada para archivo PKCS12] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Credencial de CA de individualización </td> 
   <td>El servidor de individualización utiliza la credencial de CA de individualización para firmar los certificados de equipo que emite. Asegúrese de configurar la variable <span class="filepath"> AdobeInitial.properties</span> archivo correctamente tanto con la ruta al archivo de credenciales de CA I15N como con la contraseña PKCS12 cifrada. </td> 
   <td> 
    <ul id="ul_xsj_nl2_jr"> 
     <li id="li_5A770D8A482F41A4A9AB63CA52C2EB90"><span class="codeph"> cert.i15n.ica.file =</span> [archivo PKCS12 que contiene el certificado de CA de individualización y la clave] </li> 
     <li id="li_C3C4A2D9AA2A4F86B6DDCFFD9CB55CBB"><span class="codeph"> cert.i15n.ica.password =</span> [Contraseña cifrada para archivo PKCS12] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Credencial de cifrado de individualización </td> 
   <td> El servidor de individualización utiliza la credencial de cifrado para cifrar archivos confidenciales que deben transmitirse a los servidores de individualización. Por ejemplo, este certificado admite la migración de licencias y también se utiliza para cifrar las claves privadas DRM para los servidores de individualización. </td> 
   <td> 
    <ul id="ul_nbr_kpd_w5"> 
     <li id="li_4226AD6CC85740669DAF467EFD00BBBE"><span class="codeph"> cert.i15n.decryption.file=i15n_transport.pfx</span> </li> 
     <li id="li_F51BDD94F4724FA58CEF9470B6FEE33B"><span class="codeph"> cert.i15n.decryption.password=password</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Caché de contenido </td> 
   <td>Esta configuración controla la ubicación desde la que el servidor de individualización descarga contenido y donde el contenido se almacena en caché en el disco. El servidor de individualización comprobará si hay contenido nuevo en el servidor de contenido una vez al inicio y, a continuación, a la frecuencia/hora especificada por estas propiedades. <p>Para el servidor de individualización local, se ha incluido un conjunto inicial de datos de caché de contenido. Asegúrese de copiar el <i>CONTENIDO</i> de la carpeta de caché (no la carpeta de caché en sí) al configurado <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> contentServer.localDirectory</span> ubicación. </p> </td> 
   <td> 
    <ul id="ul_r4n_1r2_jr"> 
     <li id="li_CA5F562577B04B4A9966EF46E039A137"><span class="codeph"> contentServer.localDirectory =</span> [Directorio en el que se almacena el contenido local (normalmente tomcat/temp)] </li> 
     <li id="li_9A78FBD6C54D47708226378340B46E8E"><span class="codeph"> contentServer.server =</span> [Servidor web con el que ponerse en contacto para obtener información de ECI (<i>no compatible con esta versión</i>)] </li> 
     <li id="li_4E7D7F76085D411688B5003E855F860B"><span class="codeph"> contentServer.timeout =</span> [Tiempo de espera de conexión, en segundos] </li> 
     <li id="li_4B751F238A1643A7AC730CD9354887B6"><span class="codeph"> contentServer.pollFrequency =</span> [Frecuencia con la que se sondea el servidor, en días (el mínimo es 1 día)] </li> 
     <li id="li_8E23C3C6E7EF46B0AFDD7993DE79F142"><span class="codeph"> contentServer.pollTime =</span> [Hora del día para sondear el servidor, en minutos desde la medianoche] </li> 
    </ul> <p>Asegúrese de leer la sección <i>Archivos de CRL y ECI</i> acerca de mantener la caché actualizada. </p> </td> 
  </tr> 
  <tr> 
   <td> CRL de CA de individualización </td> 
   <td> <p>Este punto de distribución de lista de revocación de certificados (CRL) se incluye en cada certificado de equipo emitido por el servidor de individualización. Durante la validación del certificado del equipo en el servidor de licencias, la CRL se descargará desde el punto de distribución indicado en el certificado (o se leerá desde la caché si ya se ha descargado) y se comprobará que el certificado no se haya revocado. Se recomienda realizar este cambio de configuración del servidor después de pasar por el proceso de creación e implementación de la CRL de CA de individualización. Reinicie el servidor de individualización después de cualquier cambio de configuración. </p> <p>Para establecer la dirección URL del punto de distribución CRL, deberá establecer la dirección URL <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> cert.machine.crldp</span> field. </p> </td> 
   <td> 
    <ul id="ul_eq3_lv2_jr"> 
     <li id="li_5E37A9E318D742B6A5E1035120888819"><span class="codeph"> cert.machine.crldp =</span> [punto de distribución CRL] </li> 
    </ul> <p>Por ejemplo: </p>
    <p> <code>
      cert.machine.crldp__DEV=<span>tps://onprem-individualization.com</span>CRL/onprem-individualization-ca.crl
     </code></p>
     <p>El servidor de licencias debe descargar automáticamente esta CRL, una vez que se gestione una solicitud de licencia. </p> <p importance="high">Nota: Este punto de distribución es <i>no</i> comprobado por DRM de Primetime para la validez. Debe comprobar que esta dirección URL es válida. Los errores resultantes de una URL no válida no aparecerán hasta que aparezcan errores de validación desde el servidor de licencias. </p> </td> 
  </tr> 
  <tr> 
   <td> Registro </td> 
   <td>Configure las variables <span class="filepath"> AdobeInitial.properties</span> para iniciar sesión según sea necesario. </td> 
   <td> 
    <ul id="ul_j1v_kw2_jr"> 
     <li id="li_B60002B33A3042FCBE1F694454966469"><span class="codeph"> adobe.weblogs.loc =</span> [Directorio donde se crearán los archivos de registro] </li> 
     <li id="li_2DD4406FBBF047589BAAAE1C9082D8B3"><span class="codeph"> log.Level =</span> [El nivel más bajo de mensajes de registro que pueden aparecer en los registros <span class="codeph"> [DEBUG | INFORMACIÓN]</span> ] </li> 
     <li id="li_610FAF239A554CE59DAC455174F0CF0A"><span class="codeph"> log.FileName =</span> [Prefijo para archivos de registro. Fecha/hora y ".log" se añadirán al nombre del archivo] </li> 
     <li id="li_1F2913B209BE4A0E8207FAAD052D1764"><span class="codeph"> log.RollInterval =</span> [Especifica la frecuencia con la que se acumulan los registros.] </li> 
     <li id="li_3F46C15488114BB5B41035F710E7A19F"><span class="codeph"> log.RollSize =</span> [Desplace los registros cuando alcancen este tamaño (los registros se moverán cuando <span class="codeph"> RollInterval</span> o <span class="codeph"> RollSize</span> se alcanza, lo que suceda primero)] </li> 
     <li id="li_DA32E862F7B0413885DA20633B682484"><span class="codeph"> log.ReportLogging.Enabled =</span>[ [true] | false ] Especifica si se debe generar un archivo independiente que contenga datos utilizados por Adobe para generar informes de individualización.] </li> 
     <li id="li_465CC6D81B8A484CBF4E7A39F7AF86AA"><span class="codeph"> log.ReportLogging.FileName =</span> [Prefijo para archivos de registro de informes. Fecha/hora y <span class="filepath"> .log</span> Se agregará la extensión al nombre del archivo. La l<span class="codeph"> og.Level</span> La propiedad no se aplica a este archivo de registro, pero <span class="codeph"> log.RollInterval</span> y <span class="codeph"> log.RollSize</span> do.] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Otros </td> 
   <td></td> 
   <td> 
    <ul id="ul_b3b_g1f_jr"> 
     <li id="li_FACF07CB332D416E91FD34DE48152FAA"><span class="codeph"> deviceinfo.key =</span> [Clave codificada Base64 cifrada utilizada para codificar la información del dispositivo HMAC antes de incluirla en el token de la máquina. La clave puede ser diferente para los entornos de desarrollo, ensayo y producción, pero debe ser la misma para todos los servidores de un entorno concreto. ] </li> 
     <li id="li_B19C77FD6F91496294DBF836A1922EE1"><span class="codeph"> keys.kgs.server =</span> [Ubicación del servidor de generación de claves (un solo host/puerto, que representa un grupo de servidores de claves) ] </li> 
     <li id="li_5DA3C89770804B148EF6FAF01A5AD958"><span class="codeph"> keys.MinQueueSize =</span> [Recupere otro lote de claves del KGS cuando queden tantas claves en la cola] </li> 
     <li id="li_0C2E5F2FDB824182A6BE418B041D2F28"><span class="codeph"> status.Timeout =</span> [La página de estado hará ping al KGS para determinar si puede llegar al servidor. Se agotará el tiempo de espera si una respuesta no se recibe en el período de tiempo especificado.] </li> 
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
     <li id="li_E4347D572F004BF0B237A662BFE7F3ED"><span class="codeph"> kgs.Threads =</span> [Número de subprocesos que se van a utilizar para generar claves (debe ser igual al número de procesadores disponibles en el equipo)] </li> 
     <li id="li_EDBC2535D48E4A66AEB240DB337187FC"><span class="codeph"> kgs.BatchSize =</span> [Número de claves que se van a generar por lote] </li> 
     <li id="li_07B41546D94F42349103BF8AF4605E14"><span class="codeph"> kgs.KeyDirectory =</span> [Directorio en el que se almacenan los archivos por lotes de claves] </li> 
     <li id="li_F4962C97DC3D491DA7FAC826E38A4459"><span class="codeph"> kgs.MaxQueueSize =</span> [Número máximo de archivos por lotes de claves que se generarán] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Registro </td> 
   <td></td> 
   <td> 
    <ul id="ul_kwq_12f_jr"> 
     <li id="li_5E5D34FE5EB44BB898090494C7DDEBD8"><span class="codeph"> adobe.weblogs.loc =</span> [Directorio donde se crearán los archivos de registro] </li> 
     <li id="li_0E34CD32CD5E47729B69B50414F93678"><span class="codeph"> log.FileName =</span> [Prefijo para archivos de registro. Fecha/hora y <span class="filepath"> .log</span> se agregará la extensión al nombre del archivo] </li> 
     <li id="li_8AB15ACEC39041A2A04C7301154C6EDB"><span class="codeph"> log.Level =</span> [El nivel más bajo de mensajes de registro que pueden aparecer en los registros] </li> 
     <li id="li_A17E84DA3ED243F381FF3A6184A3CAA0"><span class="codeph"> log.RollInterval =</span> [Especifica la frecuencia con la que se acumulan los registros.] </li> 
     <li id="li_C2B3D111608945DA9D1428BE98D61664"><span class="codeph"> log.RollSize =</span> [Desplace los registros cuando alcancen este tamaño (los registros se moverán cuando <span class="codeph"> RollInterval</span> o <span class="codeph"> RollSize</span> se alcanza, lo que suceda primero)] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
