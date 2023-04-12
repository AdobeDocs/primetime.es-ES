---
title: Integración de datos del servidor de autenticación de Primetime en Adobe Analytics
description: Integración de datos del servidor de autenticación de Primetime en Adobe Analytics
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 4%

---


# Integración de datos del servidor de autenticación de Primetime en Adobe Analytics

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

Los clientes de autenticación de Adobe Primetime desean ver los datos del servidor de autenticación de Primetime (Adobe Pass) en el panel de Adobe Analytics para un consumo más sencillo.

Los datos sirven para realizar el seguimiento de métricas importantes de TVE, tales como tasas de conversión de autenticación por MVPD, usuarios únicos basados en el ID de usuario de MVPD y más.

No está pensado para reemplazar una implementación del lado del cliente si ya existe una, ya que la actividad del usuario no se puede rastrear más allá de los eventos específicos a continuación en ausencia de un ID de visitante. Si los clientes proporcionan un ID de visitante en las llamadas Pass , podemos desbloquear otro tipo de integración de Analytics (en tiempo real) que pueda unirse a todos los eventos Pass con los datos de clientes existentes, obtenga más información sobre este nuevo tipo de posible integración aquí: &quot;[Uso del ID de Experience Cloud en la autenticación de Primetime](/help/authentication/exp-cloud-id-authn.md)&quot;

## Métricas incluidas {#metrics-included-int-authn-analyt}

| Evento | Descripción |
|----------------------------|----------------------------------------------------------------------------------------------------------------------|
| Se solicitó AuthN | Número de flujos de autenticación iniciados |
| AuthN pendiente | Número de tokens de autenticación generados correctamente (sin tener en cuenta si el cliente lo obtuvo o no) |
| AuthN OK | Número de tokens de autenticación obtenidos correctamente por los usuarios |
| Se solicitó AuthZ | Número de autorizaciones intentadas |
| AuthZ OK | Número de autorizaciones correctas |
| Error de AuthZ | Número de autorizaciones denegadas por MVPD a nivel de aplicación |
| Reproducir solicitud | Número de tokens de medios cortos generados (que se asimilan al número de solicitudes de reproducción) |
| Cerrar sesión solicitado | Número de flujos de cierre de sesión iniciados |
| Cierre de sesión completado | Número de flujos de cierre de sesión completados correctamente |
| Error de cierre de sesión | Número de flujos de cierre de sesión fallidos |
| Preautorización solicitada | Número de flujos de preautorización iniciados |
| Preautorización Aceptar | Número de eventos de preautorización correctos con los recursos previamente autorizados |
| Preautorización denegada | Número de eventos de preautorización con los recursos a los que se denegó la preautorización |
| Error de preautorización | Número de eventos de preautorización que han fallado |

| Nombre de Adobe Analytics | Descripción |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Canal | El ID del solicitante utilizado para realizar la solicitud de asignación de derechos |
| MVPD | El MVPD responsable de conceder el derecho al usuario |
| Proxy | El MVPD proxy (que será &quot;directo&quot; para integraciones directas) |
| Tipo de SDK | El SDK de cliente utilizado (Flash, HTML5, Android nativo, iOS, Clientless, etc.) |
| Versión del SDK | La versión del SDK del cliente de autenticación de Adobe Primetime |
| ID de recurso | El título real del recurso que participa en la solicitud de autorización (extraído de la carga útil MRSS como elemento/título, si se proporciona) |
| Tipo de error AuthZ | El motivo de los errores, tal como indica la autenticación de Adobe Primetime <br/> Estos son los valores más comunes <br/> **noAuthZ** = el MVPD respondió que el usuario no tiene el canal en su paquete<br/> **network** = no pudimos llegar al MVPD (MVPD tiene un problema en el momento de la llamada y no respondió)<br/> **norefreshtoken** = esto es estrictamente para implementaciones de OAuth y podría resultar si el usuario cambió su contraseña o el MVPD la negó por alguna razón. Generalmente resulta en una nueva autenticación<br/> **dismatch** = si la solicitud se realiza desde un dispositivo distinto al que tenía el token de autenticación. Puede producirse si los usuarios intentan engañar al sistema, pero la mayoría de estos sucesos se produjeron en el contexto de nuestro antiguo SDK de JavaScript, donde el ID del dispositivo utilizaba la dirección IP como parte del cálculo. Si un usuario viera TVE en casa y luego en el trabajo, este error se activaría y tendría que autenticarse de nuevo<br/> **no válido** = solicitud no válida, falta o parámetros no válidos<br/>  **authzNone** = Los programadores tienen la capacidad de denegar autorizaciones para una combinación de channelMVPD específica. Esto se activa mediante una API back-end a la que los programadores tienen acceso<br/> **fraude** = es un mecanismo de protección de nuestro lado. Si el usuario falla en la autorización y luego la solicita de nuevo varias veces en un corto intervalo (segundos), denegamos la llamada directamente. Suele suceder cuando un programador tiene un error en su implementación que solicita la autorización constantemente si falla. |
| Tipo de token | Cuando se crean tokens debido a AuthZ All y AuthN All, tenemos que saber qué se producen por una medida de degradación.<br/> Son:<br/> &quot;normal&quot; = El caso normal<br/> &quot;authnall&quot; = Cuando AuthN All está habilitado<br/> &quot;authzall&quot; = Cuando AuthZ Todo está habilitado<br/>  &quot;hba&quot; = Cuando el HBA está habilitado |
| Tipo de dispositivo sin cliente | La plataforma del dispositivo (alternativa), que actualmente se utiliza para Clientless.<br/> Los valores pueden ser:<br/> N/D: el evento no se originó desde un SDK sin cliente<br/> Desconocido: desde el parámetro deviceType de un **API sin cliente** es opcional, hay llamadas que no contienen ningún valor.<br/> Cualquier otro valor enviado a través de la variable **API sin cliente**. Por ejemplo, xbox, appletv y roku. |
| ID de usuario de MVPD | Reemplaza la ID de visitante basada en cookies |


