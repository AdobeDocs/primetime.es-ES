---
description: 'null'
seo-description: 'null'
seo-title: Configuración de un servidor de dominio
title: Configuración de un servidor de dominio
uuid: bf85305e-9a00-4bc0-ba36-c870979456e4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configuración de un servidor de dominio{#set-up-a-domain-server}

Para configurar un servidor de dominio en una instalación de servidor de licencias existente:

1. En el [!DNL tomcat/lib] directorio, abra el [!DNL flashaccess-refimpl.properties] archivo.
1. En la `Domain CA certificate` opción, complete el certificado de CA de dominio.

   Este certificado se utiliza para aceptar los tokens de dominio.
1. En la `Domain CA credential` opción, complete los `Domain CA credential certificate (PFX)` detalles.

   A continuación, este certificado se utiliza para firmar certificados de dominio y tokens.
1. Especifique el valor para `DomainServerlURL`.

   Si este valor se establece en `NULL`, es posible que la autenticación del dominio se realice correctamente. Sin embargo, durante la unión al dominio, puede producirse un error de unión del dominio.
