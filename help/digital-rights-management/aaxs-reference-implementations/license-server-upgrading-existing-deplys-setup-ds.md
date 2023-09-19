---
title: Configuración de un servidor de dominio
description: Configuración de un servidor de dominio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Configuración de un servidor de dominio {#set-up-a-domain-server}

Para configurar el servidor de dominio en una instalación existente del servidor de licencias, realice las siguientes tareas:

1. Abra el [!DNL flashaccess-refimpl.properties] archivo en [!DNL tomcat/lib].

1. En el `Domain CA certificate` opción, rellene los detalles del certificado de CA de dominio. Este certificado se utilizará para aceptar los tokens de dominio.
1. En el `Domain CA credential` , rellene el campo `Domain CA credential certificate (PFX)` detalles. Este certificado se utilizará para firmar certificados de dominio y tokens.

1. Especifique el valor para `DomainServerlURL`. Si este valor es NULL, es posible que la autenticación del dominio se realice correctamente. Sin embargo, al unirse al dominio, se producirá un error de unión de dominio.
