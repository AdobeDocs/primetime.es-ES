---
seo-title: Información general
title: Información general
uuid: 857390be-dd14-46c0-b8f7-2bc661c515d4
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# Generador de licencias DRM {#license-generator}

Utilice [!DNL AdobeLicenseGenerator.jar] para generar licencias sin requerir que el cliente envíe una solicitud de licencia a un servidor. A continuación, puede incrustar una licencia pregenerada en el contenido o entregar la licencia al cliente a través de otros mecanismos, como un servidor web HTTP sencillo.

## Uso de la línea de comandos del Generador de licencias {#license-generator-command-line-usage}

**Generar una licencia:**

```
java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

* `metadata` - Incluye los metadatos DRM de Adobe Primetime.

   Puede recuperar este archivo del contenido protegido con las opciones `-d -m` de Media Packager.

**Mostrar una licencia generada anteriormente:**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license` - Contiene una licencia DRM de Adobe Primetime generada por el Generador de licencias.

**Tabla 6: Opciones**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción de línea de comandos </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c archivo de configuración</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el nombre y la ubicación del archivo de configuración. </p> <p class="- topic/p ">Si no especifica un nombre ni una ubicación, el generador de licencias de DRM busca <span class="filepath"> flashaccesstools.properties</span> en el directorio de trabajo actual. </p> <p>Nota:  Las opciones que especifique en la línea de comandos tendrán prioridad sobre las opciones que especifique en el archivo de configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> archivo de licencia</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Muestra información sobre una licencia que ya se ha generado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-archivo hoja de hoja</span> </td> 
   <td colname="2" class="- topic/entry "> Genera una licencia de hoja y guarda la salida en un archivo especificado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m nombreDeArchivoDeMetadatos</span> </td> 
   <td colname="2" class="- topic/entry "> Especifica los metadatos de contenido para los que debe generar una licencia. Esta opción es necesaria para generar una licencia. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">No pregunte si se debe sobrescribir el archivo de destino. Si el archivo de destino ya existe y no se ha establecido <span class="codeph"> -o</span>, se produce un error. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Si el archivo de destino ya existe, puede sobrescribirlo sin que se le solicite. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy policy policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Si los metadatos incluyen varias directivas DRM, puede especificar el número de directivas DRM que puede utilizar para generar una licencia. </p> <p>Si no especifica el número de directivas DRM, se aplica automáticamente la primera directiva DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r certificado de destinatario</span> </td> 
   <td colname="2" class="- topic/entry ">Genera una licencia para un destinatario especificado. Puede utilizar un certificado de dispositivo o dominio y especificar varias <span class="+ topic/ph pr-d/codeph codeph"> -r </span>opciones para crear una licencia para varios destinatarios. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root root root_nombredearchivo</span> </td> 
   <td colname="2" class="- topic/entry "> Genera una licencia raíz y guarda la salida en un archivo especificado. </td> 
  </tr> 
 </tbody> 
</table>

## Propiedades del archivo de configuración {#configuration-file-properties}

Antes de ejecutar el generador de licencias, debe especificar los valores de las propiedades del generador de licencias en el archivo de configuración.

>[!NOTE]
>
>Para los nombres de propiedad que incluyen *n*, *n* representa un entero que comienza por 1 y aumenta para cada instancia de la propiedad.

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
   <td colname="2" class="- topic/entry "> <p>Establece la versión mínima de cliente compatible actualmente. Si no establece esta propiedad, todas las versiones se admitirán automáticamente de forma predeterminada. </p> <p>Puede definir este valor para controlar cómo responden los clientes más antiguos a los requisitos de licencia que no admiten. Especifique <span class="codeph"> x</span> (para Adobe Primetime DRM x.0) donde <span class="codeph"> x</span> representa un número de versión mayor. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificado de servidor de claves, que es un certificado de servidor de licencias emitido por Adobe que utiliza el servidor de claves. Este certificado se aplica solo si la directiva de metadatos/DRM indica que se requiere un servidor clave para la entrega de claves a dispositivos iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> El archivo PKCS12 que incluye las credenciales del servidor de licencias para firmar licencias. Esta propiedad debe hacer referencia a un archivo .pfx que incluya un certificado y una clave privada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">La contraseña que protege el archivo que ha especificado con la opción <span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certfile</span>. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Si genera licencias vinculadas al dominio, debe especificar uno o más certificados de CA de dominio para indicar las autoridades de dominio en las que puede confiar el emisor de la licencia. </p> <p>Si el destinatario de la licencia es un certificado de dominio, que no fue emitido por una de las CA de dominio especificadas, no se puede generar una licencia. Esta propiedad especifica un archivo <span class="filepath"> .cer</span> que incluye el certificado en el formato PEM o DER. <span class="codeph">No </span> debe aumentar monotónicamente, comenzando desde 1. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Archivo PKCS12 opcional que incluye credenciales adicionales del servidor de licencias para descifrar el CEK en los metadatos y la directiva DRM. Puede configurar credenciales adicionales si el contenido se ha empaquetado previamente con un certificado de servidor de licencias distinto de las credenciales especificadas con <span class="codeph"> licencisegen.sign.certfile</span>. Esta propiedad necesita hacer referencia a un archivo <span class="filepath"> .pfx</span> que incluye un certificado y una clave privada. <span class="codeph">No </span> debe aumentar monotónicamente, comenzando desde 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>La contraseña se aplica para proteger el archivo especificado con la propiedad<span class="+ topic/ph pr-d/codeph codeph"> licenseSegen.keys.asiymmetric.licenseServerCredential.n</span>. </p> </td> 
  </tr> 
 </tbody> 
</table>