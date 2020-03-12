---
description: Las siguientes opciones de cifrado se seleccionan en el momento del empaquetado y no se pueden modificar durante la adquisición de la licencia.
seo-description: Las siguientes opciones de cifrado se seleccionan en el momento del empaquetado y no se pueden modificar durante la adquisición de la licencia.
seo-title: Rotación de clave
title: Rotación de clave
uuid: 6ee47c06-9981-4281-b10b-343f8b1e55b7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Rotación de clave{#key-rotation}

Las siguientes opciones de cifrado se seleccionan en el momento del empaquetado y no se pueden modificar durante la adquisición de la licencia.

Durante el empaquetado, el contenido suele cifrarse con la clave de cifrado de contenido (CEK) y el cliente obtiene una licencia que contiene el CEK para consumir el contenido. Cuando se habilita la rotación de claves, la tecla de rotación se utiliza para cifrar el contenido y la clave se puede cambiar para que cada tecla de rotación se utilice solamente para cifrar una porción del contenido. Las claves de rotación están protegidas con la clave de cifrado de contenido y el cliente sigue obteniendo una única licencia que contiene el CEK para consumir el contenido. La implementación del empaquetador puede controlar la clave de cifrado de contenido y las claves de rotación utilizadas, así como la frecuencia con la que cambian las claves de rotación.

El contenido empaquetado mediante la rotación de claves solo se puede reproducir en los clientes de Adobe Access versión 3.0 o posterior. Los clientes más antiguos necesitarían actualizar para reproducir este contenido.
