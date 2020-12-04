---
seo-title: Propiedades del archivo de configuración
title: Propiedades del archivo de configuración
uuid: 13e158a6-c447-4e5e-884d-03fb4835c120
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Propiedades del archivo de configuración {#configuration-file-properties}

Antes de ejecutar el Generador de licencias, especifique los valores de las propiedades del Generador de licencias. El archivo de configuración especifica las siguientes propiedades. Para los nombres de propiedad que incluyen *n*, *n* representa un entero que comienza con 1 y aumenta para cada instancia de la propiedad.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Propiedad </th> 
   <th colname="2" class="- topic/entry entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> Establezca la versión mínima del cliente admitida. Si no se establece, de forma predeterminada se admiten todas las versiones. Establezca este valor para controlar la forma en que los clientes más antiguos responden a los requisitos de licencia que no admiten. Especifique x (para Adobe Access x.0) donde x es el número de versión principal. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificado de servidor de claves (un certificado de servidor de licencias emitido por Adobes que utiliza el servidor de claves). Este certificado solo se utiliza si los metadatos o la directiva indican que se requiere un servidor de claves para el envío de claves en dispositivos iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> El archivo PKCS12 que contiene las credenciales del servidor de licencias para firmar licencias. Esta propiedad debe hacer referencia a un archivo .pfx que contenga un certificado y una clave privada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">La contraseña usada para proteger el archivo especificado por <span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certfile.</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> Si se generan licencias enlazadas a dominios, se debe especificar uno o más certificados de CA de dominio para indicar las autoridades de dominio en las que confía este emisor de licencias. Si el destinatario de licencia es un certificado de dominio, que no ha sido emitido por una de las CA de dominio especificadas, no se puede generar una licencia. Esta propiedad especifica un archivo .cer que contiene únicamente el certificado (se acepta el formato PEM o DER). n debe aumentar monotónicamente, comenzando desde 1. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Archivo PKCS12 opcional que contiene credenciales adicionales del servidor de licencias para descifrar el CEK en los metadatos y la directiva. Se pueden configurar credenciales adicionales si el contenido se empaquetó previamente con un certificado de servidor de licencias distinto del especificado por <span class="codeph"> licencisegen.sign.certfile</span>. Esta propiedad debe hacer referencia a un archivo <span class="filepath"> .pfx</span> que contiene un certificado y una clave privada. n debe aumentar monotónicamente, comenzando desde 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">La contraseña utilizada para proteger el archivo especificado por: <p><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>

