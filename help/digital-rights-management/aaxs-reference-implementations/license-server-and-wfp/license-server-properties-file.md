---
seo-title: Archivo de propiedades del servidor de licencias
title: Archivo de propiedades del servidor de licencias
uuid: bede307a-2060-451f-baf5-d058702c0a7e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Archivo de propiedades del servidor de licencias {#license-server-properties-file}

Utilice el [!DNL flashaccess-refimpl.properties] archivo para configurar el componente Servidor de licencias de la implementación de referencia. Como mínimo, asegúrese de configurar las propiedades relacionadas con la credencial de transporte y la credencial del servidor de licencias. Las ubicaciones de los archivos de credenciales deben especificarse en relación con el directorio especificado por la `config.resourcesDirectory` propiedad. Este archivo también contiene varias propiedades relacionadas con el empaquetado de contenido: estas propiedades solo se utilizan para la conversión de metadatos de Flash Media Rights Management Server 1.x. Si modifica alguno de los valores de este archivo de propiedad, debe reiniciar el servidor de licencias para que los cambios surtan efecto.

Para admitir la generación de licencias para la entrega de claves remotas a clientes de iOS en Adobe Access, el certificado de servidor de claves debe especificarse en [!DNL flashaccess-refimpl.properties].

Se han agregado las siguientes propiedades en Adobe Access:

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
   <td colname="2" class="- topic/entry "> Certificado de servidor de licencias de Key Server, emitido por Adobe. Este certificado se utiliza para generar licencias para dispositivos iOS cuando los metadatos indican que se requiere un servidor de claves. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">Alias del certificado de servidor de licencias emitido por Adobe de Key Server almacenado en HSM. Cuando HSM está habilitado, utilice esta propiedad en lugar de <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </td> 
  </tr> 
 </tbody> 
</table>

