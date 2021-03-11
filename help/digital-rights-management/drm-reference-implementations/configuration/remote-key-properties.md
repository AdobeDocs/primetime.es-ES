---
title: Propiedades de entrega de claves remotas (iOS)
description: Propiedades de entrega de claves remotas (iOS)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Propiedades de entrega de claves remotas (iOS){#remote-key-delivery-properties-ios}

Para admitir la generación de licencias para el envío de claves remotas a un cliente iOS en Adobe Primetime DRM, debe especificar el certificado de servidor de claves en el archivo `flashaccess-refimpl.properties` .

Se han agregado las siguientes propiedades en el DRM de Primetime :

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
   <td colname="2" class="- topic/entry "> <p>Certificado de servidor de licencias del servidor de claves emitido por Adobe. </p> <p>Este certificado genera licencias para dispositivos iOS cuando los metadatos indican que se requiere un servidor clave. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>El alias de un certificado de servidor de licencias emitido por el Adobe de Key Server que se almacena en HSM. </p> <p>Cuando habilite HSM, puede aplicar esta propiedad en lugar de la propiedad <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> . </p> </td> 
  </tr> 
 </tbody> 
</table>

