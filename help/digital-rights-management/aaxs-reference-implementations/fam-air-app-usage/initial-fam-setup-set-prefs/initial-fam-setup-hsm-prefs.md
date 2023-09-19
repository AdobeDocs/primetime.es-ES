---
title: Preferencias de HSM
description: Preferencias de HSM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Preferencias de HSM {#hsm-preferences}

Solo es necesario especificar las preferencias de esta pestaña si la variable **[!UICONTROL Enable HSM]** La casilla de verificación está seleccionada en la pestaña Packager. En la tabla siguiente se describen estas preferencias:

| Preferencia | Descripción |
|---|---|
| Nombre del archivo de configuración Sun PKCS#11 | Ruta de acceso completa al archivo de configuración del proveedor Sun PKCS#11. Consulte la Guía de referencia PKCS#11 de Java en el sitio web de Sun para obtener más información sobre el contenido de este archivo de configuración. |
| Contraseña de partición | La contraseña para la partición HSM especificada en el archivo de configuración PKCS#11. |
| Alias de certificado del servidor de licencias | Alias para el certificado de servidor de licencias emitido por el Adobe almacenado en HSM. Este certificado se utiliza para cifrar el CEK durante el empaquetado. Especifique esto en lugar de *Certificado de servidor de licencias* en la pestaña Packager. |
| Alias de certificado de transporte de servidor de licencias | Alias para el certificado de transporte de servidor emitido por Adobe almacenado en HSM. Este certificado se utiliza para proteger las comunicaciones entre el cliente y el servidor de licencias. Especifique esto en lugar de *Certificado de transporte del servidor de licencias* en la pestaña Packager. |
| Alias de credencial de empaquetador | Alias para la credencial de empaquetador emitida por Adobe (certificado y clave privada) almacenada en HSM. Se utiliza para firmar los metadatos durante el empaquetado. Especifique esto en lugar de *Credencial del empaquetador* en la pestaña Packager. |
| Alias de credenciales del servidor de licencias | Alias para la credencial del servidor de licencias emitida por el Adobe (certificado y clave privada) almacenada en HSM. Esta credencial se utiliza para firmar listas de actualización de directivas. Especifique esto en lugar de *Credenciales del servidor de licencias* en la pestaña Lista de actualización de directivas. (Este alias probablemente será el mismo que *Alias de certificado del servidor de licencias*.) |