## Detalles {#details-int-authn-analyt}

* Las métricas se insertarán, evento por evento, en el grupo de informes específico a través de la API de inserción de datos de Adobe Analytics
* La inserción se envía por lotes cada 30 minutos. Debido a esto, el informe necesita una marca de tiempo
* Cada cliente tendrá uno o varios grupos de informes. Un ID de solicitante (canal) solo se asignará a un grupo de informes. Varios ID de solicitante solo pueden asignarse a un grupo de informes.
* Se pueden proporcionar datos históricos, pero habrá que prestar especial atención debido a problemas de tráfico y rendimiento.
* La variable de visitante único se establece en el ID de usuario de MVPD
* La asignación de eventos y eVars no se puede configurar.


## SLA {#sla-int-authn-serv-anal}

Dado que no es un componente crítico, no existe garantía de SLA para la integración.

## Configuración del grupo de informes {#report-suite-config}

El informe debe tener una marca de tiempo, ya que los eventos se enviarán en lotes.

### Eventos {#report-suite-config-events}


>[!NOTE]
>Todos deben configurarse con:
>
>* Contador (sin subrelaciones)


| Evento | Evento de Adobe Analytics |
|---------------------------------------|-----------------------|
| Se solicitó AuthN | event1 |
| AuthN pendiente | event2 |
| AuthN OK | event3 |
| Se solicitó AuthZ | event4 |
| AuthZ OK | event5 |
| Error de AuthZ | event6 |
| Reproducir solicitud | event7 |
| Error de AuthN | event8 |
| Solicitud de autenticador AuthN sin cliente correcta | event9 |
| Error en la solicitud de autenticador AuthN sin cliente | event10 |
| Error en la solicitud de reproducción | event11 |
| Solicitud de cierre de sesión | event12 |
| Cierre de sesión completado | event13 |
| Error de cierre de sesión | event14 |
| Solicitud de comprobación previa | event15 |
| Error en la comprobación previa | event16 |
| Prevuelo concedido | event17 |
| Comprobación preliminar denegada | event18 |


### eVars {#evars}


>[!NOTE]
>Todos deben configurarse con:
>
>* Asignación: Más reciente (última)
>* Caduca después de: Visita
>* Tipo: Cadena de texto


| Propiedad | eVar |
|-----------------------------------|--------------------------------|
| Canal | eVar1 |
| MVPD | eVar2 |
| Proxy | eVar3 |
| Tipo de SDK | eVar4 |
| Versión del SDK | eVar5 |
| ID de recurso | eVar6 |
| Tipo de error AuthZ | eVar7 |
| Tipo de token | eVar8 |
| Tipo de dispositivo sin cliente | eVar9 |
| ID de usuario de MVPD | visitorID (se realiza automáticamente) |
| ID de usuario de MVPD | eVar10 |
| Tipo de dispositivo | eVar11 |
| Sistema operativo | eVar12 |
| Tipo de hardware principal | eVar13 |
| TTL | eVar14 |
| Tipo de autenticación | eVar15 |
| Versión de la arquitectura del servidor | eVar16 |
| Proveedor de autenticación externa | eVar17 |
| Latencia | eVar18 |
| Id De Visitante | eVar19 |
| Mecanismo SSO | eVar20 |
| Modelo de dispositivo | eVar21 |
| Versión del dispositivo | eVar22 |
| Modelo de hardware del dispositivo | eVar23 |
| Proveedor de hardware de dispositivo | eVar24 |
| Fabricante de hardware de dispositivo | eVar25 |
| Versión de hardware del dispositivo | eVar26 |
| Nombre del SO del dispositivo | eVar27 |
| Familia Device OS | eVar28 |
| Proveedor del SO del dispositivo | eVar29 |
| Versión del SO del dispositivo | eVar30 |
| Nombre del explorador del dispositivo | eVar31 |
| Proveedor del explorador de dispositivos | eVar32 |
| Versión del explorador de dispositivos | eVar33 |
| Tipo de dispositivo normalizado sin cliente | eVar34 |

## Precio {#pricing}

Póngase en contacto con su TAM para obtener más información.
