---
title: Pasar información del cliente (dispositivo, conexión y aplicación)
description: Pasar información del cliente (dispositivo, conexión y aplicación)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 0%

---


# Pasar información del cliente (dispositivo, conexión y aplicación) {#pass-client-info}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.


## Ámbito {#pass-client-info-scope}

Este documento agrega detalles y libros de cookies para pasar información del cliente (dispositivo, conexión y aplicación) desde una aplicación de programador a las API o SDK de REST de autenticación de Adobe Primetime.

Las ventajas de proporcionar información de clientes son:

* La capacidad de habilitar correctamente la autenticación de la base del hogar (HBA) en el caso de algunos tipos de dispositivos y MVPD que admiten HBA.
* La capacidad de aplicar correctamente los TTL en el caso de algunos tipos de dispositivos (por ejemplo, configurar TTL más largos para sesiones de autenticación en dispositivos conectados a la TV).
* La capacidad de agregar correctamente métricas comerciales en informes desglosados en tipos de dispositivo mediante el monitoreo del servicio de derechos (ESM).
* Desbloquea la capacidad de aplicar correctamente varias reglas comerciales (por ejemplo, ) en tipos de dispositivos específicos.

## Información general {#pass-client-info-overview}

La información del cliente consta de:

* **Dispositivo** información sobre los atributos de hardware y software del dispositivo desde el que el usuario intenta consumir el contenido del programador.
* **Conexión** información sobre los atributos de conexión del dispositivo desde el que el usuario se está conectando a los servicios de autenticación de Adobe Primetime o a los servicios de programación (por ejemplo, implementaciones de servidor a servidor).
* **Aplicación** información sobre la aplicación registrada desde la que el usuario intenta consumir el contenido del programador.

La información del cliente es un objeto JSON creado con claves presentadas en la siguiente tabla.

>[!NOTE]
>
>Lo siguiente **keys** are **mandatory** para enviar en el objeto JSON de información de cliente: **model**, **osName**.
>
>Las claves siguientes tienen **restringido** valores: `primaryHardwareType`, `osName`, `osFamily`, `browserName`, `browserVendor`, `connectionSecure`.

