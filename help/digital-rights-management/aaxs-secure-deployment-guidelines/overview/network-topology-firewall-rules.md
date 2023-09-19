---
title: Reglas del cortafuegos
description: Reglas del cortafuegos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Reglas del cortafuegos {#firewall-rules}

## URL entrantes {#section-F111526A9DB844CBBF21A3CAE5F50880}

Configure el cortafuegos externo de modo que exponga únicamente las direcciones URL de la funcionalidad de la aplicación que desee proporcionar a los usuarios finales. Permitir que los usuarios externos accedan a través del cortafuegos externo solo a las direcciones URL enumeradas en la siguiente tabla:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-bqs-whz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">URL raíz </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Finalidad </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/getServerVersion/v3</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL para determinar la versión del servidor. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-xr4-hdn-44"> 
     <li id="li-05925A4DE4114F7786FF93A66AB8A117"><span class="filepath"> /flashaccess/authn/v1/*</span> </li> 
     <li id="li-E76E9BA0160F4E7F9EBB64428C2D9F31"><span class="filepath"> /flashaccess/authn/v3/*</span> </li> 
     <li id="li-ED3C15EB4D194FFE99954BDB7D5C1E41"><span class="filepath"> /flashaccess/authn/v4/*</span> </li> 
     <li id="li-4DD6CBBE939F4E6EABA474E3DCCBD893"><span class="filepath"> /flashaccess/authn/v5/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL para la autenticación de usuarios. Esta dirección URL solo debe ser accesible si utiliza las API de cliente de acceso a Adobe para realizar la autenticación de usuario. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-yxs-rdn-44"> 
     <li id="li-49B9987ED6E14FADA66727448F923F84"><span class="filepath"> /flashaccess/license/v1/*</span> </li> 
     <li id="li-BF4A415E573C4C728E24D548F53D923C"><span class="filepath"> /flashaccess/license/v3/*</span> </li> 
     <li id="li-E6C551DDA030429B9D0073D2685B778A"><span class="filepath"> /flashaccess/license/v4/*</span> </li> 
     <li id="li-57811F4CD7304DBDAFADD65244AED0D9"><span class="filepath"> /flashaccess/license/v5/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Direcciones URL para emitir licencias a usuarios finales. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-ibl-5dn-44"> 
     <li id="li-189BE370CD5044F988A42335C3BFE420"><span class="filepath"> /flashaccess/sync/v3</span> </li> 
     <li id="li-B333B85FFE8A46DD884595B0A620B4EE"><span class="filepath"> /flashaccess/sync/v4</span> </li> 
     <li id="li-E4771D3C5AA5454CA1EDCFAA3E027CC1"><span class="filepath"> /flashaccess/sync/v5</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL para solicitudes de sincronización. Esta URL debe estar accesible sólo si especifica los requisitos de sincronización en las licencias. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-plq-ydn-44"> 
     <li id="li-81C96F93BA904C8C95B907F1A77E6494"><span class="filepath"> /flashaccess/domain/v3</span> </li> 
     <li id="li-40F0952F09674CA3B9AAFB5A62F9D02E"><span class="filepath"> /flashaccess/domain/v4</span> </li> 
     <li id="li-3ADE44B959B548F8A31A6FF08537AF46"><span class="filepath"> /flashaccess/domain/v5</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL para el registro de dominios. Esta dirección URL solo debe ser accesible si implementa la compatibilidad con el dominio. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-btm-c2n-44"> 
     <li id="li-3535EDF7C644406FAC471D4234C4AF98"><span class="filepath"> /flashaccess/dereg/v3</span> </li> 
     <li id="li-AB33657BC7E140E695767710DF7AEC72"><span class="filepath"> /flashaccess/dereg/v4</span> </li> 
     <li id="li-D15B32BCD4674269A3A2644DD5204707"><span class="filepath"> /flashaccess/dereg/v5</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Direcciones URL para la anulación de registro de dominios. Esta dirección URL solo debe ser accesible si implementa la compatibilidad con el dominio. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/headerconversion/v1/*</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Direcciones URL que el cliente puede usar para convertir metadatos DRM de FMRMS 1.x en metadatos DRM de acceso a Adobe. </p> <p class="- topic/p ">Nota: <i class="+ topic/ph hi-d/i ">Esta dirección URL debe utilizar SSL (HTTPS)</i>. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /edcws/services/urn:EDCLicenseService/*</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL del servicio web de LiveCycle Rights Management ES. Si el contenido se publicó con una versión anterior de FMRMS, esta dirección URL permite a los clientes más antiguos conectarse al servidor y se les pedirá que actualicen a Acceso de Adobe. </p> <p class="- topic/p ">Nota: <i class="+ topic/ph hi-d/i ">Esta dirección URL debe utilizar SSL (HTTPS)</i>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/lreturn/v5</span> </td> 
   <td colname="2" class="- topic/entry "> <p>URL para devolución de licencia. La dirección URL solo debe ser accesible si implementa la compatibilidad con devoluciones de licencias. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>El cortafuegos interno solo debe permitir que se realicen conexiones al servidor de licencias de acceso a Adobe a través del proxy inverso y solo a las URL enumeradas anteriormente. Para mejorar la escalabilidad, las conexiones entre el proxy inverso y el acceso al Adobe se realizarán a través de HTTP.

## URL salientes {#section-FFF9F7BB353149F4A27F8788E9934A48}

El servidor de licencias requiere acceso a través del cortafuegos para descargar las siguientes CRL desde la Adobe:

* h<span></span>ttps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl
* ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl
* ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl
* ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl
