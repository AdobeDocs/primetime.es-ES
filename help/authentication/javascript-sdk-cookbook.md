---
title: Guía del SDK para JavaScript
description: Guía del SDK para JavaScript
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# Guía del SDK para JavaScript {#javascript-sdk-cookbook}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

## Introducción {#intro}

En este documento se describen los flujos de trabajo de derechos que implementa la aplicación de nivel superior de un programador para una integración de JavaScript con el servicio de autenticación de Adobe Primetime. Los vínculos a la Referencia de la API de JavaScript se incluyen en.

Tenga en cuenta también que la variable [Información relacionada](#related) Esta sección incluye un vínculo a un conjunto de ejemplos de código JavaScript.

## Flujos de derecho {#entitlement}

1. [Requisitos previos](#prereq)
2. [Flujo de inicio](#startup)
3. [Flujo de autenticación](#authn)
4. [Flujo de autorización](#authz)
5. [Ver flujo de medios](#logout)

</br>

![](assets/javascript-flows.png)


## Requisitos previos {#prereq}

**Dependencias:**

- Biblioteca de autenticación de Adobe Primetime (AccessEnabler), colabore con el administrador de cuentas de autenticación de Adobe Primetime para organizarlo.
- ID de solicitante de autenticación de Adobe Primetime válido, colabore con el administrador de cuentas de autenticación de Adobe Primetime para organizarlo.

Cree sus funciones de devolución de llamada:

- `entitlementLoaded`
</br>

**Déclencheur:** AccessEnabler se ha cargado y terminado de inicializar.

- `displayProviderDialog(mvpds)`

  **Déclencheur:** `getAuthentication(),` sólo si el usuario no ha seleccionado ningún proveedor (una MVPD) y aún no está autenticado. El parámetro mvpds es una matriz de proveedores disponibles para el usuario.

- `setAuthenticationStatus(status, errorcode)`

  **Déclencheur:**
   - `checkAuthentication()`cada vez.
   - `getAuthentication()` solo si el usuario ya se ha autenticado y ha seleccionado un proveedor.

  El estado devuelto es éxito o error; el código de error describe el tipo de error.

- `createIFrame(width, height)`

  **Déclencheur:** `setSelectedProvider(providerID)`, solo si el proveedor seleccionado está configurado para mostrarse en un IFrame.

  >[!NOTE]
  >
  >Un proveedor está configurado para procesar su pantalla de autenticación como redireccionamiento o en un iFrame, y el programador debe tener en cuenta ambos.

- `sendTrackingData(event, data)`

  **Déclencheur:** `checkAuthentication(), getAuthentication(),checkAuthorization(), getAuthorization(), setSelectedProvider()`.  El `event` indica qué evento de asignación de derechos se produjo; el parámetro `data` parámetro es una lista de valores relacionados con el evento.
- `setToken(token, resource)`
  **Déclencheur:** `checkAuthorization()`y `getAuthorization()` después de una autorización correcta para ver un recurso.   El `token` parámetro es el token de medios de corta duración; el `resource` parámetro es el contenido que el usuario tiene autorización para ver.

- `tokenRequestFailed(resource, code, description)`
  **Déclencheur:**`checkAuthorization()` y`getAuthorization()`  después de una autorización fallida.\
  El `resource` parámetro es el contenido que el usuario intentaba ver; la variable `code` parámetro es el código de error que indica qué tipo de error se produjo; la variable `description` describe el error asociado con el código de error.

- `selectedProvider(mvpd)`

  **Déclencheur:** [`getSelectedProvider()`](#$getSelProv El `mvpd` proporciona información sobre el proveedor seleccionado por el usuario.

- `setMetadataStatus(metadata, key, arguments)`

  **Déclencheur:** `getMetadata().`\
  El `metadata` proporciona los datos específicos solicitados; el parámetro clave es la clave utilizada en el `getMetadata()`solicitud; y la `arguments` El parámetro es el mismo diccionario que se pasó a `getMetadata()`.


## 2. Flujo de inicio

**I. Cargue el JavaScript de AccessEnabler:**

**Para el perfil de ensayo**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth-staging.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"
```

o...

**Para el perfil de producción**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"
```

**Déclencheur:** Una vez finalizada la inicialización, la autenticación de Adobe Primetime llama a su `entitlementLoaded()` función de llamada de retorno. Este es el punto de entrada a la comunicación de la aplicación con AccessEnabler.


**II.** Llamada `setRequestor()`para establecer la identidad del Programador; pase en el `requestorID` y (opcionalmente) una matriz de puntos finales de autenticación de Adobe Primetime.

**Déclencheur:** Ninguno, pero habilita `displayProviderDialog()` para que se le llame cuando sea necesario.


**III.** Llamada `checkAuthentication()` para buscar una autenticación existente sin iniciar el [flujo de autenticación].  Si esta llamada se realiza correctamente, puede continuar directamente a la `authorization flow`.  Si no es así, continúe con el `authentication flow`.

**Dependencia:** Una llamada a correcta a `setRequestor()`(esta dependencia también se aplica a todas las llamadas subsiguientes).

**Déclencheur:** `setAuthenticationStatus()` callback

</br>

## 3. Flujo de autenticación</span>


**Dependencia:** Una llamada a correcta a `setRequestor()`(esta dependencia también se aplica a todas las llamadas subsiguientes).


Llamada `getAuthentication()` para obtener el estado de autenticación O para almacenar en déclencheur el flujo de autenticación del proveedor.

**Activadores:**

- `displayProviderDialog()`si el usuario aún no se ha autenticado
- `setAuthenticationStatus()` si la autenticación ya se ha realizado

Se llega a la finalización del flujo de autenticación cuando AccessEnabler llama a `setAuthenticationStatus()`con `isAuthenticated == 1`.

## 4. Flujo de autorización {#authz}

**Dependencias:**

- Una llamada a correcta a `setRequestor()` (esta dependencia también se aplica a todas las llamadas subsiguientes).
- ResourceID(s) válidos acordados con los MVPD. Tenga en cuenta que los ResourceID deben ser los mismos que se usan en cualquier otro dispositivo o plataforma, y serán los mismos en todas las MVPD.

Llamada `getAuthorization()` y pase el ResourceID para los medios solicitados. Una llamada correcta devolverá un token de medios corto, que confirma que el usuario está autorizado para ver los medios solicitados.

- Si la llamada pasa: El usuario tiene un token de AuthN válido y está autorizado para ver el contenido solicitado.
- Si la llamada falla: Examine la excepción producida para determinar su tipo (AuthN, AuthZ o algo más):
- Si la llamada fue un error de AuthN, reinicie el flujo de AuthN.
- Si la llamada fue un error de AuthZ, el usuario no tiene autorización para ver el contenido solicitado y se debe mostrar algún tipo de mensaje de error al usuario.
- Si hubo algún otro error (error de conexión, error de red, etc.) a continuación, mostrar un mensaje de error apropiado al usuario.

Utilice el verificador de tokens de medios para validar el shortMediaToken devuelto por un correcto `getAuthorization()` llamada.


**Dependencia:** El Comprobador de tokens de medios cortos (incluido en la biblioteca AccessEnabler)

- Si se supera la validación: mostrar/reproducir el medio solicitado para el usuario.
- Si falla: El token de AuthZ no era válido, la solicitud de medios debe rechazarse y se debe mostrar un mensaje de error al usuario.

## 5. Ver flujo de medios {#logout}

- El usuario selecciona los medios que desea ver.
   - ¿Están protegidos los medios?
      - La aplicación comprueba si los medios están protegidos:
         - Si el medio está protegido, la aplicación inicia el flujo de autorización (AuthZ) anterior.
         - Si los medios no están protegidos, continúe con el flujo de Ver medios.
         - Medios de reproducción

## Configuración del ID de visitante {#visitorID}

Configuración de un [Experience Cloud visitorID](https://experienceleague.adobe.com/docs/id-service/using/home.html) El valor de es muy importante desde el punto de vista del análisis. Una vez establecido un valor EC visitorID, el SDK enviará esta información junto con cada llamada de red y el servicio de autenticación de Adobe Primetime recopilará esta información. De este modo, podrá correlacionar los datos de análisis del servicio de autenticación de Adobe Primetime con cualquier otro informe de análisis que pueda tener de otras aplicaciones o sitios web. Se puede encontrar información sobre cómo configurar el ID de visitante de EC [aquí](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=en).


>[!NOTE]
>
>Tenga en cuenta que esta compatibilidad con la funcionalidad está disponible a partir de la versión 3.1.0 del SDK de JS.

<!--
### Related Information (#related)

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK API Reference](/help/authentication/javascript-sdk-api-reference.md)
* **JavaScript SDK Code Samples**
-->
