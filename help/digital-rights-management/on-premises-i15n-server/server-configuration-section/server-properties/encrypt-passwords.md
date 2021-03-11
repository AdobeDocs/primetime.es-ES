---
title: Codificar contraseñas
description: Codificar contraseñas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 0%

---


# Codificar contraseñas{#encrypt-passwords}

Los archivos de propiedades incluyen varios valores de contraseña que no se deben introducir como texto sin formato. Cifre estos valores con el siguiente comando:

`java -jar adobe-flashaccess-i15n-setup.jar password`

Este comando generará una contraseña cifrada que se utilizará en los archivos de propiedades.

>[!NOTE]
>Esta no es la utilidad utilizada para cifrar contraseñas del servidor de licencias.

