---
title: Uso de la línea de comandos
description: Uso de la línea de comandos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Uso de la línea de comandos {#command-line-usage}

El Administrador de listas de revocación se encuentra en el directorio \Reference Implementation\Command Line Tools del DVD. Para ejecutar la herramienta, utilice una de las siguientes sintaxis:

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

* `destfile` indica dónde se escribirá la lista de revocación.
* `crlNumber` es un número de versión no negativo de la Lista de revocación de certificados (CRL). Este número debe incrementarse cada vez que se actualiza la CRL.

La siguiente tabla contiene descripciones de las opciones de la línea de comandos que se muestran en la sintaxis anterior:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opción de línea de comandos </th> 
   <th colname="2" class="- topic/entry entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c configfile</span> </td> 
   <td colname="2" class="- topic/entry ">Especifica la ubicación del archivo de configuración. Si no se utiliza esta opción, el Administrador de la lista de revocación buscará <span class="filepath"> flashaccesstools.properties</span> en el directorio de trabajo. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d nombre de archivo</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Muestra información sobre la lista de revocación. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e fecha</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) La fecha de caducidad de la lista de revocación. Utilice el formato <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> o <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> (por ejemplo, 2009-01-31-14:30:00 representa el 31 de enero a las 2:30 p. m). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filename[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">Agrega todas las entradas de la lista de revocación existente. Solo se puede especificar un archivo existente. <p class="- topic/p ">Si esta lista existente se firmó con una credencial diferente a la que se usa para firmar la nueva lista, especifique su archivo de certificado a continuación, para que se pueda verificar su firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si el archivo de destino debe sobrescribirse. Si el archivo de destino ya existe y -o no está establecido, se devuelve un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Si el archivo de destino ya existe, sobrescribirlo sin preguntar. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revoca el certificado identificado por <span class="codeph"> issuerName</span> y <span class="codeph"> serialNumber</span> en la fecha dada. El <span class="codeph"> issuerName</span> debe seguir el formato de nombre 509 (por ejemplo, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>). Especifique los números de serie en formato hexadecimal. Especifique la fecha de revocación como <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> o <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span>, por ejemplo 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de 1 de diciembre 1. 008. Si no se especifica la fecha de revocación, se utiliza la fecha actual. </p> </td> 
  </tr> 
 </tbody> 
</table>

