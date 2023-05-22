---
title: Información general
description: Información general
copied-description: true
exl-id: 1e06bead-4b45-4bf0-8bcf-1ea376af6bd8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Administrador de listas de actualización de directivas DRM {#policy-update-list-manager}

Utilice la herramienta de línea de comandos del Administrador de listas de actualización de directivas DRM de Primetime ( [!DNL AdobePolicyUpdateListManager.jar]) para crear y gestionar listas de actualización de directivas DRM y para comprobar si las directivas se han actualizado o revocado.

Antes de ejecutar la herramienta de línea de comandos del Administrador de listas de actualización de directivas, debe establecer las propiedades en la variable *Propiedades del Administrador de listas de actualización de directivas y del Administrador de listas de revocación* del archivo de configuración.

>[!NOTE]
>
>También puede especificar todas las propiedades del Administrador de listas de actualización de directivas desde la línea de comandos.

## Uso de la línea de comandos del Administrador de listas de actualización de directivas {#policy-update-list-manager-command-line-usage}

**Crear una lista de actualización de directivas:**

```
java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` indica el nombre del fichero en el que se escribe la lista de actualización de directivas DRM.

**Ver una lista de actualización de directivas existente:**

```
java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

* `filename` Nombre del archivo de lista de actualización de directivas.

**Tabla 4: Opciones de la línea de comandos**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción de línea de comandos </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c archivoDeConfiguración </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el nombre y la ubicación del archivo de configuración. </p> <p class="- topic/p ">Si no se especifica un nombre o una ubicación, el Administrador de listas de actualización de directivas DRM buscará <span class="filepath"> flashaccesstools.properties </span> en el directorio de trabajo actual. </p> <p>Nota: Las opciones que especifique en la línea de comandos tienen prioridad sobre las opciones especificadas en el fichero de configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d nombre de archivo </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Muestra información sobre la lista de actualización de directivas DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e fecha </span> </td> 
   <td colname="2" class="- topic/entry "> <p>(Opcional) Fecha de caducidad de la lista de actualización de la directiva DRM. </p> <p>Usar el formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span> (por ejemplo, 2009-01-31-14:30:00 representa el 31 de enero a las 2:30 p.m.). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f nombreDeArchivo [certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Añade todas las entradas de la lista de actualización de directivas DRM existente. Solo se puede especificar un archivo existente. </p> <p class="- topic/p ">Si la lista existente se ha firmado con una credencial distinta a la que se utiliza para firmar la nueva lista, debe especificar su archivo de certificado para comprobar su firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si el archivo de destino debe sobrescribirse. Si el archivo de destino ya existe y <span class="codeph"> -o </span> no se ha configurado, se produce un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si el archivo de destino ya existe, sobrescribirlo sin preguntar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r idDeDirectiva </span> <span class="+ topic/ph pr-d/codeph codeph"> fecha </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) Revoca el ID de la directiva DRM en la fecha especificada. Puede proporcionar un código de motivo, un texto de motivo y una URL de motivo opcionales. Debe especificar una cadena vacía "" para indicar que no se proporciona ningún valor para los parámetros opcionales. Puede especificar la fecha en <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span> en estos formatos. Por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 representa la medianoche del 1 de diciembre de 2008). Si no especifica una fecha, se aplica automáticamente la fecha actual. Por lo tanto, el código de razón debe ser bueno o igual a 0. También puede especificar varias opciones -r. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> fecha </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Realiza la misma acción que el <span class="codeph"> -r </span> opción. Sin embargo, extrae el identificador de la política DRM de un archivo especificado. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u nombreDeArchivo " códigoDeRazón " " textoDeRazón " " URLDeRazón" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Reemplaza cualquier política DRM coincidente en una solicitud de licencia por esta política DRM mediante el código de motivo dado (opcional), el texto de motivo (opcional) y la URL de motivo (opcional). </p> <p>Una cadena vacía "" indica que no ha proporcionado ningún valor para los parámetros opcionales. </p> <p>El código de motivo debe ser bueno o igual a <span class="codeph"> 0 </span>. Puede especificar varias <span class="codeph"> -u </span> opciones. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Propiedades de configuración {#configuration-properties}

Las siguientes propiedades del Administrador de listas de actualización de directivas DRM de Primetime especifican un archivo PKCS12 que incluye credenciales para firmar listas de revocación (Certificado de servidor de licencias), junto con una contraseña.

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
