---
title: Funciones de integración de MVPD
description: Funciones de integración de MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 2%

---


# Funciones de integración de MVPD

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#mvpd-int-features-overview}

La autenticación de Adobe Primetime admite los estándares emergentes para TV en todas partes. Cumple con la **Especificación de CableLabs OLCA (Acceso a contenido en línea)**, que proporciona requisitos técnicos y arquitectura para la entrega de vídeo a un cliente de televisión de pago desde fuentes en línea. Adobe participó en el proyecto conjunto de pruebas de interconexión de CableLabs en junio de 2011 y aprobó el proceso de prueba para la implementación de un proveedor de servicios.  Adobe también es miembro activo de **OATC (Open Authentication Technical Consortium)** y participa en varios de los proyectos de elaboración de especificaciones de los subcomités como parte de ese órgano.

Tras haber descrito el cumplimiento de la autenticación de Primetime OLCA, y la participación del Adobe en OATC, también es importante señalar que la autenticación de Primetime es en realidad &quot;independiente del protocolo&quot;.  Pero en esta etapa de la era TVE, la autenticación de Primetime definitivamente está orientada hacia los estándares OLCA.  Las normas definen las formas convenidas actualmente para que los diferentes reproductores de TVE (programadores, MVPD y proveedores de servicios) implementen las funciones de TVE. Muchas de estas funciones se enumeran en las tablas siguientes, con vínculos a páginas relacionadas que proporcionan detalles y ejemplos de cómo implementar las funciones.

La información de las tablas pretende impulsar el proceso de integración de autenticación de Primetime hacia una funcionalidad coherente en todas las integraciones de MVPD. La columna de prioridad clasifica las funciones en A, B y C:

* R: Son funciones que &quot;deben tener&quot; para la implementación inicial de una integración.
* B: Estas son mejoras importantes en la integración inicial que se agregarán después de la implementación inicial.
* C: Estas son mejoras adicionales para la integración que se pueden implementar después de los requisitos &quot;B&quot;.


## 1. Funciones principales {#core-func-features}


