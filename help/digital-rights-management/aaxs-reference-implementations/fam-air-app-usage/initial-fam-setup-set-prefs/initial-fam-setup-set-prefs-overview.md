---
title: Información general sobre preferencias de configuración
description: Información general sobre preferencias de configuración
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Información general sobre preferencias de configuración {#setting-preferences-overview}

Con la excepción de la URL del servidor de Packager, todas las preferencias especificadas a continuación se almacenan en el [!DNL flashaccess-refimpl-packager.properties] en el servidor. Todos los ajustes se pueden modificar directamente en el archivo de propiedades o a través de la aplicación AIR. Las contraseñas se cifran cuando se almacenan en el archivo de propiedades del servidor. Escriba la contraseña no cifrada en la interfaz de usuario y se cifrará antes de almacenarla en el archivo.

>[!NOTE]
>
>Todos los directorios y rutas hacen referencia a directorios del servidor del empaquetador, no del cliente que ejecuta la aplicación de AIR.

Cualquier cambio realizado aquí surtirá efecto inmediatamente después de guardar las preferencias. No es necesario reiniciar el servidor a menos que el subproceso Packager haya finalizado debido a problemas de configuración.

Las descripciones de preferencias utilizan los términos siguientes:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_tj5_hcz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Preferencia </th> 
   <th colname="2" class="- topic/entry entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> URL de Packager Server </td> 
   <td colname="2" class="- topic/entry "> Ubicación del servidor en ejecución <span class="filepath"> flashaccess-packager.war </span>; por ejemplo, <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Directorio de recursos </td> 
   <td colname="2" class="- topic/entry "> Directorio que contiene directivas, certificados, credenciales y cualquier otro recurso necesario para el servidor del empaquetador </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> URL del servidor de licencias </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL del servidor desde el que el cliente debe solicitar una licencia; por ejemplo, <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>
