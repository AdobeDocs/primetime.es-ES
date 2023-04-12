---
title: Autenticación de Adobe Primetime y el nuevo modelo de permisos "Marshmallow" de Android 6
description: Autenticación de Adobe Primetime y el nuevo modelo de permisos "Marshmallow" de Android 6
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---



# Autenticación de Adobe Primetime y el nuevo modelo de permisos &quot;Marshmallow&quot; de Android 6 {#adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

La nueva versión del malvavisco de Android 6 presenta algunas actualizaciones del modelo de permisos, que pueden afectar al comportamiento de las aplicaciones que utilizan la versión 1.8 o anterior del SDK de autenticación de Adobe Primetime existente. 

Como nueva función, el nuevo sistema operativo Android ofrece [control granular sobre los permisos que requieren las aplicaciones en el momento de la instalación y en tiempo de ejecución](https://developer.android.com/about/versions/marshmallow/android-6.0-changes.html).

>[!IMPORTANT]
>
>Los cambios que se describen a continuación: **solo afectan a las aplicaciones desarrolladas específicamente para Android 6.0** (targetSdkVersion=23). No afectan a las aplicaciones antiguas ya instaladas en el dispositivo del usuario al actualizar a Android 6.0. 


En concreto, para aplicaciones desarrolladas en Android Studio que utilizan [Nivel de API 23](http://developer.android.com/sdk/api_diff/23/changes.html) y que utilizan el SDK de autenticación de Adobe Primetime, el desarrollador deberá escribir código personalizado (consulte el fragmento de código a continuación) [déclencheur del cuadro de diálogo permitir/denegar permisos](https://developer.android.com/training/permissions/requesting.html). 

A continuación se muestra el extracto de código utilizado para solicitar acceso de escritura al almacenamiento externo del dispositivo:

```java
// Here, thisActivity is the current activity
if (ContextCompat.checkSelfPermission(thisActivity,
                Manifest.permission.WRITE_EXTERNAL_STORAGE)
        != PackageManager.WRITE_EXTERNAL_STORAGE) {

    // Should we show an explanation?
    if (ActivityCompat.shouldShowRequestPermissionRationale(thisActivity,
            Manifest.permission.WRITE_EXTERNAL_STORAGE)) {

        // Show an expanation to the user *asynchronously* -- don't block
        // this thread waiting for the user's response! After the user
        // sees the explanation, try again to request the permission.

    } else {

        // No explanation needed, we can request the permission.

        ActivityCompat.requestPermissions(thisActivity,
                new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE);

        // MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE is an
        // app-defined int constant. The callback method gets the
        // result of the request.
    }
}
```




**Desde la perspectiva de los usuarios**, una vez instalados, los usuarios son recibidos por una ventana que les solicita que confirmen los permisos de lectura y escritura de los archivos (véase la figura 2 a continuación). Esto lleva a uno de los dos resultados siguientes:

1. Si el usuario **confirma** Con los permisos, el flujo de autenticación normal se mantendrá y los tokens se almacenarán en el almacenamiento global. Los usuarios permanecerán autenticados en la aplicación y en todas las aplicaciones mediante la autenticación de Adobe Primetime durante todo el tiempo que los tokens sean válidos.
1. Si el usuario **niega** Con los permisos, las acciones de escritura en el almacenamiento fallarán y los usuarios solo se autenticarán hasta que salgan de la aplicación. Tenga en cuenta que algunas aplicaciones se reinician al cambiar entre en primer y segundo plano, de modo que los usuarios se cierren la sesión al realizar esta acción. Los tokens NO se almacenan y los usuarios deberán autenticarse cada vez que utilicen la aplicación. 


>[!TIP]
>
>Actualmente se está desarrollando una función que introduce resiliencia de almacenamiento para el SDK 1.9 de autenticación de Adobe Primetime. El nuevo SDK está diseñado para **versión de la última semana de octubre**. La aplicación volverá a escribir en el almacenamiento de simulación de pruebas de la aplicación cada vez que no se pueda utilizar el almacenamiento general. Esto cubre el caso en el que, para aplicaciones desarrolladas en el nivel de API 23, los usuarios NO aceptan permisos de lectura/escritura en el almacenamiento global. Los tokens se almacenan individualmente por aplicación, lo que significa que el inicio de sesión único entre aplicaciones que utilizan la autenticación de Adobe Primetime se desactivará.


![](assets/android-permissions-request.png)

*Figura: El cuadro de diálogo de solicitud de permiso para aplicaciones escritas en el nivel 23 de la API de segmentación*

>[!IMPORTANT]
>
> Consejos de Adobe **sus socios para desarrollar aplicaciones utilizando el nivel de API 22 (targetSdkVersion=22) o superior para garantizar la mejor experiencia de usuario posible en el proceso de autenticación**. 
