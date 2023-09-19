---
title: Aprobar un certificado (cuenta o administrador secundario)
description: Aprobar un certificado (cuenta o administrador secundario)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Aprobar un certificado (cuenta o administrador secundario){#approve-a-certificate-account-or-secondary-administrator}

1. Inicie sesión en el sitio de inscripción de certificados.
1. Seleccione el **[!UICONTROL Certificates]** pestaña.
1. Revise la solicitud para comprobar que es válida.
1. Si la solicitud es válida, haga clic en **[!UICONTROL Approve]**.

   También puede agregar un comentario. Se envía un correo electrónico al solicitante en el que se indica que uno de los administradores de la empresa ha aprobado la solicitud. Se envía una copia de este correo electrónico a los administradores de la empresa y del Adobe.

1. Si la solicitud no es válida, haga clic en **[!UICONTROL Reject]** e introduzca un comentario en el cuadro de diálogo de confirmación.

   Se envía un correo electrónico al solicitante en el que se indica que uno de los administradores de la empresa ha rechazado la solicitud. Se envía una copia de este correo electrónico a los administradores de la empresa.

Cuando un administrador aprueba una solicitud de certificado, el Adobe comprueba la identidad del solicitante. El Adobe se pone en contacto con el solicitante en el número de teléfono que aparece en su perfil.

El administrador del Adobe intenta ponerse en contacto con el solicitante dos veces en un periodo de tres días. Si el administrador del Adobe no puede ponerse en contacto con el solicitante, deja un mensaje en el que se solicita una devolución de llamada o indica la hora en la que volverá a llamar. Si el administrador del Adobe no puede ponerse en contacto con el solicitante, se envía un mensaje de correo electrónico a los administradores.

>[!NOTE]
>
>Solo los administradores de cuenta y secundarios pueden cambiar el número de teléfono de la empresa y la frase de desafío del solicitante.

Si se verifica la identidad del solicitante, el solicitante recibe un mensaje de correo electrónico con el archivo PKCS#7 ( [!DNL p7b]).

El solicitante puede copiar el contenido PKCS#7 del cuerpo del correo electrónico y guardarlo en un archivo o utilizar el archivo adjunto al correo electrónico. Adobe recomienda que, al guardar el archivo PKSC#7, utilice el nombre base utilizado para generar la clave privada y el archivo CSR.

>[!NOTE]
>
>El archivo enviado al solicitante contiene solo el certificado. El archivo no contiene información de clave privada.
