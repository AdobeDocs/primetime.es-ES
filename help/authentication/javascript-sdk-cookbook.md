---
title: Guía de SDK para JavaScript
description: Guía de SDK para JavaScript
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---


# Guía de SDK para JavaScript {#javascript-sdk-cookbook}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción (#intro)

En este documento se describen los flujos de trabajo de asignación de derechos que implementa la aplicación de nivel superior de un programador para una integración de JavaScript con el servicio de autenticación de Adobe Primetime. Los vínculos a la referencia de la API de JavaScript se incluyen en todas las secciones.

Tenga en cuenta también que la variable [Información relacionada](#related) incluye un vínculo a un conjunto de ejemplos de código JavaScript.

## Flujos de derechos (#rights)

1. [Requisitos previos](#prereq)
2. [Flujo de inicio](#startup)
3. [Flujo de autenticación](#authn)
4. [Flujo de autorización](#authz)
5. [Ver flujo de medios](#logout)

</br>

![](assets/javascript-flows.png)


## Requisitos previos(#preereq)

**Dependencias:**

- Biblioteca de autenticación de Adobe Primetime (AccessEnabler), trabaje con el administrador de cuentas de autenticación de Adobe Primetime para arreglarlo.
- requestorId de autenticación válida de Adobe Primetime, trabaje con el administrador de cuentas de autenticación de Adobe Primetime para solucionarlo.

Cree sus funciones de llamada de retorno:

- `entitlementLoaded`

</br>

**Déclencheur:** AccessEnabler se ha cargado y ha finalizado la inicialización.

- `displayProviderDialog(mvpds)`

   **Déclencheur:** `getAuthentication(),` solo si el usuario no ha seleccionado un proveedor (un MVPD) y aún no está autenticado El parámetro mvpds es una matriz de proveedores disponibles para el usuario.

- `setAuthenticationStatus(status, errorcode)`

   **Déclencheur:**
   - `checkAuthentication()`cada vez.
   - `getAuthentication()` solo si el usuario ya está autenticado y ha seleccionado un proveedor.

   El estado devuelto es correcto o fallido; el código de error describe el tipo de error.

- `createIFrame(width, height)`

   **Déclencheur:** `setSelectedProvider(providerID)`, solo si el proveedor seleccionado está configurado para mostrarse en un IFrame.

   >[!NOTE]
   >
   >Un proveedor está configurado para representar su pantalla de autenticación como redireccionamiento o en un iFrame, y el programador debe tener en cuenta ambos.

- `sendTrackingData(event, data)`

   **Déclencheur:** `checkAuthentication(), getAuthentication(),checkAuthorization(), getAuthorization(), setSelectedProvider()`.  La variable `event` indica qué evento de asignación de derechos se ha producido; el `data` es una lista de valores relacionados con el evento. 
- `setToken(token, resource)`

   **Déclencheur:** `checkAuthorization()`y `getAuthorization()` después de una autorización correcta para ver un recurso.   La variable `token` es el token de contenido breve; el `resource` es el contenido que el usuario está autorizado a ver.

- `tokenRequestFailed(resource, code, description)`

   **Déclencheur:**`checkAuthorization()` y`getAuthorization()`  después de una autorización incorrecta.\
   La variable `resource` es el contenido que el usuario estaba intentando ver; el `code` es el código de error que indica qué tipo de error se ha producido; el `description` describe el error asociado al código de error.

- `selectedProvider(mvpd)`

   **Déclencheur:** [`getSelectedProvider()`](#$getSelProv El `mvpd` proporciona información sobre el proveedor seleccionado por el usuario.

- `setMetadataStatus(metadata, key, arguments)`

   **Déclencheur:** `getMetadata().`\
   La variable `metadata` proporciona los datos específicos solicitados; el parámetro key es la clave utilizada en la variable `getMetadata()`solicitud; y `arguments` es el mismo diccionario que se pasó a `getMetadata()`.


## 2. Flujo de inicio

**I. Carga del JavaScript de AccessEnabler:**

**Para el perfil de ensayo**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth-staging.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"
```

o...

**Para perfil de producción**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"
```

**Déclencheur:** Cuando se completa la inicialización, la autenticación de Adobe Primetime llama a su `entitlementLoaded()` función de llamada de retorno. Este es el punto de entrada a la comunicación de su aplicación con AccessEnabler. 

 
**II.** La llamada `setRequestor()`establecer la identidad del programador; pase en el `requestorID` y (opcionalmente) una matriz de extremos de autenticación de Adobe Primetime.

**Déclencheur:** Ninguno, pero habilita `displayProviderDialog()` cuando sea necesario.


**III.** La llamada `checkAuthentication()` para comprobar si hay una autenticación existente sin iniciar la [flujo de autenticación].  Si esta llamada se realiza correctamente, puede continuar directamente con el `authorization flow`.  Si no es así, vaya a la `authentication flow`.

**Dependencia:** Una llamada correcta a `setRequestor()`(esta dependencia también se aplica a todas las llamadas posteriores).

 **Déclencheur:** `setAuthenticationStatus()` callback

</br>

## 3. Flujo de autenticación</span>


**Dependencia:** Una llamada correcta a `setRequestor()`(esta dependencia también se aplica a todas las llamadas posteriores).


La llamada `getAuthentication()` para obtener el estado de autenticación O para almacenar en déclencheur el flujo de autenticación del proveedor.

**Activadores:**

- `displayProviderDialog()`si el usuario aún no se ha autenticado
- `setAuthenticationStatus()` si la autenticación ya se ha realizado

Se llega a la finalización del flujo de autenticación cuando AccessEnabler llama a `setAuthenticationStatus()`con `isAuthenticated == 1`.

## 4. Flujo de autorización (#authz)

**Dependencias:**

- Una llamada correcta a `setRequestor()` (esta dependencia también se aplica a todas las llamadas posteriores).
- ResourceID(s) válidos acordados con los MVPD(s). Tenga en cuenta que los ID de recursos deben ser los mismos que los utilizados en cualquier otro dispositivo o plataforma, y serán los mismos en todos los MVPD.

La llamada `getAuthorization()` y pase el ID de recurso para el medio solicitado. Una llamada correcta devolverá un token multimedia corto, que confirma que el usuario está autorizado para ver el contenido multimedia solicitado.

- Si la llamada pasa: El usuario tiene un token AuthN válido y está autorizado para ver el contenido multimedia solicitado.
- Si la llamada falla: Examine la excepción lanzada para determinar su tipo (AuthN, AuthZ u otro):
- Si la llamada fue un error AuthN, vuelva a iniciar el flujo AuthN.
- Si la llamada fue un error AuthZ, el usuario no está autorizado a ver el contenido multimedia solicitado y se debería mostrar algún tipo de mensaje de error al usuario.
- Si hay algún otro error (error de conexión, error de red, etc.) a continuación, muestre un mensaje de error apropiado al usuario.

Utilice el verificador de tokens de medios para validar el shortMediaToken devuelto correctamente `getAuthorization()` llamada a .

 
**Dependencia:** El verificador de tokens de medios cortos (incluido con la biblioteca AccessEnabler)

- Si la validación pasa: Mostrar/reproducir el contenido solicitado para el usuario.
- Si falla: El token AuthZ no es válido, la solicitud de medios debe rechazarse y se debe mostrar un mensaje de error al usuario.

## 5. Ver flujo de medios (#logout)

- El usuario selecciona los medios que desea ver.
   - ¿Está protegido el medio?\
          - La aplicación comprueba si los medios están protegidos:
      - Si el contenido está protegido, la aplicación inicia el flujo de autorización (AuthZ) anterior.
      - Si el contenido no está protegido, continúe con el flujo Ver contenido.
      - Medios de reproducción

## Configuración de la ID de visitante (#visitorID)

Configuración de un [visitorID del Experience Cloud](https://marketing.adobe.com/resources/help/en_US/mcvid/) es muy importante desde el punto de vista analítico. Una vez establecido el valor visitorID de EC, el SDK envía esta información junto con cada llamada de red y el servicio de autenticación de Adobe Primetime recopila esta información. De este modo, podrá correlacionar los datos de análisis del servicio de autenticación de Adobe Primetime con cualquier otro informe de análisis que pueda tener de otras aplicaciones o sitios web. Encontrará información sobre cómo configurar la ID de visitante de EC [here](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=en).

 
>[!NOTE]
>
>Tenga en cuenta que esta funcionalidad es compatible a partir de la versión 3.1.0 del SDK para JS. 

<!--
### Related Information (#related)

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK API Reference](/help/authentication/javascript-sdk-api-reference.md)
* **JavaScript SDK Code Samples**
-->