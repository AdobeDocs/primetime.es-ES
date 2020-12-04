---
seo-title: Configurar Tomcat
title: Configurar Tomcat
uuid: 5f23aa33-29d7-4b41-87a4-59dc5b433de4
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Configurar Tomcat{#configure-tomcat}

En el servidor de individualización, modifique el archivo [!DNL conf/server.xml] de Tomcat para incluir información adicional en el registro de acceso. Puede utilizar esta información con fines de sistema de informes.

1. Busque la configuración de `AccessLogValve` en [!DNL server.xml] y modifique el patrón como se muestra aquí:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` registrará el valor del  `x-forwarded-for` encabezado. Si utiliza un proxy inverso Apache para reenviar solicitudes al servidor Tomcat, este encabezado contendrá la dirección IP del cliente original, mientras que `%h` registra la dirección IP del servidor Apache. `%{request-id}r` registrará el identificador de la solicitud, que corresponde al ID de la solicitud incluido en el registro de la aplicación de individualización.

1. Edite [!DNL conf/server.xml] y establezca la propiedad `unpackwars` en false.

   Tanto para los servidores de individualización como de generación de claves, es recomendable editar [!DNL conf/server.xml] y establecer la propiedad `unpackwars` en `false`. De lo contrario, cuando se actualizan las GUERRAS, es posible que también haya que limpiar las carpetas de la GUERRA desembaladas.

>[!NOTE]
>
>Los futuros clientes de DRM requerirán que habilite y configure el filtro CORS (Uso compartido de recursos entre Orígenes) que está disponible para Tomcat. Actualmente, ningún cliente de DRM tiene este requisito.

