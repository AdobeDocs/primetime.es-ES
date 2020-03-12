---
seo-title: Configuración de un servidor de dominio
title: Configuración de un servidor de dominio
uuid: b262ea86-f465-4ed1-b278-122d4dafc881
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configuración de un servidor de dominio {#set-up-a-domain-server}

Para configurar el servidor de dominio en una instalación de servidor de licencias existente, realice las siguientes tareas:

1. Abra el [!DNL flashaccess-refimpl.properties] archivo en [!DNL tomcat/lib].

1. En la `Domain CA certificate` opción, rellene los detalles del certificado de CA de dominio. Este certificado se utilizará para aceptar los tokens de dominio.
1. En la `Domain CA credential` opción, rellene los `Domain CA credential certificate (PFX)` detalles. Este certificado se utilizará para firmar certificados de dominio y tokens.

1. Especifique el valor para `DomainServerlURL`. Si este valor es NULO, la autenticación de dominio puede realizarse correctamente. Sin embargo, mientras se une al dominio, habrá un error de unión del dominio.

