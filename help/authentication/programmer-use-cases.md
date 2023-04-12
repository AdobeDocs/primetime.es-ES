---
title: Casos de uso de programadores
description: Casos de uso de programadores
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 0%

---


# Casos de uso de programadores {#programmer-use-cases}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#overview}

Este documento resume los casos de uso de integración de programadores admitidos por la autenticación de Adobe Primetime. Puede consultar esta página antes de comenzar un proyecto de integración para ver qué funciones se admiten actualmente.

## Casos de uso {#use-cases}


### Integración básica: Autenticación federada y autorización para una red de un solo canal {#basic-integration}

**Prioridad** - Alto

**Desglose** - Aplicación TVE de marca única de programador con una red de canal alojada dentro de la experiencia

Esto permite a los programadores ofrecer contenido premium, en su propia aplicación TVE* con marca, con una comprobación federada de derechos para el MVPD. El requestorID debe alinearse para que coincida con la marca de la aplicación que proporciona el contenido al visor. En este escenario, existe una relación 1-1 entre el ID del solicitante de autenticación de Adobe Primetime y el ID de recurso que se verifica para la asignación de derechos.

>[!NOTE]
>
>La aplicación TVE se utiliza en este documento para hacer referencia de forma colectiva a los distintos tipos de aplicaciones (aplicaciones web, aplicaciones móviles, etc.) compatible con la autenticación de Adobe Primetime. La siguiente columna Plataformas puede contener detalles sobre plataformas admitidas para casos de uso específicos.

#### Casos de uso específicos (comunes a la mayoría de las integraciones) {#sp-use-cases-basic-int}

| Prioridad | Caso de uso | Descripción | Plataformas | Notas de MVPD |
|:--------:|:-----------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------:|:-----------------------------------------:|
| Alto | Descubrimiento de MVPD desde la aplicación TVE del programador | El usuario comienza en la aplicación TVE con marca del programador y se le solicita que seleccione su proveedor MVPD. | API móvil (SWF/JS) (iOS/Android) sin cliente web (para la segunda pantalla) |  |
| Alto | Autenticación federada desde la aplicación TVE del programador | El usuario comienza en la aplicación TVE con marca del programador y, después de seleccionar su proveedor MVPD, pasa a la página de inicio de sesión de la MVPD para introducir sus credenciales. | Móvil web (SWF/JS) (iOS/Android) |  |
| Alto | Autorización Desde La Aplicación TVE Del Programador | Una vez que el usuario está autenticado, la aplicación TVE del programador puede realizar solicitudes de autorización de canal posterior al MVPD para comprobar el derecho del usuario. Normalmente esto es solo comprobar si la red de canal está en el paquete de suscripción MVPD de los usuarios.                                  En este caso, el ID de solicitante y el ID de recurso coincidirán con 1:1. | Todas las plataformas |  |
| Medio | Cerrar sesión desde la aplicación TVE del programador | Permite al usuario cerrar la sesión y borrar los tokens AuthN/AuthZ de autenticación de Adobe Primetime. En muchos casos, esto también cierra la sesión del usuario desde el MVPD. Sin embargo, los MVPD varían en cuanto a si se admite o no. Siempre borra la sesión de autenticación de Adobe Primetime y los tokens. | Todas las plataformas excepto XBox Native | Varios MVPD no admiten esto. |
| Alto | Inicio de sesión único en sitios y aplicaciones | Permite al usuario compartir la sesión de inicio de sesión entre sitios y aplicaciones sin necesidad de iniciar sesión de nuevo. | Todas las plataformas excepto la API sin cliente | Requiere al menos SDK 1.7 para algunos MVPD. |

### Una sola aplicación TVE que hospeda varias redes de canales {#single-app-multi-channel}

**Prioridad**- Alto

Permite al programador agregar varias redes de canales de contenido en el mismo destino de marca para sus visualizadores.

#### Casos de uso específicos {#sp-use-cases-singl-tve-app}

