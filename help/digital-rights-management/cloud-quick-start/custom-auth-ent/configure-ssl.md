---
seo-title: Configurar SSL en el servidor BEES
title: Configurar SSL en el servidor BEES
uuid: 041a106e-8b21-4018-815d-b7ea48c3de03
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Configurar SSL en el servidor BEES {#configure-ssl-on-your-bees-server}

1. Proporcione el certificado SSL de servidor a su contacto de Adobe que suministró este software.

   El certificado se agregará como certificado de confianza al almacén de confianza de DRM de Primetime Cloud.
1. Para habilitar la autenticación de cliente para la conexión SSL (deshabilitada en esta versión):
   1. Agregue los certificados `[!DNL clouddrm-transport.cer]` y `[!DNL AdobeFlashAccessIntermediateCA.cer]` al almacén de confianza utilizado para la autenticación de cliente.
   1. Habilite la autenticación de cliente en la configuración SSL.
