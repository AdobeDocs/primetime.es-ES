---
title: Configuración de un servidor de dominio
description: Configuración de un servidor de dominio
copied-description: true
exl-id: eeb0d39d-58a4-4414-9123-2cf1b27b73de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# Configuración de un servidor de dominio{#set-up-a-domain-server}

Para configurar un servidor de dominio en una instalación de servidor de licencias existente:

1. En el [!DNL tomcat/lib] , abra el directorio [!DNL flashaccess-refimpl.properties] archivo.
1. En el `Domain CA certificate` opción, complete el certificado de CA de dominio.

   Este certificado se utiliza para aceptar los tokens de dominio.
1. En el `Domain CA credential` opción, complete la `Domain CA credential certificate (PFX)` detalles.

   Este certificado se utiliza para firmar certificados de dominio y tokens.
1. Especifique el valor para `DomainServerlURL`.

   Si este valor se establece en `NULL`, es posible que la autenticación del dominio se realice correctamente. Sin embargo, al unirse al dominio, puede producirse un error de unión de dominio.