| Prioridad | Caso de uso | Descripción | Plataformas | Notas de MVPD |
|--------|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Alto | Autorización de canal diferente | El usuario puede ver contenido de varias redes de canales dentro de la misma aplicación TVE. El programador puede realizar llamadas de autorización específicas a cada red de canales para confirmar la asignación de derechos de los usuarios. | Todas las plataformas | Todos los MVPD ahora lo admiten de alguna forma. |
| Bajo | Consulta de autorización de comprobación previa | Esto permite al programador comprobar qué canales tiene el usuario en su paquete en una sola llamada de API. Esto se hace antes de las llamadas AuthZ reales para filtrar contenido desde la interfaz de usuario a la que el usuario no tiene acceso. |  | La mayoría de los MVPD aún no exponen estos datos como Atributos del usuario, por lo que Adobe hace llamadas AuthZ para obtenerlos. Además, la mayoría de los MVPD están limitados a 5 a la vez, ya que no admiten varios canales en una sola llamada.                             Es muy importante verificar cuántos canales necesita el programador para la comprobación previa. Independientemente del número, tendremos que comprobar que está bien con los MVPD. Actualmente, la mayoría de los MVPD no admiten más de 5 canales (tercer trimestre de 2013). |

### Autorización de nivel de recurso {#asset-level-authz}

**Prioridad** - Bajo

**Desglose** - Pasar Un Identificador De Recurso En Una Solicitud De Autorización

**Plataformas** - Todas las plataformas

#### Casos de uso específicos {#sp-use-cases-asset-lvl-authz}

Permite que el MVPD obtenga análisis de nivel de recurso en cada llamada a AuthZ. Esto tiene la desventaja de negar la caché AuthZ de autenticación de Adobe Primetime.

| Prioridad | Caso de uso | Descripción | Plataformas | Notas de MVPD |
|--------|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|-------------|--------------------------------------|
| Bajo | Pasar un identificador de recurso en una solicitud de autorización | Permite que el MVPD obtenga análisis de nivel de recurso en cada llamada a AuthZ.  Tiene el inconveniente de negar la caché AuthZ de autenticación de Adobe Primetime. | Todas las plataformas | Actualmente, solo un MVPD lo admite. |




### Controles parentales {#parental-controls}

**Prioridad** - Bajo

Permite aplicar restricciones de cuenta de usuario de MVPD en la aplicación TVE del programador.

| Prioridad | Caso de uso | Descripción | Plataformas | Notas de MVPD |
|--------|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|-----------------------------------|
| Bajo | Filtrar contenido en función de los atributos de usuario | Permite al programador comprobar la clasificación máxima permitida para un usuario antes de procesar la lista de contenido disponible para el usuario. | Móvil web (Flash/JS) (iOS/Android) | Actualmente solo funciona con un MVPD. |
| Bajo | Pasar clasificaciones de contenido en la solicitud AuthZ | Permite al programador pasar la clasificación específica del contenido que el usuario desea ver como parte de la solicitud AuthZ a MVPD Relacionado con el número 3, ya que las clasificaciones generalmente se encuentran en el nivel de recursos. | Todas las plataformas | Actualmente solo funciona con un MVPD. |

#### Personalización de la integración de MVPD por programador marca {#mvpd-int-cust-prog-brand}

**Prioridad** - Medio

Habilita la experiencia personalizada durante AuthN o para mensajes de error AuthZ.

| Prioridad | Caso de uso | Descripción | Plataformas | Notas de MVPD |
|--------|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------------------------------------|
| Medio | Pase el identificador del proveedor de servicios en la solicitud AuthN. | Habilite la promoción de una marca específica en la página de inicio de sesión de MVPD específica del proveedor de servicios. Habilite también la selección automática del valor predeterminado para que coincida con la audiencia, como español para Univision. | Todas las plataformas | Varía por MVPD. Algunos no lo admiten. |
| Medio | Mensajes de error personalizados en la respuesta de AuthZ | Habilita los mensajes de error específicos de programador o marca de MVPD que pueden incluir un mensaje específico para la mejora de ventas con un enlace que actualiza el paquete. | Web, Android, iOS | Varía por MVPD. Algunos no lo admiten. |


### Casos de uso de dispositivos conectados {#connected-devices}

| Prioridad | Caso de uso | Descripción | Plataformas | Notas de MVPD |
|--------|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Medio | XBox LiveID SSO en varias aplicaciones y consolas | Permite al usuario compartir sesión de AuthN entre aplicaciones y entre distintas consolas de juegos, vinculadas a su cuenta de LiveID. | SDK nativo de XBox | A la mayoría de los MVPD no les gusta esto porque el modelo típico es enlazar el token al dispositivo, no al usuario.                             Ya no recomendamos este enfoque si es posible. |
| Alto | Dispositivo conectado con tokens enlazados al appID en el dispositivo | Permite al programador enlazar el derecho de MVPD en el token al appID del dispositivo al que se emitió. | API sin cliente | Esto alinea el dispositivo conectado más estrechamente con la implementación de pase estándar para los tokens.                             Sigue siendo necesario mejorar para que sea un ID de todo el dispositivo. |

