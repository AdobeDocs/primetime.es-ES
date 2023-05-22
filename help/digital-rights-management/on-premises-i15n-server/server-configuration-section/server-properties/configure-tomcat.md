---
title: Configuración de Tomcat
description: Configuración de Tomcat
copied-description: true
exl-id: 766b66dd-6070-4b0d-a860-a426fca05e56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Configuración de Tomcat{#configure-tomcat}

En el servidor de individualización, modifique el de Tomcat [!DNL conf/server.xml] para incluir información adicional en el registro de acceso. Puede utilizar esta información con fines de creación de informes.

1. Busque la configuración de `AccessLogValve` in [!DNL server.xml] y modifique el patrón como se muestra aquí:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` registrará el valor del `x-forwarded-for` encabezado. Si utiliza un proxy inverso Apache para reenviar solicitudes al servidor Tomcat, este encabezado contendrá la dirección IP del cliente original, mientras que `%h` registra la dirección IP del servidor Apache. `%{request-id}r` registrará el identificador de solicitud, que corresponde al ID de solicitud contenido en el registro de aplicaciones de individualización.

1. Editar [!DNL conf/server.xml] y configure el `unpackwars` propiedad en false.

   Tanto para los servidores de Individualización como de Generación de claves, es aconsejable editar [!DNL conf/server.xml] y configure el `unpackwars` propiedad a `false`. De lo contrario, cuando actualice los archivos WAR, es posible que tenga que limpiar también las carpetas WAR desempaquetadas.

>[!NOTE]
>
>Los futuros clientes de DRM necesitarán que active y configure el filtro CORS (Intercambio de Recursos de Origen Cruzado) disponible para Tomcat. Actualmente, ningún cliente DRM tiene este requisito.
