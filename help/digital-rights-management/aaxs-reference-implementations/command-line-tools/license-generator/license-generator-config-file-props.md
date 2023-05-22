---
title: Propiedades del archivo de configuración
description: Propiedades del archivo de configuración
copied-description: true
exl-id: ce4193fa-d217-4134-b08e-715c2cc57c84
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Propiedades del archivo de configuración {#configuration-file-properties}

Antes de ejecutar el Generador de licencias, especifique los valores de las propiedades del Generador de licencias. El archivo de configuración especifica las siguientes propiedades. Para nombres de propiedades que incluyen *n*, *n* representa un entero que comienza por 1 y aumenta para cada instancia de la propiedad.

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
   <td colname="2" class="- topic/entry "> Establezca la versión de cliente mínima admitida. Si no se configura, de forma predeterminada se admiten todas las versiones. Establezca este valor para controlar cómo responden los clientes más antiguos a los requisitos de licencia que no admiten. Especifique x (para Acceso al Adobe x.0), donde x es el número de versión principal. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licenses.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificado de servidor de claves (un certificado de servidor de licencias emitido por Adobe utilizado por el servidor de claves). Este certificado solo se utiliza si la directiva o los metadatos indican que se requiere un servidor de claves para la entrega de claves a los dispositivos iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> Archivo PKCS12 que contiene las credenciales del servidor de licencias para firmar licencias. Esta propiedad debe hacer referencia a un archivo .pfx que contenga un certificado y una clave privada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">La contraseña utilizada para proteger el archivo especificado por <span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certfile.</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> Si se generan licencias enlazadas al dominio, se deben especificar uno o más certificados de CA de dominio para indicar las autoridades de dominio en las que confía este emisor de licencias. Si el destinatario de la licencia es un certificado de dominio, que no fue emitido por una de las CA de dominio especificadas, no se puede generar una licencia. Esta propiedad especifica un archivo .cer que contiene solo el certificado (se acepta el formato PEM o DER). n debe aumentar monotónicamente, a partir de 1. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Archivo PKCS12 opcional que contiene credenciales adicionales del servidor de licencias para descifrar el CEK en los metadatos y la directiva. Se pueden configurar credenciales adicionales si el contenido se ha empaquetado anteriormente con un certificado del servidor de licencias distinto del especificado por <span class="codeph"> licencisegen.sign.certfile</span>. Esta propiedad debe hacer referencia a un <span class="filepath"> .pfx</span> archivo que contiene un certificado y una clave privada. n debe aumentar monotónicamente, a partir de 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">La contraseña utilizada para proteger el archivo especificado por: <p><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>
