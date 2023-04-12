---
title: Requisitos mínimos del sistema
description: Requisitos mínimos del sistema
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Requisitos mínimos del sistema {#minimum-system-requirements}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.


## Información general {#overview}

Este documento presenta los requisitos actuales de software y hardware para implementar integraciones de autenticación de Adobe Primetime en plataformas admitidas. Todos los navegadores web/móviles compatibles y los sistemas operativos enumerados a continuación se beneficiarán de la compatibilidad completa del equipo de autenticación de Adobe Primetime, enlazado a los SLAs acordados.

Aunque como equipo de autenticación de Adobe Primetime, recomendamos el uso de las últimas versiones estables de los navegadores y sistemas operativos; también reconocemos la existencia de plataformas y navegadores no compatibles/antiguos que están actualmente en uso. Estos dispositivos obsoletos pueden funcionar sin problemas, sin embargo, son más propensos a errores.

El enfoque inicial para mitigar cualquier problema que aparezca en estas plataformas obsoletas debe ser actualizar a las versiones más recientes; puede ser la versión del sistema operativo, la versión del explorador o la versión de la aplicación instalada.

Cualquier problema que aparezca en estas plataformas será tratado como base del mejor esfuerzo por el equipo de autenticación de Adobe Primetime. 

Adobe Primetime anima a nuestros clientes y socios a que consideren la posibilidad de actualizar a las versiones más recientes para beneficiarse de la compatibilidad total de Adobe en cualquier problema potencial, además de las mejoras de rendimiento, eficacia y seguridad. 


## Requisitos del sistema operativo y del explorador {#browser-OS-system-requirements}


| Explorador web/móvil (†) | Versiones admitidas |
|---|---|
| Google Chrome | **70** o posterior |
| Mozilla Firefox | **57** o posterior |
| Apple Safari | **14** o posterior |
| Microsoft Edge | **100** o posterior |

(†) El Adobe aconseja no utilizar el modo privado o incógnito.

| Sistema operativo | Versiones admitidas |
|---|---|
| *Android* | **7,0** (Nougat) o posterior |
| *iOS* | **14** o posterior |
| *iPadOS* | **14** o posterior |
| *tvOS* | **14** o posterior |
| *Fire OS* | **5 (Android 5.1)** o posterior |
| *Mac OS* | **10,13** o posterior |
| *Microsoft Windows* | **10** o posterior |




>[!NOTE]
>
>Cookies de terceros: es posible que los flujos de derechos de autenticación de Adobe Primetime fallen cuando las cookies de terceros estén desactivadas.  Este problema solo se reproduce cuando se modifica la configuración del explorador. Para todos los exploradores compatibles, la autenticación de Primetime debe ser funcional con la configuración predeterminada.\
 

## Requisitos del dispositivo para implementaciones sin cliente (REST) {#general_clientless_reqs}

 
Cualquier dispositivo que consuma los servicios de autenticación de Adobe Primetime a través de implementaciones sin cliente **debe poder**:

* Proporcione un ID de dispositivo único con hash. Si el dispositivo no proporciona un ID de dispositivo con hash único, debe poder mantener un ID único proporcionado por la autenticación de Adobe Primetime. El dispositivo debe poder mantener el ID único de forma permanente en su almacenamiento local y proporcionar el ID exclusivo como ID de dispositivo al realizar llamadas a las API de autenticación de Adobe Primetime.
* Generar firmas digitales mediante el algoritmo HMAC-SHA1
* Establecer encabezados HTTP arbitrarios
* Consumir servicios web RESTful
* Analizar formatos de datos XML y JSON
* Enviar tráfico mediante HTTPS
* Gestión de códigos de error HTTP