| No. | Función | Descripción | Prioridad | Notas |
|------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1.1 | [Inicio de sesión iniciado por el programador](/help/authentication/authn-oauth2-protocol.md) | El visor selecciona el MVPD e inicia el flujo de autenticación (AuthN) desde el sitio web o la aplicación de la marca del programador. | A+ |  |
| 1.2 | [Autorización basada en canales](/help/authentication/authz-usecase.md) | Una vez autenticada, la autorización (AuthZ) puede producirse en segundo plano, con el paso de un identificador de canal de red y un identificador de usuario al MVPD. | A+ |  |
| 1.3 | Persistencia de UserID | El MVPD proporciona un UserID ofuscado y persistente. | A |  |
| 1.4 | [Compatibilidad con inicio de sesión único](/help/authentication/sso-support.md) | El visor inicia sesión con el MVPD en el sitio de una marca y luego puede ir a otra marca y no se le pedirá que vuelva a iniciarla. La sesión de AuthN se comparte entre las marcas. La compatibilidad con SSO es tanto para sitios web como para aplicaciones móviles/de dispositivos.  Para los MVPD, es necesario devolver un ID de usuario o algún otro token de usuario que se pueda usar para AuthZ entre marcas. | A |  |
| 1.5 | Experiencia del usuario de inicio de sesión optimizada para dispositivos (UX) | El MVPD admite el cambio de tamaño de la pantalla de inicio de sesión para que se ajuste a las dimensiones del dispositivo que utiliza la vista. | A |  |
| 1.6 | Logotipo predeterminado del selector de MVPD | El MVPD proporciona una URL a un logotipo predeterminado de dimensiones adecuadas (112x33 píxeles). | A | El logotipo debe ser alojado por el MVPD y debe ser almacenado en caché por CDN. |
| 1.7 | [Ámbitos del proveedor de servicios](/help/authentication/serv-provider-scoping.md) | MVPD admite pasar el identificador de marca (valor del solicitante) en la solicitud AuthN. | A- | Esto habilita una experiencia de inicio de sesión específica del proveedor de servicios. |
| 1.8 | [Autorización de varios canales](/help/authentication/mvpd-preflight-authz.md#preflight-multich-authz) | El MVPD es compatible con un programador que envía varios canales en una única solicitud de autorización. | B+ |  |
| 1.9 | Autenticación basada en iFrame o &quot;JS Pop-up&quot; | El programador puede integrar el flujo de inicio de sesión en una experiencia de iFrame o de ventana emergente en lugar de en un redireccionamiento HTTP. | B |  |
| 1.10 | [Cierre de sesión iniciado por el programador](/help/authentication/usecase-mvpd-logout.md) | El visor tiene una sesión autenticada tanto en el sitio o la aplicación del programador como con el MVPD. El usuario puede iniciar un cierre de sesión federado desde el sitio del programador, y el cierre de sesión también borra la sesión en el portal de MVPD. | B | Garantiza que los ordenadores compartidos estén más protegidos contra el uso indebido desde la perspectiva del programador. |
| 1.11 | [Mensajería de error de autorización personalizada](/help/authentication/error-reporting.md) | El MVPD pasa su propia cadena de error personalizada, que es apropiada para que el Sitio o la Aplicación Federados del Programador se muestre al usuario. | B | Permite situaciones de venta ascendente |
| 1.12 | **Metadatos de usuario de la respuesta de autenticación** | La respuesta MVPD AuthN puede incluir metadatos de usuario que actúan como indicio de personalización de la experiencia del usuario durante el flujo de derechos. Este requisito permite recibir sugerencias de control paterno desde el MVPD hasta el Programador. | B- |  |
| 1.13 | Autenticación iniciada por MVPD | El visor completa una sesión AuthN correcta en el portal MVPD y luego navega al sitio TVE del programador. No se solicita al usuario el selector de MVPD y se autentica automáticamente. | B- |  |
| 1.14 | Creación de ámbitos de UserID | El UserID de MVPD debe presentarse en dos formularios: uno para los programadores y otro para todo el Adobe para el fraude.  Esto permite que Adobe comparta el UserID de MVPD con alcance de programador sin necesidad de encriptar/ofuscar más. | C |  |
| 1.15 | Autorización basada en activos | Una vez completado el AuthN, el AuthZ se puede producir en segundo plano, pasando datos estructurados que pueden incluir red, programa, recurso, clasificación de control parental y más según sea necesario. Esto permite el control parental en cada llamada de AuthZ del programador al MVPD. | C |  |
| 1.16 | Cierre de sesión iniciado por MVPD | El visor tiene una sesión autenticada tanto en el sitio o la aplicación del programador como con el MVPD. El usuario puede iniciar un cierre de sesión federado desde el sitio de MVPD que también borra la sesión en todos los sitios de programadores federados. | C |  |
| 1.17 | Obligaciones de autorización | El MVPD proporciona condiciones adicionales en la respuesta de AuthZ, como el registro, o una clasificación de control paterno máxima actualizada (OLCA). | C |  |
| 1.18 | Contexto de dirección IP | El MVPD requiere pasar explícitamente la dirección IP. Para AuthZ, donde las llamadas son del lado del servidor, esto proporciona al MVPD información de seguimiento del fraude sobre de dónde viene el usuario en la llamada AuthZ. | C |  |
| 1.19 | Valor de tiempo de vida de persistencia de tokens (TTL) definido dinámicamente | El MVPD puede establecer el TTL del token de autenticación de Primetime de forma dinámica a través de las propiedades de la respuesta, de modo que el Adobe esté fuera del bucle para los cambios del TTL. | C- |  |
| 1.20 | Tipo de dispositivo | El MVPD admite pasar el tipo de dispositivo en la solicitud AuthN o AuthZ. Esta propiedad informa al MVPD sobre la naturaleza del dispositivo en el que se consumirá el contenido, de modo que puedan ajustar el TTL del token AuthN o AuthZ para que se ajuste a sus propias consideraciones de seguridad para el dispositivo. | C- | Esto es útil para la plataforma sin clientes, donde puede ser difícil exponer cada tipo de dispositivo como una configuración en el lado de autenticación de Primetime. |



## 2. Características operacionales {#operational-features}

| No | Función | Descripción | Prioridad | Notas |
|-----|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|-------|
| 2.1 | Tiempo de actividad 24 horas al día, 7 días a la semana | Un acuerdo de MVPD para esforzarse por un tiempo y una medida ininterrumpidos frente a eso con el paso del tiempo. | A |  |
| 2.2 | Credenciales De Prueba Para Cada Programador | El MVPD proporciona cuentas de prueba independientes para cada programador. | A |  |
| 2.3 | Caducidad del certificado y plan de programación de renovación | Un plan documentado por MVPD con una programación para garantizar que los certificados SAML estén actualizados. | A- |  |
| 2.4 | Latencia Media Menor De 250 Ms/Respuesta | Un acuerdo de MVPD para luchar por una baja latencia, y para medirla contra eso con el tiempo. | A- |  |
| 2.5 | Logotipo del selector de MVPD propio | El MVPD necesita alojar su propio logotipo y debe estar protegido por el almacenamiento en caché de la CDN. | B |  |
| 2.6 | Plan de escalación de soporte | Un plan de escalación documentado por MVPD que se mantiene actualizado y se revisa al menos trimestralmente. | A |  |
| 2.7 | Plan de protección contra interrupciones | Un plan conjunto de MVPD con Adobes sobre las medidas de degradación que pueden utilizarse en general según sea necesario. | B |  |
| 2.8 | Mantener puntos de conexión de ensayo y producción separados | Una prueba de integración de MVPD que no requiere simulación de archivos de host para probar la integración de ensayo. | B |  |
| 2.9 | Punto final de control de calidad adicional | El MVPD mantiene una integración de IDP de control de calidad adicional para el desarrollo conjunto de nuevas funciones.  Si se admite esto, sería menos probable que necesitáramos solicitudes especiales de UAT para probar los certificados de la tienda de aplicaciones. | C |  |





## 3. Funciones de la experiencia de autenticación {#authn-exp-features}


| No | Función | Descripción | Prioridad | Notas |
|-----|----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| 3.1 | Conversión de autenticación sobre expectativa mínima | El MVPD garantiza una tasa de conversión mínima para demostrar su funcionalidad (5%) y razonable (30%). | A |  |
| 3.2 | Recuperación de contraseña en línea | El MVPD proporciona un medio para recuperar contraseñas en línea con el flujo federado AuthN. | A |  |
| 3.3 | Registro de cuentas en línea | El MVPD proporciona un medio para crear una nueva cuenta en línea con el flujo federado de AuthN. | A |  |
| 3.4 | Ayuda/asistencia en línea | El MVPD proporciona un medio para proporcionar ayuda durante el flujo federado de AuthN. | A |  |
| 3.5 | Autenticación interna basada en módem | El MVPD autentica automáticamente un dispositivo cuando está en la red local de un modelo registrado (solo MVPD ISP). | B | Esto es de menor prioridad porque es una optimización que muchos aún no pueden apoyar e introduce algunos desafíos para la mitigación del fraude y los controles parentales |
Ahora puede importar el código de la tabla Markdown directamente mediante el cuadro de diálogo File/Paste table data... .



## 4. Funciones de Analytics {#analytics-features}


| No | Función | Descripción | Prioridad |
|-----|--------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| 4.1 | Alineación del canal de conversión de autenticación | El MVPD tiene una métrica para las solicitudes AuthN que comienza con la solicitud SAML AuthN - para alinearse con las métricas de autenticación de Primetime y de solicitud AuthN del programador. | A |
| 4.2 | Usuarios únicos | Usuarios que se han autenticado correctamente y se han deduplicado en un resumen mensual a lo largo de los días. | A |
| 4.3 | Contabilidad de zona horaria | Los informes incluyen una zona horaria para el momento en que se cambia el día. | A |





## 5. Funciones de mitigación del fraude {#fraud-mitgn-features}


| No | Función | Descripción | Prioridad | Notas |
|-----|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------------|
| 5.1 | Validación del suscriptor de vídeo en la autenticación | El MVPD garantiza que el usuario sea un suscriptor de vídeo válido durante el flujo AuthN. | A |  |
| 5.2 | Límite de tasas para autenticación/autorización | El MVPD admite la restricción en sus servicios web para limitar el uso de una cuenta de usuario específica cuando sea apropiado. | B |  |
| 5.3 | UserID persistente con ámbito global para el Adobe | El MVPD garantiza que el Adobe tenga un UserID que se pueda rastrear entre los programadores por fraude. Esto no necesita proporcionarse directamente al cliente. | B | Especificación del Protocolo de autorización multimedia en línea (OMAP) y Monitorización del usuario real (RUM). |
| 5.4 | Validación de uso concurrente | El MVPD tiene un medio para rastrear y limitar el uso simultáneo de la cuenta del suscriptor más allá de un umbral comercial. | B |  |

## P1. Funciones específicas del proxy {#proxy-sp-func-features}

| No | Descripción | Prioridad | Notas |
|-------|--------------------------------------------------------------------------------|----------|---------------------------------------------------|
| P 1.1 | Proxy responsable de mantener la precisión de la lista actualizada de subMVPD | A |  |
| P 1.2 | Proxy ofrece un logotipo de tamaño apropiado para cada subMVPD | A | Algunos subMVPD en directo no tienen el tamaño del logotipo correcto |
| P 1.3 | El proxy ofrece una página de inicio de sesión con marca adecuada para cada sub-MVPD | A |  |
| P 1.4 | Proxy responsable de dirigir a marcas específicas de proveedores de servicios con la lista sub-MVPD | B |  |
| P 1.5 | Proxy especifica correctamente todas las propiedades subMVPD (tamaño de iFrame, TTL, logotipo, etc.) | A |  |
| P 1.6 | Proxy especifica entityID independiente | B |  |

## P2. Funciones operativas proxy {#proxy-op-features}

| No | Descripción | Prioridad |
|-------|----------------------------------------------------------------------------------------|----------|
| P 2.1 | La clave de API está segura | A |
| P 2.2 | Credenciales de prueba para el primer subMVPD utilizado en la integración activa para cada nuevo solicitante | A |
| P 2.3 | Las listas subMVPD son exactas y completas por solicitante | A |