### Longitud TTL AuthN específica del dispositivo {#authn-ttl-length}

Habilite la asignación TVE para eventos especiales que pueden no ser recursos que estén en la base de datos de autorizaciones de MVPD como canales normales.

| Prioridad | Caso de uso | Descripción | Plataformas | Notas de MVPD |
|--------|------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|--------------------------------------------------------------------------------------------------------------------------|
| Alto | Definir diferentes valores de TTL por plataforma | Permite al programador establecer una longitud TTL diferente para dispositivos web, móviles y conectados. Actualmente, la autenticación de Adobe Primetime admite la capacidad de tener 3 valores TTL independientes: Web (Flash) Móvil/HTML5 Clientless - Dispositivos conectados |  | Algunos MVPD establecen el TTL de forma dinámica. Adobe puede anular estos ajustes dinámicos si es necesario, utilizando los ajustes de configuración. |

### Aplicaciones especiales basadas en eventos {#special-event}

**Prioridad** - Bajo

Habilite la asignación TVE para eventos especiales que pueden no ser recursos que estén en la base de datos de autorizaciones de MVPD como canales normales.

| Prioridad | Caso de uso | Descripción | Plataformas | Notas de MVPD |
|--------|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|------------------------------------------|
| Bajo | Varios canales como proxy para un evento | Esto se hizo para las Olimpiadas, donde el suscriptor necesitaba tener dos canales diferentes en su paquete para tener acceso. En este caso, la autenticación de Adobe Primetime creó un nuevo resourceID y hizo que todos los MVPD hicieran la asignación a los canales específicos de su extremo.  Eso funcionó bien con suficiente antelación. Esto era importante porque la mayoría de los MVPD no admiten varias llamadas de recursos. | Todas las plataformas | Admitido por todos los MVPD con el debido aviso. |
| Bajo | Aplicación de evento nuevo especial, uso de recursos de canal existentes | Esto se hizo para March Madness. El proveedor de contenido creó una aplicación nueva con un requestorID nuevo. Todos los MVPD necesitaban añadir compatibilidad con el nuevo requestorID en su sistema. Los resourceIDs eran canales normales.  Algunos MVPD también necesitaban asignar los canales como válidos bajo el nuevo solicitante, por lo que se necesitaba más tiempo para esos casos. | Todas las plataformas | Admitido por todos los MVPD con el debido aviso. |
| Bajo | RequestorID existente, resourceID | Esto se hizo para el torneo del fin de semana de golf Masters. Fue solo un pequeño evento durante un par de días, y los Maestros tuvieron su propia aplicación móvil que estuvo bien para mostrar el contenido. El programador planeaba pagar por el tráfico de autenticación de Adobe Primetime y usar simplemente su requestorID y resourceID estándar. El único truco fue hacer que el programador comparta un certificado móvil para la firma requestorID con los maestros, y que lo añadan a su configuración como certificado de respaldo para ese fin de semana. | Todas las plataformas | Sin impacto para los MVPD |

### Integración del servidor de contenido {#content-server-integration}

**Prioridad**- Medio

Habilitación de la validación del token de medios antes de lanzar el flujo de vídeo al reproductor cliente.
| Prioridad | Caso de uso | Descripción | Plataformas | Notas de MVPD | |—|—|—|—|—| | Alto | Reproductor federado de programadores - Con autorización de nivel de página | Las API de autenticación de Adobe Primetime se realizan en JavaScript en la página y el token se pasa al reproductor. El token se puede pasar al servicio de validación de un par de formas: Obtenga parámetro en el parámetro de URL del servicio de validación que se pasa en la cadena de consulta de la URL de flujo API de interfaz externa FlashVars | | | | Medio | Programador Federated Player - Con Autorización Interna Del Reproductor | Las API de autenticación de Adobe Primetime se realizan en ActionScript en el SWF del reproductor, por lo que el token está disponible para el reproductor desde la rellamada.                                                                                                                                                                                         | | | | Alto | Reproductor sindicado: alojado en el portal MVPD con autorización de nivel de página utilizando un iFrame para envolver el reproductor | Similar al reproductor con autorización de nivel de página, pero con el envoltorio de páginas del reproductor iFramed en el portal MVPD. La autenticación debe realizarse por separado en el portal MVPD.                                                                                                                                                    |           |                        |


<!--
>[!RELATEDINFORMATION]
>
>* MVPD Integration Features
>* Entitlement Flow
>* Platform / Device Requirements
-->
