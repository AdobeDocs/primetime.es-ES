---
title: Propiedades del archivo de configuración
description: Propiedades del archivo de configuración
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# Propiedades del archivo de configuración {#configuration-file-properties}

Antes de ejecutar Media Packager, especifique valores para las propiedades de Media Packager. El archivo de configuración especifica las siguientes propiedades. Para los nombres de propiedad que incluyen* n*, *n* representa un entero que comienza con 1 y aumenta para cada instancia de la propiedad.

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
   <td colname="2" class="- topic/entry "> Indica si se codificará el contenido de vídeo. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.audio</span> </td> 
   <td colname="2" class="- topic/entry "> Indica si codificar audio. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.script</span> </td> 
   <td colname="2" class="- topic/entry ">Indica si se cifrarán los datos de secuencia de comandos en FLV. <i class="+ topic/ph hi-d/i ">Las etiquetas de datos </i> onMetaDataand  <i class="+ topic/ph hi-d/i "></i> onXMPscript nunca se cifran, aunque esta opción esté habilitada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica el nivel de codificación de vídeo. Se utiliza un valor de alto para cifrar todo el contenido de vídeo, mientras que los valores medios y bajos se utilizan para cifrar partes del contenido de vídeo para archivos F4V que contienen contenido H.264. </p> <p class="- topic/p ">value = <span class="codeph"> high | media | low</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.secondsUnencryption</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si el valor es bueno a 0, el número especificado de segundos de contenido al principio del archivo no se cifrará. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Archivo de certificado del servidor de licencias utilizado para cifrar la clave. La propiedad <span class="codeph"> encrypt.keys.asymmetric.certfile</span> especifica un archivo que contiene solo el certificado (se acepta el formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esta propiedad se utiliza repetidamente para crear una lista de directivas que se aplican al contenido. <span class="codeph"> </span> es un número entero cuyo valor es 1 o bueno. El cliente utilizará la primera instancia de forma predeterminada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La URL del servidor de licencias. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El certificado de transporte para el servidor de licencias. Esta propiedad especifica un archivo <span class="filepath"> .cer</span> que contiene únicamente el certificado (se acepta el formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Archivo PKCS12 que contiene credenciales del empaquetador para firmar contenido. El <span class="codeph"> encrypt.sign.certfile</span> debe hacer referencia a un archivo <span class="filepath"> .pfx</span> que contenga un certificado y una clave privada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La contraseña utilizada para proteger el archivo especificado por <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Establece la versión mínima del servidor necesaria para emitir licencias para el contenido que se empaqueta. Especifique x (acceso a Adobe x.0) donde x = el número de versión principal. Los servidores anteriores a Adobe Access 3.0 no admiten esta configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si una directiva <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> requiere registro de dominio con un servidor que usa un certificado de transporte diferente al especificado en <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, debe proporcionarse el certificado de transporte de dominio. </p> <p class="- topic/p ">Esta propiedad especifica un archivo que contiene solo el certificado (se acepta el formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifique la clave de licencia. Si no se especifica ninguna clave, la clave se generará aleatoriamente. Cuando la rotación de claves no está habilitada, esta es la clave utilizada para cifrar el contenido. </p> <p class="- topic/p ">Cuando la rotación de claves está habilitada, esta clave se utiliza para proteger las claves de rotación. La clave debe tener una longitud de 16 bytes y especificarse como valores hexadecimales. El espacio en blanco entre los valores hexadecimales es opcional. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rot.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica si la rotación de claves está activada. Si se establece en false (predeterminado), la rotación de claves se desactiva y el CEK maestro se utilizará para cifrar todas las muestras del contenido. </p> <p class="- topic/p ">Si se establece en true, se habilitará la rotación de claves y se podrán utilizar claves diferentes para cifrar partes del contenido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rot.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Secuencia de claves giradas que se utilizan para cifrar contenido cuando la rotación de claves está habilitada. Si no se especifica ninguna clave, las claves se generarán aleatoriamente. Las claves deben tener una longitud de 16 bytes y especificarse como valores hexadecimales. </p> <p class="- topic/p ">El espacio en blanco entre los valores hexadecimales es opcional. <i class="+ topic/ph hi-d/i "></i> debe aumentar monotónicamente, a partir de 1. Cuando se especifican claves múltiples, las claves se recorren en el orden indicado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rot.range</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el intervalo (en segundos) durante el cual se utilizará una clave de rotación para cifrar muestras de contenido. </p> <p class="- topic/p ">Una vez que se haya cifrado esta cantidad de tiempo en el contenido, se utilizará la siguiente clave de rotación. Si la rotación de claves está habilitada y no se especifica ningún intervalo, las claves se girarán cada 15 minutos. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.server.less</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si es true, no hay ningún servidor de licencias desde el que se puedan obtener las licencias. Las licencias deben integrarse o obtenerse fuera de banda. El valor predeterminado es false si no se especifica lo contrario. Solo se admite en Adobe Access Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>

