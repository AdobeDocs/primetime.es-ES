---
title: Ejemplos de solicitudes de cliente
description: Ejemplos de solicitudes de cliente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# Ejemplos de solicitudes de cliente{#sample-client-requests}

Puede recopilar una biblioteca de solicitudes de cliente de ejemplo mediante herramientas como Charles Proxy o Wireshark. Debe capturar las solicitudes del cliente después de configurar el servidor de Individualización mediante la credencial de transporte de individualización. A continuación, puede enviar estas solicitudes de cliente (a través de *curl* u otra herramienta) al punto final del servidor de individualización para verificar que el servidor está funcionando correctamente. Por ejemplo:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

También puede que desee volver a enviar estas solicitudes después de cualquier cambio en la configuración del servidor o de actualizaciones de ECI/CRL.

También debe actualizar correctamente la página Estadísticas de Individualización con transacciones de individualización correctas.
