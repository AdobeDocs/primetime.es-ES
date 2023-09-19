---
title: Ejemplos de solicitudes de clientes
description: Ejemplos de solicitudes de clientes
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Ejemplos de solicitudes de clientes{#sample-client-requests}

Puede recopilar una biblioteca de solicitudes de cliente de ejemplo con herramientas como Charles Proxy o Wireshark. Debe capturar las solicitudes de los clientes una vez configurado el servidor de individualización mediante la credencial de transporte de individualización. A continuación, puede enviar estas solicitudes de cliente (mediante *rizar* u otra herramienta) al extremo del servidor de individualización para comprobar que el servidor funciona correctamente. Por ejemplo:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

También es posible que desee volver a enviar estas solicitudes después de cualquier cambio en la configuración del servidor o de actualizaciones de ECI/CRL.

También debe actualizar adecuadamente la página Estadísticas de Individualización con transacciones de individualización exitosas.
