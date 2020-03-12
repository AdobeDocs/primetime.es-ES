---
description: 'Puede seleccionar las siguientes opciones de codificación al crear un paquete. Sin embargo, no puede modificar las opciones de cifrado durante la adquisición de licencias '
seo-description: 'Puede seleccionar las siguientes opciones de codificación al crear un paquete. Sin embargo, no puede modificar las opciones de cifrado durante la adquisición de licencias '
seo-title: Rotación de clave
title: Rotación de clave
uuid: 6ac3b828-2cd1-42df-b9ee-4daa8e553d5e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Rotación de clave {#key-rotation}

Puede seleccionar las siguientes opciones de codificación al crear un paquete. Sin embargo, no puede modificar las opciones de codificación durante la adquisición de licencias:

Durante el empaquetado, el contenido suele cifrarse con la clave de cifrado de contenido (CEK). El cliente obtiene una licencia que contiene el CEK para consumir el contenido.

Cuando se activa la rotación de claves, la tecla de rotación se utiliza para cifrar el contenido y la clave se puede cambiar para que cada tecla de rotación se utilice solamente para cifrar una parte del contenido. Las claves de rotación están protegidas mediante la clave de cifrado de contenido y el cliente sigue obteniendo una única licencia que contenga el CEK para consumir el contenido.

La implementación del empaquetador puede controlar la clave de cifrado de contenido y las claves de rotación utilizadas, así como la frecuencia con la que cambian las claves de rotación.

>[!NOTE]
>
>El contenido empaquetado mediante rotación de clave solo se puede reproducir en los clientes Primetime DRM versión 3.0 o posterior. Es posible que los clientes más antiguos necesiten actualizar para reproducir este contenido.