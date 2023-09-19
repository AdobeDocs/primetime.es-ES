---
title: Cifrar contraseñas
description: Cifrar contraseñas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 0%

---

# Cifrar contraseñas{#encrypt-passwords}

Los archivos de propiedades incluyen varios valores de contraseña que no debe introducir como texto sin formato. Cifre estos valores con el siguiente comando:

`java -jar adobe-flashaccess-i15n-setup.jar password`

Este comando generará una contraseña cifrada, que se utilizará en los archivos de propiedades.

>[!NOTE]
>Esta no es la utilidad que se usa para cifrar contraseñas del servidor de licencias.
