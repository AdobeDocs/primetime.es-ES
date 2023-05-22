---
title: Configuración de SSL en el servidor BEES
description: Configuración de SSL en el servidor BEES
copied-description: true
exl-id: 6823a71c-3be6-4c07-a3e6-e16bd931deaf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Configuración de SSL en el servidor BEES {#configure-ssl-on-your-bees-server}

1. Proporcione el certificado SSL del servidor al contacto de Adobe que proporcionó este software.

   El certificado se agregará como un certificado de confianza al almacén de confianza DRM de Primetime Cloud.
1. Para habilitar la autenticación de cliente para la conexión SSL (deshabilitada en esta versión):
   1. Añada el `[!DNL clouddrm-transport.cer]` y `[!DNL AdobeFlashAccessIntermediateCA.cer]` certificados al almacén de confianza utilizado para la autenticación de clientes.
   1. Habilite la autenticación de cliente en la configuración SSL.
