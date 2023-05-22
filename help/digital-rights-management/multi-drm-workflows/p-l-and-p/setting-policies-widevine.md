---
title: Uso de directivas de protección de salida
description: Uso de directivas de protección de salida
copied-description: true
exl-id: d91c9181-a6b2-4982-a3ba-57c4b56428eb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Uso de directivas de protección de salida{#using-output-protection-policies}

**Políticas de protección de salida Widevine**

Widevine admite de forma nativa las restricciones de protección de salida analógica y digital. Consulte la documentación de su proveedor de servicios Widevine sobre cómo adjuntar estas políticas a las licencias generadas.

Si utiliza Expressplay como proveedor de servicios de Widevine, adjunte directivas de protección de salida digital en el momento de la generación del token mediante el indicador hdcpOutputControl: Los valores permitidos son 0, 1, 2, donde 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2. Tanto HDCP_V1 como HDCP_V2 aplican las versiones 1.X y 2.X de HDCP, respectivamente.

En este momento, Expressplay no admite adjuntar restricciones de salida analógica

**Políticas de protección de salida PlayReady**

PlayReady también admite de forma nativa restricciones de protección de salida analógica y digital. Los valores del nivel de protección de salida que puede establecer. La página [Niveles de protección de salida](https://msdn.microsoft.com/en-us/library/dn468831.aspx) documenta los valores que puede establecer y el comportamiento esperado del cliente.

Si utiliza Expressplay, adjunte valores de nivel de protección de salida en el momento de la generación del token mediante los indicadores compressedDigitalAudioOPL, uncompressedDigitalAudioOPL, compressedDigitalVideoOPL, uncompressedDigitalVideoOPL y unknownOutputBehavior. Se documentan en [Solicitud de token de licencia de PlayReady](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
