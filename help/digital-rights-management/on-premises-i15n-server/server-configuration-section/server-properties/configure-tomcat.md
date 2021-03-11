---
title: Configurar Tomcat
description: Configurar Tomcat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Configurar Tomcat{#configure-tomcat}

En el servidor de Individualización, modifique el archivo [!DNL conf/server.xml] de Tomcat para incluir información adicional en el registro de acceso. Puede utilizar esta información para generar informes.

1. Busque la configuración para `AccessLogValve` en [!DNL server.xml] y modifique el patrón como se muestra aquí:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` registrará el valor del  `x-forwarded-for` encabezado. Si utiliza un proxy inverso de Apache para reenviar solicitudes al servidor Tomcat, este encabezado contendrá la dirección IP del cliente original, mientras que `%h` registra la dirección IP del servidor Apache. `%{request-id}r` registrará el identificador de solicitud, que corresponde al ID de solicitud contenido en el registro de aplicación de Individualización.

1. Edite [!DNL conf/server.xml] y establezca la propiedad `unpackwars` en false.

   Para los servidores de Individualización y Generación de claves, es aconsejable editar [!DNL conf/server.xml] y establecer la propiedad `unpackwars` en `false`. De lo contrario, cuando actualices las GUERRAS, tal vez tengas que limpiar también las carpetas de la GUERRA desempaquetadas.

>[!NOTE]
>
>Los futuros clientes de DRM requerirán que habilite y configure el filtro CORS (Uso compartido de recursos de origen cruzado) que está disponible para Tomcat. Actualmente, ningún cliente de DRM tiene este requisito.

