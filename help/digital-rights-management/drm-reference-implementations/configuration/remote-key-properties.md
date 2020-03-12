---
description: 'null'
seo-description: 'null'
seo-title: Propiedades de entrega de claves remotas (iOS)
title: Propiedades de entrega de claves remotas (iOS)
uuid: 17e1b756-d106-47a7-99ae-641190693870
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Propiedades de entrega de claves remotas (iOS){#remote-key-delivery-properties-ios}

Para admitir la generación de licencias para la entrega de claves remotas a un cliente iOS en Adobe Primetime DRM, debe especificar el certificado del servidor de claves en el `flashaccess-refimpl.properties` archivo.

Se han agregado las siguientes propiedades en Primetime DRM:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_xz2_lwy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Propiedad </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Certificado de servidor de licencias de Key Server emitido por Adobe. </p> <p>Este certificado genera licencias para dispositivos iOS cuando los metadatos indican que se requiere un servidor de claves. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Alias del certificado de servidor de licencias emitido por Adobe de Key Server que se almacena en HSM. </p> <p>Al habilitar HSM, puede aplicar esta propiedad en lugar de la propiedad <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> . </p> </td> 
  </tr> 
 </tbody> 
</table>

