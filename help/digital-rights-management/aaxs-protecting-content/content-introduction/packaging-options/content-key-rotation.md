---
description: Las siguientes opciones de cifrado se seleccionan en el momento del empaquetado y no se pueden modificar durante la adquisición de la licencia.
title: Rotación de clave
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Rotación de clave{#key-rotation}

Las siguientes opciones de cifrado se seleccionan en el momento del empaquetado y no se pueden modificar durante la adquisición de la licencia.

Durante el empaquetado, el contenido se cifra normalmente mediante la clave de cifrado de contenido (CEK) y el cliente obtiene una licencia que contiene la CEK para consumir el contenido. Cuando se habilita la rotación de claves, la clave de rotación se utiliza para cifrar el contenido y la clave se puede cambiar para que cada clave de rotación se utilice únicamente para cifrar una parte del contenido. Las claves de rotación están protegidas mediante la clave de cifrado de contenido, y el cliente sigue obteniendo una sola licencia que contiene el CEK para consumir el contenido. La implementación del empaquetador puede controlar la clave de cifrado de contenido y las claves de rotación utilizadas, así como la frecuencia con la que cambian las claves de rotación.

El contenido empaquetado con rotación de clave sólo se puede reproducir en clientes de Adobe Access versión 3.0 y posterior. Los clientes más antiguos necesitarían actualizarse para reproducir este contenido.