|  | Clave | Restringido | Descripción | Valores posibles |
|---|---|---|---|---|
|  | primaryHardwareType | # Sí | El tipo de hardware principal del dispositivo. | # Los valores están restringidos: Cámara DataCollectionTerminal Escritorio incrustadoRedMódulo eReader JuegosGeolocalización de la consolaRastreador Gafas MediaPlayer MobilePhone PagoTerminal PluginMódem SetTopBox TV Tablet WirelessZona inalámbricaRegistro Desconocido |
| #mandatory | model | No | El nombre del modelo del dispositivo. | Por ejemplo, iPhone, SM-G930V, AppleTV, etc. |
|  | version | No | Versión del dispositivo. | Por ejemplo, 2.0.1, etc. |
|  | fabricante | No | Empresa/organización de fabricación del dispositivo. | Por ejemplo, Samsung, LG, ZTE, Huawei, Motorola, Apple, etc. |
|  | proveedor | No | Empresa/organización de venta del dispositivo. | Por ejemplo, Apple, Samsung, LG, Google, etc. |
| #mandatory | osName | # Sí | El nombre del sistema operativo (OS) del dispositivo. | # Los valores están restringidos: Android Chrome OS Linux Mac OS X OpenBSD Roku OS Windows iOS tvOS webOS |
|  | osFamily | Sí | El nombre del grupo Sistema operativo (OS) del dispositivo. | # Los valores están restringidos: Android BSD Linux PlayStation OS Roku OS Symbian Tizen Windows iOS macOS tvOS webOS |
|  | osVendor | No | El proveedor del sistema operativo (OS) del dispositivo. | Amazon Apple Google LG Microsoft Mozilla Nintendo Nokia Roku Samsung Sony Tizen Project |
|  | osVersion | No | Versión del sistema operativo (OS) del dispositivo. | Por ejemplo, 10.2, 9.0.1, etc. |
|  | browserName | # Sí | El nombre del explorador. | # Los valores están restringidos: Explorador Android Chrome Edge Firefox Internet Explorer Opera Safari SeaMonkey Explorador Symbian |
|  | browserVendor | # Sí | Empresa u organización de creación del explorador. | # Los valores están restringidos: Amazon Apple Google Microsoft Motorola Mozilla Netscape Nintendo Nokia Samsung Sony Ericsson |
|  | browserVersion | No | La versión del explorador del dispositivo. | Por ejemplo, 60.0.3112 |
|  | userAgent | No | El agente de usuario del dispositivo. | Por ejemplo, Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/602.4.8 (KHTML, como Gecko) Versión/10.0.3 Safari/602.4.8 |
|  | displayWidth | No | Ancho de pantalla físico del dispositivo. |  |
|  | displayHeight | No | Altura de la pantalla física del dispositivo. |  |
|  | displayPpi | No | Densidad de píxeles de la pantalla física del dispositivo. | Por ejemplo, 294 |
|  | diagonalScreenSize | No | Dimensión diagonal de pantalla física del dispositivo en pulgadas. | Por ejemplo, 5.5, 10.1 |
|  | connectionIp | No | La IP del dispositivo utilizada para enviar solicitudes HTTP. | Por ejemplo, 8.8.4.4 |
|  | connectionPort | No | Puerto del dispositivo utilizado para enviar solicitudes HTTP. | por ejemplo, 53124 |
|  | connectionType | No | Tipo de conexión de red. | Por ejemplo, WiFi, LAN, 3G, 4G, 5G |
|  | connectionSecure | # Sí | El estado de seguridad de la conexión de red. | # Los valores están restringidos: true - en el caso de una red segura falsa - en el caso de un punto interactivo público |
|  | applicationId | No | Identificador único de la aplicación. | Por ejemplo, CNN |

## Referencias de API {#api-ref}

Esta sección presenta la API responsable de gestionar la información del cliente al utilizar las API o SDK de REST de autenticación de Adobe Primetime.

### API de REST {#rest-api}

Los servicios de autenticación de Adobe Primetime admiten la recepción de la información del cliente de las siguientes maneras:

* Como **encabezado: &quot;X-Device-Info&quot;**
* Como **parámetro de consulta: &quot;device_info&quot;**
* Como **parámetro posterior: &quot;device_info&quot;**

>[!IMPORTANT]
>
>En los tres escenarios, la carga útil del encabezado o del parámetro debe ser **Codificado en base64 y codificado en la dirección URL**.

**SDK**

#### SDK de JavaScript {#js-sdk}

El SDK de JavaScript de AccessEnabler crea de forma predeterminada un objeto JSON de información de cliente, que se pasa a los servicios de autenticación de Adobe Primetime, a menos que se sobrescriba.

