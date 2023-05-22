---
title: Emisión de licencias para la entrega de claves remotas a clientes de iOS (requiere Adobe Primetime)
description: Emisión de licencias para la entrega de claves remotas a clientes de iOS (requiere Adobe Primetime)
copied-description: true
exl-id: 91eecc25-16a9-4f8c-9307-83e70bb77d68
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 0%

---

# Emisión de licencias para la entrega de claves remotas a clientes de iOS (requiere Adobe Primetime){#issuing-licenses-for-remote-key-delivery-to-ios-clients-requires-adobe-primetime}

Para emitir licencias para contenido que requiera la entrega de claves remotas para dispositivos iOS, el certificado del servidor de licencias del servidor de claves debe especificarse en `HandlerConfiguration.setKeyServerCertificate()`.
