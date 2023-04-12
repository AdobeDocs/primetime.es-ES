---
title: Compatibilidad con SFSafariViewController en el SDK para iOS 3.2+
description: Compatibilidad con SFSafariViewController en el SDK para iOS 3.2+
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Compatibilidad con SFSafariViewController en el SDK para iOS 3.2+ {#sfsafariviewcontroller-support-on-ios-sdk-3.2}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>


**Debido a los requisitos de seguridad, algunas páginas de inicio de sesión de MVPD DEBEN presentarse en un SFSafariViewController, en lugar de en vistas web.**

Algunos MVPD requieren que sus páginas de inicio de sesión se presenten en un control de navegador seguro como SFSafariViewController. Están bloqueando activamente webviews, por lo que para poder autenticarnos con ellos debemos usar SVC. 

## Compatibilidad {#compatiblity}

A partir del SDK para iOS versión 3.1, el SDK de AccessEnabler muestra automáticamente la página de inicio de sesión de MVPD específicos en un SFSafariViewController, en función de la configuración del servidor.

La versión 3.1 del SDK presenta automáticamente el SFSafariViewController desde el controlador de vista raíz de la aplicación. Aunque esto simplifica la administración de páginas de inicio de sesión para los implementadores, hay casos en los que no es posible presentar el SFSafariViewController desde el controlador de vista raíz, debido a la implementación específica de la aplicación (como un controlador modal ya visible).

Para estos casos, la versión 3.2 introduce la capacidad del programador para administrar manualmente el SVC.

## Gestión manual de SVC {#manual-svc-management}

Para administrar manualmente SVC, el implementador debe realizar los siguientes pasos:
 

1. llamada **setOptions([&quot;handleSVC&quot;:true])** después de la inicialización de AccessEnabler (asegúrese de que esta llamada se realice antes de que comience la autenticación). Esto habilitará la administración &quot;manual&quot; de SVC, el SDK no presentará automáticamente el SVC, sino que, cuando sea necesario, llamará a **navegar(toUrl:*{url}* useSVC:true)**.  

1. implementar la llamada de retorno opcional **navegarToUrl:useSVC:** dentro de la implementación debe crear una instancia svc utilizando la instancia SFSafariViewController utilizando la dirección url proporcionada y presentarla en la pantalla:

   ```obj-c
   func navigate(toUrl url: String!, useSVC: Bool) {
       svc =  SFSafariViewController(url: URL(string: url)!)
       svc.delegate = self
       myController.present(svc, animated: true)
       }
   ```

   ***Notas:***

   - *Puede personalizar el SFSafariViewController del modo que desee. Por ejemplo, en iOS 11+ puede cambiar la etiqueta &quot;Listo&quot; a &quot;Cancelar&quot;.*
   - *para poder descartar el svc, necesita una referencia a él, no lo cree en el ámbito de **navegarToUrl:useSVC***
   - *use su propio controlador de vista para &quot;myController&quot;*\
       

1. En la implementación delegada de **application(\_app: UIApplication, abrir url: URL, opciones: \[UIApplicationOpenURLOptionsKey: Any\]) -\> Bool**, añada código para cerrar el svc. Ya debería tener algún código ahí que llame a **accessEnabler.handleExternalURL()**. Justo debajo, añada:

   ```obj-c
   if(svc != nil) {
       svc.dismiss(animated: true)
   }
   ```

   De nuevo, svc es una referencia al SFSafariViewController que creó en el paso 2.\
    

1. Implementación **safariViewControllerDidFinish(\_ controlador: SFSafariViewController)** from **SFSafariViewControllerDelegate** para poder capturar cuando el usuario canceló el svc con el botón &quot;Listo&quot;. En esta función, para informar al SDK de que la autenticación se ha cancelado, debe llamar a:

   ```obj-c
   accessEnabler.setSelectedProvider(nil)
   ```

