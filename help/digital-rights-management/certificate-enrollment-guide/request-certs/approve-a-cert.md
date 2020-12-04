---
description: 'null'
seo-description: 'null'
seo-title: Aprobar un certificado (cuenta o administrador secundario)
title: Aprobar un certificado (cuenta o administrador secundario)
uuid: 5b95e2e8-abe9-4aef-bcb4-9b98ba6604d1
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Aprobar un certificado (cuenta o administrador secundario){#approve-a-certificate-account-or-secondary-administrator}

1. Inicie sesión en el sitio de inscripción de certificados.
1. Seleccione la ficha **[!UICONTROL Certificates]**.
1. Revise la solicitud para comprobar que es válida.
1. Si la solicitud es válida, haga clic en **[!UICONTROL Approve]**.

   También puede agregar un comentario. Se envía un mensaje de correo electrónico al solicitante indicando que uno de los administradores de compañía ha aprobado la solicitud. Se envía una copia de este correo electrónico a los administradores de compañía y Adobe.

1. Si la solicitud no es válida, haga clic en **[!UICONTROL Reject]** e introduzca un comentario en el cuadro de diálogo de confirmación.

   Se envía un mensaje de correo electrónico al solicitante indicando que uno de los administradores de la compañía ha rechazado la solicitud. Se envía una copia de este correo electrónico a los administradores de compañía.

Cuando un administrador aprueba una solicitud de certificado, Adobe comprueba la identidad del solicitante. Adobe se pone en contacto con el solicitante en el número de teléfono indicado en su perfil.

El administrador de Adobe intenta ponerse en contacto con el solicitante dos veces en un período de tres días. Si el administrador de Adobe no puede ponerse en contacto con el solicitante, dejará un mensaje solicitando una llamada de retorno o le proporcionará una hora para volver a llamar. Si el administrador de Adobe no puede ponerse en contacto con el solicitante, se enviará un mensaje de correo electrónico a los administradores.

>[!NOTE]
>
>Solo los administradores de cuenta y de secundaria pueden cambiar el número de teléfono de compañía y la frase de desafío del solicitante.

Si se comprueba la identidad del solicitante, éste recibe un correo electrónico que contiene el archivo PKCS#7 ( [!DNL p7b]).

El solicitante puede copiar el contenido PKCS#7 del cuerpo del correo electrónico y guardarlo en un archivo o utilizar el archivo adjunto al correo electrónico. Adobe recomienda que, al guardar el archivo PKSC#7, utilice el nombre base que utilizó para generar la clave privada y el archivo CSR.

>[!NOTE]
>
>El archivo enviado al solicitante solo contiene el certificado. El archivo no contiene información de clave privada.

