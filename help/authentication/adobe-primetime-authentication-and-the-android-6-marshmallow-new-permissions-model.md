---
title: Autenticación de Adobe Primetime y el modelo de nuevos permisos de Android 6 "Marshmallow"
description: Autenticación de Adobe Primetime y el modelo de nuevos permisos de Android 6 "Marshmallow"
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Autenticación de Adobe Primetime y el modelo de nuevos permisos de Android 6 &quot;Marshmallow&quot; {#adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

</br>

La nueva versión de Android 6 Marshmallow presenta algunas actualizaciones del modelo de permisos, que pueden afectar al comportamiento de las aplicaciones que utilizan la versión 1.8 y anteriores del SDK de autenticación de Adobe Primetime.

Como nueva función, el nuevo sistema operativo Android ofrece [control granular sobre los permisos que las aplicaciones requieren en el momento de la instalación y durante la ejecución](https://developer.android.com/about/versions/marshmallow/android-6.0-changes.html).

>[!IMPORTANT]
>
>Los cambios que se describen a continuación **solo afectan a las aplicaciones desarrolladas específicamente para Android 6.0** (targetSdkVersion=23). No afectan a las aplicaciones más antiguas instaladas en el dispositivo del usuario al actualizar a Android 6.0.


En concreto, para aplicaciones desarrolladas en Android Studio que utilizan [Nivel de API 23](http://developer.android.com/sdk/api_diff/23/changes.html) y que utilizan el SDK de autenticación de Adobe Primetime, el desarrollador deberá escribir un código personalizado (consulte el fragmento de código que aparece a continuación) [para almacenar en déclencheur el cuadro de diálogo permitir/denegar permisos](https://developer.android.com/training/permissions/requesting.html).

A continuación se muestra un extracto de código utilizado para solicitar acceso de escritura al almacenamiento externo del dispositivo:

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




**Desde la perspectiva de los usuarios** Sin embargo, tras la instalación, los usuarios son recibidos por una ventana pidiéndoles que confirmen los permisos de lectura y escritura para los archivos (ver figura 2 a continuación). Esto conduce a uno de los dos resultados siguientes:

1. Si el usuario **confirma** Con los permisos, se mantendrá el flujo de autenticación normal y los tokens se almacenarán en el almacenamiento global. Los usuarios permanecerán autenticados en la aplicación y en todas las aplicaciones mediante la autenticación de Adobe Primetime durante el tiempo en que los tokens sean válidos.
1. Si el usuario **niega** Con los permisos, las acciones de escritura en el almacenamiento fallarán y los usuarios solo se autenticarán hasta que salgan de la aplicación. Tenga en cuenta que algunas aplicaciones se reinicializan al cambiar entre primer y segundo plano, de modo que se cerrará la sesión de los usuarios al realizar esta acción. Los tokens NO se almacenan, y los usuarios deberán autenticarse cada vez que usen la aplicación.


>[!TIP]
>
>Actualmente se está desarrollando una función que introduce resiliencia del almacenamiento para el SDK 1.9 de autenticación de Adobe Primetime. El nuevo SDK está diseñado para **Lanzamiento en la última semana de octubre**. La aplicación volverá a escribir en el almacenamiento de espacio aislado de la aplicación siempre que no se pueda utilizar el almacenamiento general. Esto cubre el caso en el que, para aplicaciones desarrolladas en el nivel de API 23, los usuarios NO aceptan permisos de lectura/escritura en el almacenamiento global. Los tokens se almacenan individualmente por aplicación, lo que significa que el inicio de sesión único entre aplicaciones que utilizan la autenticación de Adobe Primetime se deshabilitará.


![](assets/android-permissions-request.png)

*Imagen: cuadro de diálogo de solicitud de permiso para aplicaciones escritas como objetivo de nivel de API 23*

>[!IMPORTANT]
>
> Adobe aconseja **a sus socios a desarrollar aplicaciones con el nivel de API 22 (targetSdkVersion=22) o anterior para garantizar la mejor experiencia de usuario posible en el proceso de autenticación**.
