---
description: Puede configurar la Implementación de referencia para utilizar los informes de Adobe Analytics.
title: Configuración de informes de Adobe Analytics
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---


# Configuración de informes de Adobe Analytics {#configure-adobe-analytics-reporting}

Puede configurar la Implementación de referencia para utilizar los informes de Adobe Analytics.

La implementación de referencia está configurada para enviar datos de evento de autenticación de Primetime a Adobe Analytics mediante la biblioteca móvil de Adobe incluida en el SDK de Primetime. Para habilitar y utilizar los datos de evento enviados desde la aplicación, primero debe crear una cuenta de Adobe Analytics. Una vez creada la cuenta:

1. Configure la aplicación con la información de su cuenta; y
1. Cree reglas de procesamiento para personalizar el modo en que se muestran los datos del evento en los informes.

La tabla siguiente presenta los datos enviados a Adobe Analytics:

| Nombre de la acción | `a.media.pass.event.MvpdSelection` | El usuario seleccionó un distribuidor de programación de vídeo multicanal (MVPD) en un cuadro de diálogo de selección |
|---|---|---|
| Datos de contexto | `a.media.pass.MvpdId (String)` | MVPD seleccionado por el usuario |
|  | `a.media.pass.ClientType` | (Cadena) El tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot;. |
|  |  |  |
| Nombre de la acción | `a.media.pass.event.AuthenticationDetection` | Se completó un flujo de trabajo de autenticación |
| Datos de contexto | `a.media.pass.Successful` | (Booleano) Si la solicitud de token se ha realizado correctamente, si es verdadera o falsa |
|  | `a.media.pass.MvpdId` | (Cadena) MVPD seleccionado por el usuario |
|  | `a.media.pass.Guid` | (Cadena) Un ID de seguimiento |
|  | `a.media.pass.Cached` | (Booleano) Token ya en la caché, verdadero o falso |
|  | `a.media.pass.ClientType` | (Cadena) El tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot;. |
|  |  |  |
| Nombre de la acción | `a.media.pass.event.AuthorizationDetection` | Se completó un flujo de trabajo de autorización |
| Datos de contexto | `a.media.pass.Successful` | (Booleano) Si la solicitud de token se ha realizado correctamente, si es verdadera o falsa |
|  | `a.media.pass.MvpdId` | (Cadena) El usuario seleccionó MVPD |
|  | `a.media.pass.Guid` | (Cadena) Un ID de seguimiento |
|  | `a.media.pass.Cached` | (Booleano) Token ya en la caché, verdadero o falso |
|  | `a.media.pass.Error` | (Cadena) El error si falla el intento de autorización |
|  | `a.media.pass.ErrorDetails` | (Cadena) Más detalles del error |
|  | `a.media.pass.ClientType` | (Cadena) El tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot;. |

1. Configure la aplicación para usarla con Adobe Marketing Cloud.

   Para permitir el envío de datos de autenticación de Primetime Primetime a Adobe Analytics, se debe agregar un archivo de configuración [!DNL `ADBMobileConfig.json`] a la Implementación de referencia en el momento de la compilación. Tenga en cuenta que este es exactamente el mismo archivo de configuración que utiliza el SDK de Primetime para enviar datos de Video Analytics al Marketing Cloud. Consulte la [documentación de Adobe Marketing Cloud](https://microsite.omniture.com/t2/help/en_US/reference/) para obtener más información sobre cómo configurar una aplicación con su cuenta de Adobe Analytics.
1. Cree reglas de procesamiento.

   Los datos de evento de autenticación de Primetime enviados por la implementación de referencia no aparecerán automáticamente en los informes de análisis. Primero debe utilizar los datos creando reglas de procesamiento. Consulte la [documentación de Adobe Analytics sobre la creación de reglas de procesamiento](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
