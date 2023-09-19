---
description: Puede configurar la Implementación de referencia para utilizar los informes de Adobe Analytics.
title: Configuración de informes de Adobe Analytics
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# Configuración de informes de Adobe Analytics {#configure-adobe-analytics-reporting}

Puede configurar la Implementación de referencia para utilizar los informes de Adobe Analytics.

La implementación de referencia está configurada para enviar datos de evento de autenticación de Primetime a Adobe Analytics mediante la biblioteca móvil de Adobe incluida en el SDK de Primetime. Para habilitar y utilizar los datos de evento enviados desde la aplicación, primero debe crear una cuenta de Adobe Analytics. Una vez creada la cuenta:

1. Configurar la aplicación con la información de la cuenta; y
1. Cree reglas de procesamiento para personalizar el modo en que se muestran los datos de evento en los informes.

La siguiente tabla presenta los datos enviados a Adobe Analytics:

| Nombre de acción | `a.media.pass.event.MvpdSelection` | El usuario seleccionó Multi-channel Video Programming Distribution (MVPD) en un cuadro de diálogo de selección |
|---|---|---|
| Datos de contexto | `a.media.pass.MvpdId (String)` | La MVPD seleccionada por el usuario |
|  | `a.media.pass.ClientType` | (Cadena) El tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot; |
|  | | |
| Nombre de acción | `a.media.pass.event.AuthenticationDetection` | Flujo de trabajo de autenticación completado |
| Datos de contexto | `a.media.pass.Successful` | (Booleano) Si la solicitud de token se realizó correctamente, verdadero o falso |
|  | `a.media.pass.MvpdId` | (Cadena) MVPD seleccionada por el usuario |
|  | `a.media.pass.Guid` | (Cadena) Un ID de seguimiento |
|  | `a.media.pass.Cached` | (Booleano) El token ya está en la caché, verdadero o falso |
|  | `a.media.pass.ClientType` | (Cadena) El tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot; |
|  | | |
| Nombre de acción | `a.media.pass.event.AuthorizationDetection` | Flujo de trabajo de autorización completado |
| Datos de contexto | `a.media.pass.Successful` | (Booleano) Si la solicitud de token se realizó correctamente, verdadero o falso |
|  | `a.media.pass.MvpdId` | (Cadena) El usuario seleccionó MVPD |
|  | `a.media.pass.Guid` | (Cadena) Un ID de seguimiento |
|  | `a.media.pass.Cached` | (Booleano) El token ya está en la caché, verdadero o falso |
|  | `a.media.pass.Error` | (Cadena) Error si se produjo un error en el intento de autorización |
|  | `a.media.pass.ErrorDetails` | (Cadena) Más detalles del error |
|  | `a.media.pass.ClientType` | (Cadena) El tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; o &quot;android&quot; |

1. Configure la aplicación para usarla con Adobe Marketing Cloud.

   Para habilitar el envío de datos de autenticación de Primetime Primetime a Adobe Analytics, una [!DNL `ADBMobileConfig.json`] El archivo de configuración de debe agregarse a la Implementación de referencia en tiempo de compilación. Tenga en cuenta que es exactamente el mismo archivo de configuración que utiliza el SDK de Primetime para enviar datos de Video Analytics al Marketing Cloud. Consulte la [Documentación de Adobe Marketing Cloud](https://microsite.omniture.com/t2/help/en_US/reference/) para obtener más información sobre cómo configurar una aplicación con su cuenta de Adobe Analytics.
1. Crear reglas de procesamiento.

   Los datos del evento de autenticación de Primetime enviados por la Implementación de referencia no aparecerán automáticamente en los informes de Analytics. Primero debe utilizar los datos creando reglas de procesamiento. Consulte la [Documentación de Adobe Analytics sobre la creación de reglas de procesamiento](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
