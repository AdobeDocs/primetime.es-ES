---
title: Configuración de un servidor de dominio
description: Configuración de un servidor de dominio
copied-description: true
exl-id: b2589412-25e4-44c8-be11-8b2cfccbf7bb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
