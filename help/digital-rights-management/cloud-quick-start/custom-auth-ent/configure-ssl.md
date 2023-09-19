---
title: Configuración de SSL en el servidor BEES
description: Configuración de SSL en el servidor BEES
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
