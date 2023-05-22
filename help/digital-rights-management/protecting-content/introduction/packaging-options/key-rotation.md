---
description: Puede seleccionar las siguientes opciones de cifrado al crear un paquete. Sin embargo, no puede modificar las opciones de cifrado durante la adquisición de la licencia
title: Rotación de clave
exl-id: 1b439b5f-7a63-4fe2-ae15-c18cda0b31cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Rotación de clave {#key-rotation}

Puede seleccionar las siguientes opciones de cifrado al crear un paquete. Sin embargo, no puede modificar las opciones de cifrado durante la adquisición de la licencia:

Durante el empaquetado, el contenido suele cifrarse con la clave de cifrado de contenido (CEK). El cliente obtiene una licencia que contiene el CEK para consumir el contenido.

Cuando se habilita la rotación de claves, la clave de rotación se utiliza para cifrar el contenido y la clave se puede cambiar para que cada clave de rotación se utilice únicamente para cifrar una parte del contenido. Las claves de rotación están protegidas mediante la clave de cifrado de contenido y el cliente sigue obteniendo una sola licencia que contiene la clave CEK para consumir el contenido.

La implementación del empaquetador puede controlar la clave de cifrado de contenido y las claves de rotación utilizadas, así como la frecuencia con la que cambian las claves de rotación.

>[!NOTE]
>
>El contenido empaquetado mediante la rotación de claves solo se puede reproducir en clientes DRM de Primetime versión 3.0 o posterior. Es posible que los clientes más antiguos tengan que actualizar para reproducir este contenido.
