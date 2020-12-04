---
seo-title: Uso de directivas de protección de salida
title: Uso de directivas de protección de salida
uuid: f00d2a97-0036-41a6-ab44-391cc40b146e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Uso de directivas de protección de salida{#using-output-protection-policies}

**Políticas amplias de protección de la producción**

Widevine admite de forma nativa tanto restricciones de protección de salida analógica como digital. Consulte la documentación de su proveedor de servicio de Widevine sobre cómo adjuntar estas directivas a las licencias generadas.

Si utiliza Expressplay como proveedor de servicio Widevine, adjunte políticas de protección de salida digital en el tiempo de generación de tokens a través del indicador hdcpOutputControl:
Los valores permitidos son 0, 1, 2 donde 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2. Tanto HDCP_V1 como HDCP_V2 aplican HDCP versión 1.X y 2.X respectivamente.

Expressplay no admite actualmente la adición de restricciones de salida analógicas

**Directivas de protección de salida PlayReady**

PlayReady también admite de forma nativa restricciones de protección de salida tanto analógica como digital. Los valores de nivel de protección de salida que se pueden definir. La página [Niveles de protección de salida](https://msdn.microsoft.com/en-us/library/dn468831.aspx) documentos los valores que puede establecer y el comportamiento esperado del cliente.

Si utiliza Expressplay, adjunte los valores de nivel de protección de salida en el tiempo de generación del token a través de los valores de compresiónDigitalAudioOPL, sin comprimirDigitalAudioOPL, zipDigitalVideoOPL, sin comprimirDigitalVideoOPL y el indicador unknownOutputBehavior. Estos se documentan en [Solicitud de token de licencia de PlayReady](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
