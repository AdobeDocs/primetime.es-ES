---
title: Configurar SSL en el servidor BEES
description: Configurar SSL en el servidor BEES
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Configure SSL en su servidor BEES {#configure-ssl-on-your-bees-server}

1. Proporcione el certificado SSL del servidor al contacto del Adobe que suministró este software.

   El certificado se agregará como certificado de confianza al almacén de confianza de DRM de Primetime Cloud.
1. Para habilitar la autenticación de cliente para la conexión SSL (deshabilitada en esta versión):
   1. Agregue los certificados `[!DNL clouddrm-transport.cer]` y `[!DNL AdobeFlashAccessIntermediateCA.cer]` al almacén de confianza utilizado para la autenticación de clientes.
   1. Habilite la autenticación de cliente en la configuración SSL.
