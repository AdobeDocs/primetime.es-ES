---
seo-title: Uso de la línea de comandos
title: Uso de la línea de comandos
uuid: 273e9d3b-efeb-46fa-a4b1-f13247b4e498
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Uso de la línea de comandos {#command-line-usage}

El Administrador de listas de revocación se encuentra en el directorio \Reference Implementation\Command Line Tools del DVD. Para ejecutar la herramienta, utilice una de las sintaxis siguientes:

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
* `crlNumber` es un número de versión no negativo de la Lista de revocación de certificados (CRL). Este número debe incrementarse cada vez que se actualice la CRL.

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
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c archivo de configuración</span> </td> 
   <td colname="2" class="- topic/entry ">Especifica la ubicación del archivo de configuración. Si no se utiliza esta opción, el Administrador de listas de revocación buscará <span class="filepath"> flashaccesstools.properties</span> en el directorio de trabajo. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d nombre de archivo</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Muestra información sobre la lista de revocación. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e fecha</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) La fecha de caducidad de la lista de revocación. Utilice el formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:sec</span> (por ejemplo, 2009-01-31-14:30:00 representa el 31 de enero a las 2:30 p.m.). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filename[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">Agrega todas las entradas de la lista de revocación existente. Sólo se puede especificar un archivo existente. <p class="- topic/p ">Si esta lista existente se firmó con una credencial diferente a la que se está utilizando para firmar la nueva lista, especifique su archivo de certificado siguiente para que se pueda comprobar su firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si se debe sobrescribir el archivo de destino. Si el archivo de destino ya existe y -o no está establecido, se mostrará un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Si el archivo de destino ya existe, sobrescribirlo sin preguntar. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revoca el certificado identificado por <span class="codeph"> issuerName</span> y <span class="codeph"> serialNumber</span> en la fecha determinada. El <span class="codeph"> nombreemisor</span> debe seguir el formato de nombre 509 (por ejemplo, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>). Especifique los números de serie en formato hexadecimal. Especifique la fecha de revocación como <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:sec</span>, por ejemplo 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008. Si no se especifica la fecha de revocación, se utiliza la fecha actual. </p> </td> 
  </tr> 
 </tbody> 
</table>

