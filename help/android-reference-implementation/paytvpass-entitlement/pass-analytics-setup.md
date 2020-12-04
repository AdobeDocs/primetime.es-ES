---
description: Puede configurar la implementación de referencia para utilizar Adobe Analytics sistema de informes.
seo-description: Puede configurar la implementación de referencia para utilizar Adobe Analytics sistema de informes.
seo-title: Configurar Adobe Analytics Sistema de informes
title: Configurar Adobe Analytics Sistema de informes
uuid: bdf8bb7f-a0c8-48a2-a632-0b872687f3fe
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Configurar Adobe Analytics Sistema de informes {#configure-adobe-analytics-reporting}

Puede configurar la implementación de referencia para utilizar Adobe Analytics sistema de informes.

La implementación de referencia está configurada para enviar datos de evento de autenticación Primetime a Adobe Analytics mediante la biblioteca móvil de Adobe incluida en el SDK de Primetime. Para habilitar y utilizar los datos de evento enviados desde la aplicación, primero debe crear una cuenta de Adobe Analytics. Una vez creada la cuenta:

1. Configure la aplicación con la información de su cuenta; y
1. Cree reglas de procesamiento para personalizar la forma en que se muestran los datos de evento en los informes.

La tabla siguiente presenta los datos enviados a Adobe Analytics:

| Nombre de la acción | `a.media.pass.event.MvpdSelection` | El usuario seleccionó un distribuidor de programación de vídeo con varios canales (MVPD) en un cuadro de diálogo de selección |
|---|---|---|
| Datos de contexto | `a.media.pass.MvpdId (String)` | MVPD seleccionado por el usuario |
|  | `a.media.pass.ClientType` | (Cadena) El tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot; |
|  |  |  |
| Nombre de la acción | `a.media.pass.event.AuthenticationDetection` | Se completó un flujo de trabajo de autenticación |
| Datos de contexto | `a.media.pass.Successful` | (Booleano) Si la solicitud de token se ha realizado correctamente, verdadero o falso |
|  | `a.media.pass.MvpdId` | (Cadena) MVPD seleccionado por el usuario |
|  | `a.media.pass.Guid` | (Cadena) Un ID de seguimiento |
|  | `a.media.pass.Cached` | (Booleano) Token ya en la caché, true o false |
|  | `a.media.pass.ClientType` | (Cadena) El tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot; |
|  |  |  |
| Nombre de la acción | `a.media.pass.event.AuthorizationDetection` | Se completó un flujo de trabajo de autorización |
| Datos de contexto | `a.media.pass.Successful` | (Booleano) Si la solicitud de token se ha realizado correctamente, verdadero o falso |
|  | `a.media.pass.MvpdId` | (Cadena) El usuario seleccionó MVPD |
|  | `a.media.pass.Guid` | (Cadena) Un ID de seguimiento |
|  | `a.media.pass.Cached` | (Booleano) Token ya en la caché, true o false |
|  | `a.media.pass.Error` | (Cadena) El error si falla el intento de autorización |
|  | `a.media.pass.ErrorDetails` | (Cadena) Detalles de error adicionales |
|  | `a.media.pass.ClientType` | (Cadena) El tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot; |

1. Configure la aplicación para utilizarla con Adobe Marketing Cloud.

   Para habilitar el envío de datos de autenticación Primetime a Adobe Analytics, se debe agregar un archivo de configuración [!DNL `ADBMobileConfig.json`] a la Implementación de referencia en tiempo de compilación. Tenga en cuenta que este es exactamente el mismo archivo de configuración que utiliza el SDK de Primetime para enviar datos de Video Analytics al Marketing Cloud. Consulte la [documentación de Adobe Marketing Cloud](https://microsite.omniture.com/t2/help/en_US/reference/) para obtener más información sobre cómo configurar una aplicación con su cuenta de Adobe Analytics.
1. Cree reglas de procesamiento.

   Los datos del evento de autenticación Primetime enviados por la implementación de referencia no aparecerán automáticamente en los informes de análisis. Primero debe utilizar los datos creando reglas de procesamiento. Consulte la [documentación de Adobe Analytics sobre la creación de reglas de procesamiento](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
