---
description: Al configurar una arquitectura de red segura, se requieren protocolos de red para la interacción entre Adobe Primetime DRM y otros sistemas de la red empresarial.
seo-description: Al configurar una arquitectura de red segura, se requieren protocolos de red para la interacción entre Adobe Primetime DRM y otros sistemas de la red empresarial.
seo-title: Protocolos de red Adobe Primetime DRM
title: Protocolos de red Adobe Primetime DRM
uuid: 8954e33c-83ac-4b40-9e45-005d4954b44e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Protocolos de red Adobe Primetime DRM {#adobe-primetime-drm-network-protocols}

Al configurar una arquitectura de red segura, se requieren protocolos de red para la interacción entre Adobe Primetime DRM y otros sistemas de la red empresarial.

Al configurar una arquitectura de red segura, se requieren los siguientes protocolos de red para esta interacción:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_itc_33z_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocolo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Usar </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los clientes de Flash Player, Adobe AIR® y Adobe Primetime se comunican con Primetime DRM a través de HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (opcional) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los clientes de Flash Player, Adobe AIR y Adobe Primetime pueden utilizar HTTPS para comunicarse con Primetime DRM; HTTPS (SSL) no es necesario a menos que admita clientes FMRMS 1.x. Para obtener más información, consulte <a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local"> Direcciones URL entrantes </a> y Configuración de SSL. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Puertos para servidores de aplicaciones {#ports-for-application-servers}

Puede configurar el servidor de licencias DRM de Adobe Primetime para que utilice cualquier puerto de red.

Estos puertos deben habilitarse o deshabilitarse en el servidor de seguridad interno, según la funcionalidad de red que desee permitir a los clientes que se conecten al servidor de aplicaciones que ejecuta Primetime DRM.

## Configuración de SSL {#configuring-ssl}

La capa de sockets seguros (SSL) solo es necesaria si necesita compatibilidad con los clientes de Flash Media Rights Management Server 1.x.

Se requiere SSL con autenticación de cliente para Adobe Primetime DRM Key Server. Para obtener más información, consulte [Uso del servidor de claves DRM de Adobe Primetime](../../using-the-drm-key-server/requirements.md).