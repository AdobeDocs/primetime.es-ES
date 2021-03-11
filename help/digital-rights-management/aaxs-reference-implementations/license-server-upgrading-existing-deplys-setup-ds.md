---
title: Configuración de un servidor de dominio
description: Configuración de un servidor de dominio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Configuración de un servidor de dominio {#set-up-a-domain-server}

Para configurar el servidor de dominio en una instalación de servidor de licencias existente, realice las siguientes tareas:

1. Abra el archivo [!DNL flashaccess-refimpl.properties] en [!DNL tomcat/lib].

1. En la opción `Domain CA certificate`, rellene los detalles del certificado de CA de dominio. Este certificado se utilizará para aceptar los tokens de dominio.
1. En la opción `Domain CA credential`, rellene los detalles de `Domain CA credential certificate (PFX)`. Este certificado se utilizará para firmar certificados de dominio y tokens.

1. Especifique el valor para `DomainServerlURL`. Si este valor es NULL, es posible que la autenticación del dominio se realice correctamente. Sin embargo, al unirse al dominio, habrá un error de unión del dominio.

