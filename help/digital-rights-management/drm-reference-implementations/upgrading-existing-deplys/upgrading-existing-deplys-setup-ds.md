---
title: Configuración de un servidor de dominio
description: Configuración de un servidor de dominio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
