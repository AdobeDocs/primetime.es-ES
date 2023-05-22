---
title: Propiedades de entrega de claves remotas (iOS)
description: Propiedades de entrega de claves remotas (iOS)
copied-description: true
exl-id: 0fe3ed9b-a8ee-43b4-ab3c-8ea2e696503b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Propiedades de entrega de claves remotas (iOS){#remote-key-delivery-properties-ios}

Para admitir la generación de licencias para la entrega de claves remotas a un cliente de iOS en Adobe Primetime DRM , debe especificar el certificado de servidor de claves en la `flashaccess-refimpl.properties` archivo.

Se han añadido las siguientes propiedades en Primetime DRM:

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
   <td colname="2" class="- topic/entry "> <p>Certificado del servidor de licencias del servidor de claves emitido por el Adobe. </p> <p>Este certificado genera licencias para dispositivos iOS cuando los metadatos indican que se requiere un servidor de claves. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Alias de un certificado de servidor de licencias emitido por Adobe de Key Server que se almacena en HSM. </p> <p>Al habilitar HSM, puede aplicar esta propiedad en lugar del <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> propiedad. </p> </td> 
  </tr> 
 </tbody> 
</table>
