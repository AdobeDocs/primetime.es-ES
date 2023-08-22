---
title: Compatibilidad con SFSafariViewController en el SDK 3.2+ de iOS
description: Compatibilidad con SFSafariViewController en el SDK 3.2+ de iOS
exl-id: 6691550f-c36f-4fae-aa77-082ca7d8a60a
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Compatibilidad con SFSafariViewController en el SDK 3.2+ de iOS {#sfsafariviewcontroller-support-on-ios-sdk-3.2}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

</br>


**Debido a los requisitos de seguridad, algunas páginas de inicio de sesión de MVPD DEBEN presentarse en un SFSafariViewController, en lugar de vistas web.**

Algunas MVPD requieren que sus páginas de inicio de sesión se presenten en un control de explorador seguro como SFSafariViewController. Están bloqueando activamente las visualizaciones web, por lo que para poder autenticarnos con ellas debemos usar SVC.

## Compatibilidad {#compatiblity}

A partir de la versión 3.1 del SDK de iOS, el SDK de AccessEnabler muestra automáticamente la página de inicio de sesión de MVPD específicas en un SFSafariViewController, en función de la configuración del servidor.

La versión 3.1 del SDK presenta automáticamente SFSafariViewController desde el controlador de vista raíz de la aplicación. Aunque esto simplifica la administración de páginas de inicio de sesión para los implementadores, hay casos en los que no es posible presentar el SFSafariViewController desde el controlador de vista raíz, debido a la implementación específica de la aplicación (como un controlador modal ya visible).

Para estos casos, la versión 3.2 introduce la capacidad para que el programador administre manualmente el SVC.

## Administración manual de SVC {#manual-svc-management}

Para administrar manualmente SVC, el implementador debe realizar los siguientes pasos:


1. llamada **setOptions()[&quot;handleSVC&quot;:true])** después de la inicialización de AccessEnabler (asegúrese de que esta llamada se realiza antes de que comience la autenticación). Esto habilitará la administración &quot;manual&quot; de SVC, el SDK no presentará automáticamente el SVC, sino que, cuando sea necesario, llamará a **navegar(toUrl:*{url}* useSVC:true)**.

1. implementar la llamada de retorno opcional **navigationToUrl:useSVC:** dentro de la implementación debe crear una instancia de servicio con la instancia de SFSafariViewController utilizando la dirección url proporcionada y presentarla en la pantalla:

   ```obj-c
   func navigate(toUrl url: String!, useSVC: Bool) {
       svc =  SFSafariViewController(url: URL(string: url)!)
       svc.delegate = self
       myController.present(svc, animated: true)
       }
   ```

   ***Notas:***

   - *Puede personalizar SFSafariViewController como desee. Por ejemplo, en iOS 11+ puede cambiar la etiqueta &quot;Listo&quot; a &quot;Cancelar&quot;.*
   - *para poder descartar el svc, necesita una referencia a él, no lo cree en el ámbito de **navegarAurl:usarSVC***
   - *use su propio controlador de vista para &quot;myController&quot;*


1. En la implementación delegada de la aplicación de **application(\_app: UIApplication, abrir url: URL, opciones: \[UIApplicationOpenURLOptionsKey: Any\]) -\> Bool**, agregue código para cerrar el svc. Ya debería tener algún código allí que llame a **accessEnabler.handleExternalURL()**. Justo debajo añada:

   ```obj-c
   if(svc != nil) {
       svc.dismiss(animated: true)
   }
   ```

   De nuevo, svc es una referencia al SFSafariViewController que creó en el paso 2.


1. Implementación **safariViewControllerDidFinish(\_ controller: SFSafariViewController)** de **SFSafariViewControllerDelegate** para detectar cuándo el usuario canceló el servicio con el botón &quot;Listo&quot;. En esta función, para informar al SDK de que la autenticación se ha cancelado, debe llamar a:

   ```obj-c
   accessEnabler.setSelectedProvider(nil)
   ```