El SDK de JavaScript de AccessEnabler es compatible con **solo anulación** la clave &quot;applicationId&quot; del objeto JSON de información de cliente a través del [setRequestor](/help/authentication/javascript-sdk-api-reference.md#setrequestor(inRequestorID,endpoints,options))&#39;s *applicationId* parámetro de opciones.

>[!CAUTION]
>
>La variable `applicationId` El valor del parámetro debe ser un valor String de texto sin formato.
>Si la aplicación Programmer decide pasar el applicationId, el SDK de JavaScript de AccessEnabler seguirá calculando el resto de las claves de información del cliente.

#### SDK de iOS/tvOS {#ios-tvos-sdk}

El SDK de AccessEnabler para iOS/tvOS crea de forma predeterminada un objeto JSON de información de cliente, que se pasa a los servicios de autenticación de Adobe Primetime, a menos que se sobrescriba.

El SDK de AccessEnabler iOS/tvOS es compatible **anular todo** información del cliente objeto JSON a través de la variable [setOptions](/help/authentication/iostvos-sdk-api-reference.md#setoptions)del parámetro device_info.

>[!CAUTION]
>
>La variable *device_info* el valor del parámetro debe ser **Codificado en Base64** *NSString* valor.
>
>En caso de que la aplicación Programador decida pasar la variable *device_info*, se anularán todas las claves de información del cliente calculadas por el SDK de AccessEnabler iOS/tvOS. Por lo tanto, es muy importante calcular y pasar los valores de tantas claves como sea posible. Para obtener más información sobre la implementación, consulte la [Información general](#pass-client-info-overview) y [Guía de iOS/tvOS](#ios-tvos).

#### SDK para Android/FireOS {#and-fire-os-sdk}

La variable `AccessEnabler` El SDK para Android/FireOS crea de forma predeterminada un objeto JSON de información de cliente, que se pasa a los servicios de autenticación de Adobe Primetime, a menos que se sobrescriba.

La variable `AccessEnabler` El SDK para Android/FireOS es compatible **anular todo** información del cliente objeto JSON a través de la variable [setOptions](/help/authentication/android-sdk-api-reference.md#setOptions)&#39;s/[setOptions](/help/authentication/amazon-fireos-native-client-api-reference.md#fire_setOption)&#39;s `device_info` parámetro.

>[!NOTE]
>
>La variable `device_info` el valor del parámetro debe ser **Codificado en Base64** Valor de cadena.

>[!IMPORTANT]
>
>En caso de que la aplicación Programador decida pasar la variable `device_info`, luego todas las claves de información del cliente calculadas por la variable `AccessEnabler` Se anulará el SDK de Android/FireOS. Por lo tanto, es muy importante calcular y pasar los valores de tantas claves como sea posible. Para obtener más información sobre la implementación, consulte la [Información general](#pass-client-info-overview) y [Android](#android) y [FireOS](#fire-tv) guía.

## Cookbooks {#cookbooks}

Esta sección presenta una guía para crear el objeto JSON de información de cliente en el caso de diferentes tipos de dispositivos.

>[!IMPORTANT]
>
>Las claves marcadas con  **!** son obligatorios para enviarse.

### Android {#android}

La información del dispositivo se puede construir de la siguiente manera:

|  | Clave | Fuente | Valor (ejemplo) |
|---|---------------|-----------------------------|---------------|
| ! | model | Build.MODEL | GT-I9505 |
|  | proveedor | Build.BRAND | samsung |
|  | fabricante | Build.MANUFACTURER | samsung |
| ! | version | Build.DEVICE | jflte |
|  | displayWidth | DisplayMetrics.widthPixels | 600 |
|  | displayHeight | DisplayMetrics.heightPixels | 800 |
| ! | osName | codificado | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.0.1 |

La información de conexión se puede construir de la siguiente manera:

|  | Clave | Fuente | Valor (ejemplo) |
|---|---|---|---|
| ! | connectionType | `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>` `getSystemService(Context.CONNECTIVITY_SERVICE).getActiveNetworkInfo().getType()` | `"WIFI","BLUETOOTH","MOBILE","ETHERNET","VPN","DUMMY","MOBILE_DUN","WIMAX","notAccessible"` |
|  | connectionSecure |  |  |

La información de la aplicación se puede construir de la siguiente manera:

|  | Clave | Fuente | Valor (ejemplo) |
|---|---------------|-----------|--------------|
|  | applicationId | codificado | CNN |

>[!IMPORTANT]
La información de dispositivo, conexión y aplicación debe agregarse al mismo objeto JSON. Después, el objeto resultante debe ser **Codificado en Base64**. Además, en el caso de las API de REST de autenticación de Adobe Primetime, el valor debe ser **URL codificada**.

**Código de muestra**

```JAVA
private JSONObject computeClientInformation() {
     String LOGGING_TAG = "DefineClass.class";
  
     JSONObject clientInformation = new JSONObject();

     String connectionType;

     try {
          ConnectivityManager cm = (ConnectivityManager) getContext().getSystemService(CONNECTIVITY_SERVICE);
          NetworkInfo activeNetwork = cm.getActiveNetworkInfo();

          if (activeNetwork != null && activeNetwork.isConnectedOrConnecting()) {
              switch (activeNetwork.getType()) {
                    case ConnectivityManager.TYPE_WIFI: {
                        connectionType = "WIFI";
                        break;
                    }
                    case ConnectivityManager.TYPE_BLUETOOTH: {
                        connectionType = "BLUETOOTH";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE: {
                        connectionType = "MOBILE";
                        break;
                    }
                    case ConnectivityManager.TYPE_ETHERNET: {
                        connectionType = "ETHERNET";
                        break;
                    }
                    case ConnectivityManager.TYPE_VPN: {
                        connectionType = "VPN";
                        break;
                    }
                    case ConnectivityManager.TYPE_DUMMY: {
                        connectionType = "DUMMY";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE_DUN: {
                        connectionType = "MOBILE_DUN";
                        break;
                    }
                    case ConnectivityManager.TYPE_WIMAX: {
                        connectionType = "WIMAX";
                        break;
                    }
                    default:
                       connectionType = ConnectivityManager.EXTRA_OTHER_NETWORK_INFO;
              }
          } else {
                connectionType = ConnectivityManager.EXTRA_NO_CONNECTIVITY;
          }
     } catch (Exception e) {
          connectionType = "notAccessible";
     }

     try {
          clientInformation.put("model",Build.MODEL);
          clientInformation.put("vendor", Build.BRAND);
          clientInformation.put("manufacturer",Build.MANUFACTURER);
          clientInformation.put("version",Build.DEVICE);
          clientInformation.put("osName","Android");
          clientInformation.put("osVersion",Build.VERSION.RELEASE);
          clientInformation.put("connectionType",connectionType);
          clientInformation.put("applicationId","CNN");
     } catch (JSONException e) {
          Log.e(LOGGING_TAG, e.getMessage());
     }

     return Base64.encodeToString(clientInformation.toString().getBytes(), Base64.NO_WRAP);
}
```

>[!NOTE]
**Recursos:**
* clase pública [versión](https://developer.android.com/reference/android/os/Build.html){target=_blank} en la documentación de desarrolladores de Java.


### FireTV {#fire-tv}

La información del dispositivo se puede construir de la siguiente manera:

|  | Clave | Fuente | Valor (p. ej.) |
|---|---------------|-----------------------------|--------------|
| ! | model | Build.MODEL | AFTM |
|  | proveedor | Build.BRAND | Amazon |
|  | fabricante | Build.MANUFACTURER | Amazon |
| ! | version | Build.DEVICE | montoya |
|  | displayWidth | DisplayMetrics.widthPixels |  |
|  | displayHeight | DisplayMetrics.heightPixels |  |
| ! | osName | codificado | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.1.1 |

La información de conexión se puede construir de la siguiente manera:

|  | Clave | Fuente | Valor (ejemplo) |
|---|------------------|--------|---------------|
| ! | connectionType |  |  |
|  | connectionSecure |  |  |

La información de la aplicación se puede construir de la siguiente manera:

|  | Clave | Fuente | Valor (ejemplo) |
|---|---------------|-----------|--------------|
|  | applicationId | codificado | CNN |

>[!IMPORTANT]
La información de dispositivo, conexión y aplicación debe agregarse al mismo objeto JSON. Después, el objeto resultante debe ser **Codificado en Base64**. Además, en el caso de las API de REST de autenticación de Adobe Primetime, el valor debe ser **URL codificada**.

>[!NOTE]
**Recursos:**
* clase pública [Generar](https://developer.android.com/reference/android/os/Build.html){target=_blank} en la documentación de desarrolladores de Android.
* [Identificación de dispositivos FireTV](https://developer.amazon.com/docs/fire-tv/identify-amazon-fire-tv-devices.html){target=_blank}


### iOS/tvOS {#ios-tvos}

La información del dispositivo se puede construir de la siguiente manera:

|  | Clave | Fuente | Valor (ejemplo) |
|---|---------------|------------------------|--------------|
| ! | model | uname.machine | iPhone |
|  | proveedor | codificado | Apple |
|  | fabricante | codificado | Apple |
| ! | version | uname.machine | 8,1 |
|  | displayWidth | UIScreen.mainScreen | 320 |
|  | displayHeight | UIScreen.mainScreen | 568 |
| ! | osName | UIDevice.systemName | iOS |
| ! | osVersion | UIDevice.systemVersion | 10.2 |

La información de conexión se puede construir de la siguiente manera:

|  | Clave | Fuente | Valor (ejemplo) |
|---|------------------|-------------------------------------------|--------------|
| ! | connectionType | [Reachability currentReachabilityStatus] |  |
|  | connectionSecure |  |  |


La información de la aplicación se puede construir de la siguiente manera:

|  | Clave | Fuente | Valor (ejemplo) |
|---|---------------|-----------|--------------|
|  | applicationId | codificado | CNN |

>[!IMPORTANT]
La información de dispositivo, conexión y aplicación debe agregarse al mismo objeto JSON. Después, el objeto resultante debe estar codificado en Base64. Además, en el caso de las API de REST de autenticación de Adobe Primetime, el valor debe tener codificación de dirección URL.

**Código de muestra**

```C
+ (NSString *)computeClientInformation {        
        struct utsname u;
        uname(&u);

        NSString *hardware = [NSString stringWithCString:u.machine encoding:NSUTF8StringEncoding];

        UIDevice *device = [UIDevice currentDevice];

        NSString *deviceType;

        switch (UI_USER_INTERFACE_IDIOM()) {
            case UIUserInterfaceIdiomPhone:
                deviceType = @"MobilePhone";
                break;
            case UIUserInterfaceIdiomPad:
                deviceType = @"Tablet";
                break;
            case UIUserInterfaceIdiomTV:
                deviceType = @"TV";
                break;
            default:
                deviceType = @"Unknown";
        }

        CGRect screenRect = [[UIScreen mainScreen] bounds];
        NSNumber *screenWidth = @((float) screenRect.size.width);
        NSNumber *screenHeight = @((float) screenRect.size.height);

        Reachability *reachability = [Reachability reachabilityForInternetConnection];
        [reachability startNotifier];

        NetworkStatus status = [reachability currentReachabilityStatus];

        NSString *connectionType;

        if (status == NotReachable) {
            connectionType = @"notConnected";
        } else if (status == ReachableViaWiFi) {
            connectionType = @"WiFi";
        } else if (status == ReachableViaWWAN) {
            connectionType = @"cellular";
        }

        NSMutableDictionary *clientInformation = [@{
                @"type": deviceType,
                @"model": device.model,
                @"vendor": @"Apple",
                @"manufacturer": @"Apple",
                @"version": [hardware stringByReplacingOccurrencesOfString:device.model withString:@""],
                @"osName": device.systemName,
                @"osVersion": device.systemVersion,
                @"displayWidth": screenWidth,
                @"displayHeight": screenHeight,
                @"connectionType": connectionType,
                @"applicationId": @"CNN" 
        } mutableCopy];

        NSError *error;
        NSData *jsonData = [NSJSONSerialization dataWithJSONObject:clientInformation options:NSJSONWritingPrettyPrinted error:&error];
        NSString *base64Encoded = [jsonData base64EncodedStringWithOptions:0];

        return base64Encoded;
}
```

>[!NOTE]
**Recursos:**
* [UIDevice](https://developer.apple.com/documentation/uikit/uidevice#//apple_ref/occ/cl/UIDevice){target=_blank}
* [uname](https://man7.org/linux/man-pages/man2/uname.2.html){target=_blank}
* [Acerca de la accesibilidad](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html){target=_blank}


### Roku {#roku}

La información del dispositivo se puede construir de la siguiente manera:

| Clave | Fuente | Valor (ejemplo) |  |
|-----|---------------|--------------------------------------------|-----------------|
| ! | model | codificado | &quot;Roku&quot; |
|  | proveedor | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;, &quot;Roku&quot; |
|  | fabricante | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;, &quot;Roku&quot; |
| ! | version | ifDeviceInfo.GetModelDetails().ModelNumber | &quot;5303X&quot; |
|  | displayWidth | ifDeviceInfo.GetDisplaySize().w | 1920 |
|  | displayHeight | ifDeviceInfo.GetDisplaySize().h | 1080 |
| ! | osName | codificado | &quot;Roku&quot; |
| ! | osVersion | ifDeviceInfo.getVersion() |  |

La información de conexión se puede construir de la siguiente manera:

|  | Clave | Fuente | Valor (ejemplo) |
|---|---|---|---|
| ! | connectionType | ifDeviceInfo.GetConnectionType() | &quot;WifiConnection&quot;, &quot;WiredConnection&quot; |
|  | connectionSecure | codificado | true si la conexión está cableada |

La información de la aplicación se puede construir de la siguiente manera:

|  | Clave | Fuente | Valor (ejemplo) |
|---|---------------|-----------|--------------|
|  | applicationId | codificado | CNN |

>[!IMPORTANT]
La información de dispositivo, conexión y aplicación debe agregarse al mismo objeto JSON. Después, el objeto resultante debe ser **Codificado en Base64**. Además, en el caso de las API de REST de autenticación de Adobe Primetime, el valor debe tener codificación de dirección URL.

>[!NOTE]
Para obtener más información, consulte [ifDeviceInfo](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md)

### XBOX 1/360 {#xbox}

La información del dispositivo se puede construir de la siguiente manera:

|  | Clave | Fuente | Valor (ejemplo) |
|---|---|---|---|
| ! | model | EasClientDeviceInformation.SystemProductName |  |
|  | proveedor | codificado | Microsoft |
|  | fabricante | codificado | Microsoft |
| ! | version | EasClientDeviceInformation.SystemHardwareVersion |  |
|  | displayWidth | DisplayInformation.ScreenWidthInRawPixels | 1920 |
|  | displayHeight | DisplayInformation.ScreenHeightInRawPixels | 1080 |
| ! | osName | EasClientDeviceInformation.OperatingSystem |  |
| ! | osVersion | EasClientDeviceInformation.SystemFirmwareVersion |  |

La información de conexión se puede construir de la siguiente manera:

|  | Clave | Fuente | Ejemplo |
|---|---|---|---|
| ! | connectionType |  |  |
|  | connectionSecure | NetworkAuthenticationType | &quot;None&quot;, &quot;Wpa&quot;, etc. |

La información de la aplicación se puede construir de la siguiente manera:

| Clave | Fuente | Valor (ejemplo) |
|---|---|---|
| applicationId | codificado | CNN |

>[!IMPORTANT]
La información de dispositivo, conexión y aplicación debe agregarse al mismo objeto JSON. Después, el objeto resultante debe ser **Codificado en Base64**. Además, en el caso de las API de REST de autenticación de Adobe Primetime, el valor debe ser **URL codificada**.

**Recursos**

* [EasClientDeviceInformation (clase)](https://docs.microsoft.com/en-us/uwp/api/windows.security.exchangeactivesyncprovisioning.easclientdeviceinformation?view=winrt-22000)
* [Clase DisplayInformation](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.display.displayinformation?view=winrt-22000)


