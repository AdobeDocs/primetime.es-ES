---
seo-title: Solicitudes de cliente de muestra
title: Solicitudes de cliente de muestra
uuid: 330d5e3c-1711-4375-bd11-e7702f0cde31
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# Solicitudes de cliente de muestra{#sample-client-requests}

Puede recopilar una biblioteca de solicitudes de cliente de ejemplo mediante herramientas como Charles Proxy o Wireshark. Debe capturar las solicitudes de cliente una vez configurado el servidor de individualización mediante la credencial Transporte de individualización. A continuación, puede enviar estas solicitudes de cliente (mediante *curl* u otra herramienta) al punto final del servidor de individualización para verificar que el servidor esté activo y funcionando correctamente. Por ejemplo:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

También puede que desee enviar estas solicitudes de nuevo después de realizar cualquier cambio en la configuración del servidor o de actualizar ECI/CRL.

También debe actualizar la página Estadísticas de individualización correctamente con las transacciones de individualización correctas.
