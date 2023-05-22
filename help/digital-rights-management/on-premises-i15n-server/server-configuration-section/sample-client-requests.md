---
title: Ejemplos de solicitudes de clientes
description: Ejemplos de solicitudes de clientes
copied-description: true
exl-id: 2b6a1349-aafc-4222-9081-525662f62961
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
