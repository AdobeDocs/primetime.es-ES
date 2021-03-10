---
title: Configuración de un servidor de dominio
description: Configuración de un servidor de dominio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---


# Configuración de un servidor de dominio{#set-up-a-domain-server}

Para configurar un servidor de dominio en una instalación de servidor de licencias existente:

1. En el directorio [!DNL tomcat/lib], abra el archivo [!DNL flashaccess-refimpl.properties].
1. En la opción `Domain CA certificate`, complete el certificado de CA de dominio.

   Este certificado se utiliza para aceptar los tokens de dominio.
1. En la opción `Domain CA credential`, complete los detalles de `Domain CA credential certificate (PFX)`.

   A continuación, este certificado se utiliza para firmar certificados de dominio y tokens.
1. Especifique el valor para `DomainServerlURL`.

   Si este valor se establece en `NULL`, es posible que la autenticación del dominio se realice correctamente. Sin embargo, mientras se une al dominio, puede producirse un error de unión del dominio.
