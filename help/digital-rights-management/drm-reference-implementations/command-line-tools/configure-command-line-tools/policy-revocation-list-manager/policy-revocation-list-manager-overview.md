---
title: Administrador de listas de revocación DRM
description: Administrador de listas de revocación DRM
copied-description: true
exl-id: 5b17d195-30ca-4005-b710-83a6f77779a2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Administrador de listas de revocación DRM {#policy-revocation-list-manager}

Utilice la herramienta de línea de comandos del Administrador de listas de revocación de DRM de Primetime ( [!DNL AdobeRevocationListManager.jar]) para crear y administrar listas de revocación y para comprobar si se han revocado las directivas.

Antes de ejecutar [!DNL AdobeRevocationListManager.jar], debe establecer las propiedades en *Propiedades del Administrador de listas de actualización de directivas y del Administrador de listas de revocación* del archivo de configuración.

>[!NOTE]
>
>También puede especificar todas las propiedades del Administrador de listas de revocación desde la línea de comandos.

## Uso de la línea de comandos del Administrador de listas de revocación {#revocation-list-manager-command-line-usage}

```
java -jar AdobeRevocationListManager.jar 
<i class="+ topic ph hi-d="" i "="">
 destfile 
 <i class="+ topic ph hi-d="" i "="">
  crlNumber [
  <i class="+ topic ph hi-d="" i "="">
   options] 
       java -jar AdobeRevocationListManager.jar -d 
   <i class="+ topic ph hi-d="" i "="">
     filename
   </i class="+ topic>
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `destfile` especifica el nombre del archivo en el que se guardan las propiedades de la lista de revocación.
* `crlNumber` representa un número de versión no negativo de la lista de revocación de certificados (CRL). Debe aumentar este número cada vez que se actualiza la CRL.

**Tabla 5: Opciones de la línea de comandos**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opción de línea de comandos </th> 
   <th colname="2" class="- topic/entry entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c archivoDeConfiguración</span> </td> 
   <td colname="2" class="- topic/entry "><p class="- topic/p ">Especifica el nombre y la ubicación del archivo de configuración. </p><p class="- topic/p ">Si no se especifica un nombre o una ubicación, el Administrador de listas de revocación de DRM buscará <span class="filepath"> flashaccesstools.properties</span> en el directorio de trabajo actual. </p><p>Nota: Las opciones que especifique en la línea de comandos tienen prioridad sobre las opciones especificadas en el fichero de configuración. </p>Especifica la ubicación del archivo de configuración. Si no aplica esta opción, el Administrador de listas de revocación busca <span class="filepath"> flashaccesstools.properties</span> en el directorio de trabajo. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d nombre de archivo</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Muestra información acerca de la lista de revocación. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e fecha</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) Fecha de caducidad de la lista de revocación. Utilice uno de los siguientes formatos: 
     <ul id="ul_2C89F8183C3647C593CB67576D9DED07"> 
      <li id="li_A866F6CBCB464193A119A6609C8F3B2A"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> </li> 
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span> </li> 
     </ul>Por ejemplo, 2009-01-31-14:30:00 representa el 31 de enero a las 2:30 p.m. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f nombreDeArchivo[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Agrega todas las entradas de la lista de revocación existente. Solo se puede especificar un archivo existente. </p> <p class="- topic/p ">Si la lista existente se firmó con una credencial distinta de la que utilizó para firmar la nueva lista, debe especificar su archivo de certificado junto a comprobar su firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si el archivo de destino debe sobrescribirse. Si el archivo de destino ya existe y <span class="codeph"> -o</span> no se ha configurado, se produce un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Si el archivo de destino ya existe, puede sobrescribirlo sin que se le solicite. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r nombreDeEmisor númeroDeSerie revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revoca el certificado que ha identificado <span class="codeph"> IssuerName</span> y <span class="codeph"> serialNumber</span> en la fecha especificada. El <span class="codeph"> IssuerName</span> debe utilizar el formato de nombre 509. Por ejemplo, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>. </p> <p>Debe especificar los números de serie en formato hexadecimal. También debe especificar la fecha de revocación en uno de los siguientes formatos: 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span> </li> 
     </ul>Por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008. Si no especifica la fecha de revocación, se aplica automáticamente la fecha actual. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Propiedades de configuración {#configuration-properties}

Debe aplicar credenciales para firmar listas de revocación. Las siguientes propiedades del Administrador de listas de revocación especifican un archivo PKCS12 que incluye credenciales para firmar listas de revocación (Certificado de servidor de licencias), junto con la contraseña del certificado:

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
