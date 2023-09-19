---
title: Propiedades del archivo de configuración
description: Propiedades del archivo de configuración
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Propiedades del archivo de configuración {#configuration-file-properties}

Antes de ejecutar el empaquetador de medios, especifique los valores de las propiedades del empaquetador de medios. El archivo de configuración especifica las siguientes propiedades. Para nombres de propiedades que incluyen* n*, *n* representa un entero que comienza por 1 y aumenta para cada instancia de la propiedad.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Propiedad </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.video</span> </td> 
   <td colname="2" class="- topic/entry "> Indica si se debe cifrar el contenido de vídeo. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.audio</span> </td> 
   <td colname="2" class="- topic/entry "> Indica si se debe cifrar el audio. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.script</span> </td> 
   <td colname="2" class="- topic/entry ">Indica si se deben cifrar los datos de script en los FLV. <i class="+ topic/ph hi-d/i ">onMetaData</i> y <i class="+ topic/ph hi-d/i ">onXMP</i> las etiquetas de datos de scripts nunca se cifran, aunque esta opción esté habilitada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica el nivel de cifrado de vídeo. Un valor alto se utiliza para cifrar todo el contenido de vídeo, mientras que los valores medio y bajo se utilizan para cifrar partes del contenido de vídeo para archivos F4V que contienen contenido H.264. </p> <p class="- topic/p ">value = <span class="codeph"> alto | medio | bajo</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.secondsUnencryption</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si el valor es mayor que 0, no se cifrará el número especificado de segundos de contenido al principio del archivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Archivo de certificado del servidor de licencias utilizado para cifrar la clave. El <span class="codeph"> encrypt.keys.asymmetric.certfile</span> especifica un archivo que contiene solo el certificado (se acepta el formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esta propiedad se utiliza repetidamente para crear una lista de directivas que se aplicarán al contenido. <span class="codeph"> n</span> es un entero cuyo valor es 1 o mayor. El cliente utilizará la primera instancia de forma predeterminada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL del servidor de licencias. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Certificado de transporte para el servidor de licencias. Esta propiedad especifica un <span class="filepath"> .cer</span> que solo contiene el certificado (se acepta el formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El archivo PKCS12 que contiene las credenciales del empaquetador para firmar contenido. El <span class="codeph"> encrypt.sign.certfile</span> debe hacer referencia a un <span class="filepath"> .pfx</span> archivo que contiene un certificado y una clave privada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La contraseña utilizada para proteger el archivo especificado por <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Establece la versión mínima del servidor necesaria para emitir licencias para el contenido que se empaqueta. Especifique x (Acceso desde Adobe x.0) donde x = el número de versión principal. Los servidores anteriores a Adobe Access 3.0 no admiten esta configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si una directiva <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> requiere el registro del dominio con un servidor que utilice un certificado de transporte distinto del especificado en <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, se debe proporcionar el certificado de transporte de dominio. </p> <p class="- topic/p ">Esta propiedad especifica un archivo que contiene solo el certificado (se acepta el formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifique la clave de licencia. Si no se especifica ninguna clave, la clave se generará aleatoriamente. Cuando la rotación de claves no está habilitada, esta es la clave utilizada para cifrar el contenido. </p> <p class="- topic/p ">Cuando la rotación de clave está habilitada, esta clave se usa para proteger las claves de rotación. La clave debe tener 16 bytes de longitud y especificarse como valores hexadecimales. El espacio en blanco entre los valores hexadecimales es opcional. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica si la rotación de claves está habilitada. Si se establece en false (valor predeterminado), la rotación de claves está deshabilitada y se utilizará la CEK maestra para cifrar todas las muestras del contenido. </p> <p class="- topic/p ">Si se establece en true, se habilita la rotación de claves y se pueden utilizar claves diferentes para cifrar partes del contenido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Secuencia de claves giradas que se utiliza para cifrar contenido cuando se habilita la rotación de claves. Si no se especifica ninguna clave, las claves se generan aleatoriamente. Las claves deben tener 16 bytes de longitud y especificarse como valores hexadecimales. </p> <p class="- topic/p ">El espacio en blanco entre los valores hexadecimales es opcional. <i class="+ topic/ph hi-d/i ">n</i> debe aumentar monotónicamente, a partir de 1. Cuando se especifican varias teclas, estas se recorren en el orden indicado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el intervalo (en segundos) durante el cual se utilizará una clave de rotación para cifrar muestras de contenido. </p> <p class="- topic/p ">Después de encriptar esta cantidad de tiempo en el contenido, se utiliza la siguiente clave de rotación. Si la rotación de claves está habilitada y no se especifica ningún intervalo, las teclas girarán cada 15 minutos. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si el valor es True, no hay ningún servidor de licencias desde el que se puedan obtener las licencias. Las licencias deben estar incrustadas u obtenerse fuera de banda. El valor predeterminado es false si no se especifica. Solo se admite en Adobe Access Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>
