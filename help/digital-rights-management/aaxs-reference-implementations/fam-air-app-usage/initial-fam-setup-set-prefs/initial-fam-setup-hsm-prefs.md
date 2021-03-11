---
title: Preferencias de HSM
description: Preferencias de HSM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Preferencias de HSM {#hsm-preferences}

Las preferencias de esta ficha solo deben especificarse si la casilla **[!UICONTROL Enable HSM]** está seleccionada en la ficha Empaquetador. En la tabla siguiente se describen estas preferencias:

| Preferencia | Descripción |
|---|---|
| Nombre del archivo de configuración de Sun PKCS#11 | Ruta de acceso completa al archivo de configuración del proveedor de Sun PKCS#11. Consulte la Guía de referencia de Java PKCS#11 en el sitio web de Sun para obtener más información sobre el contenido de este archivo de configuración. |
| Contraseña de partición | La contraseña de la partición HSM especificada en el archivo de configuración PKCS#11. |
| Alias de certificado del servidor de licencias | Alias para el certificado de servidor de licencias emitido por Adobe almacenado en HSM. Este certificado se utiliza para cifrar el CEK durante el empaquetado. Especifique esto en lugar de *Certificado de servidor de licencias* en la pestaña Packager . |
| Alias de certificado de transporte del servidor de licencias | Alias para el certificado de transporte de servidor emitido por Adobe almacenado en HSM. Este certificado se utiliza para proteger las comunicaciones entre el cliente y el servidor de licencias. Especifique esto en lugar de *Certificado de transporte del servidor de licencias* en la pestaña Packager. |
| Alias de Credencial de Packager | Alias para las credenciales de empaquetador emitidas por Adobe (certificado y clave privada) almacenadas en HSM. Se utiliza para firmar los metadatos durante el empaquetado. Especifique esto en lugar de *Credencial del empaquetador* en la pestaña del empaquetador. |
| Alias de Credencial del Servidor de Licencias | Alias para las credenciales de servidor de licencias emitidas por Adobe (certificado y clave privada) almacenadas en HSM. Esta credencial se utiliza para firmar listas de actualización de directivas. Especifique esto en lugar de *Credencial de servidor de licencias* en la pestaña Lista de actualización de directivas. (Es probable que este alias sea el mismo que *Alias de certificado de servidor de licencias*). |

