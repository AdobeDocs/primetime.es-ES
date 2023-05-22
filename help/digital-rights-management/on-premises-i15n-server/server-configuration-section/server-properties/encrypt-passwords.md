---
title: Cifrar contraseñas
description: Cifrar contraseñas
copied-description: true
exl-id: 97b78e00-e5e3-4a9d-8eab-fcf96d3b1219
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
