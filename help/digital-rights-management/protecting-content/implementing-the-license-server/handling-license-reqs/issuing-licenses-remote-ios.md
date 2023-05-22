---
title: Emisión de licencias para la entrega de claves remotas a clientes de iOS (requiere Adobe Primetime)
description: Emisión de licencias para la entrega de claves remotas a clientes de iOS (requiere Adobe Primetime)
copied-description: true
exl-id: f9f13ab3-3394-4729-a64c-f28c67601e26
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Emisión de licencias para la entrega de claves remotas a clientes de iOS (requiere Adobe Primetime){#issuing-licenses-for-remote-key-delivery-to-ios-clients-requires-adobe-primetime}

Si desea emitir licencias para contenido que requiera la entrega de claves remotas para dispositivos iOS, debe especificar el certificado del servidor de licencias del servidor de claves en `HandlerConfiguration.setKeyServerCertificate()`.
