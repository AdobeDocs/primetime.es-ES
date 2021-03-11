---
title: Uso de directivas de protección de salida
description: Uso de directivas de protección de salida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Uso de directivas de protección de salida{#using-output-protection-policies}

**Políticas de protección de la producción de Widevine**

Widevine es compatible de forma nativa con las restricciones de protección de salida analógica y digital. Consulte la documentación del proveedor de servicios de Widevine sobre cómo adjuntar estas directivas a las licencias generadas.

Si utiliza Expressplay como proveedor de servicios de Widevine, adjunte políticas de protección de salida digital en el momento de la generación de tokens mediante el indicador hdcpOutputControl :
Los valores permitidos son 0, 1, 2, donde 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2. Tanto HDCP_V1 como HDCP_V2 aplican HDCP versión 1.X y 2.X respectivamente.

Expressplay actualmente no admite adjuntar restricciones de salida analógicas

**Políticas de protección de salida PlayReady**

PlayReady también admite de forma nativa restricciones de protección de salida analógica y digital. Los valores de nivel de protección de salida que puede establecer. La página [Niveles de protección de salida](https://msdn.microsoft.com/en-us/library/dn468831.aspx) documenta los valores que puede establecer y el comportamiento esperado del cliente.

Si utiliza Expressplay, adjunte valores de nivel de protección de salida en el tiempo de generación de tokens a través de los indicadores zipDigitalAudioOPL, unzipDigitalAudioOPL, zipDigitalVideoOPL, unzipDigitalVideoOPL y unknownOutputBehavior. Estos se documentan en [PlayReady License Token Request](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
