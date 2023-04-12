---
title: Función de metadatos de usuario
description: Función de metadatos de usuario
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 0%

---



# Metadatos de usuario {#user-metadata}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>
</br>

## Introducción {#intro}

La función Metadatos de usuario permite a los programadores acceder a diferentes tipos de datos específicos del usuario que mantienen los MVPD.  Los tipos de metadatos de usuario incluyen códigos postales, clasificaciones parentales, ID de usuario y mucho más.  *Usuario* metadata es una extensión de la disponible anteriormente *static* metadatos (TTL token de autenticación, TTL token de autorización e ID de dispositivo).


Puntos clave de metadatos de usuario:

- Transferido a la aplicación del programador durante los flujos de autenticación y autorización
- Los valores se guardan en el token
- Los valores se pueden normalizar si diferentes MVPD proporcionan datos en diferentes formatos
- Algunos parámetros se pueden cifrar con la clave del programador (p. ej. código postal)
- Los valores específicos están disponibles por Adobe a través de un cambio de configuración

## Obtención de metadatos de usuario {#obtaining}

Los metadatos de usuario están disponibles para los programadores a través de AccessEnabler `getMetadata()` y a través de la función `/usermetadata` en la API sin cliente.  Consulte la documentación de la API de plataforma para obtener más información sobre el uso de `getMetadata()` y su llamada de retorno correspondiente `setMetadataStatus()` (o para los extremos y parámetros utilizados en la API sin cliente).

Los programadores obtienen metadatos suministrando una clave para el tipo de metadatos que desean obtener: `getMetadata(key)`.  

Los metadatos se devuelven de la siguiente manera: `setMetadataStatus(key, encrypted, data)`:

| Parámetro | Tipo | Descripción |
| ----------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `key` | Cadena | Especifica el tipo de metadatos solicitados |
| `encrypted` | Booleano | Un indicador booleano que señala si el &quot;valor&quot; está cifrado o no. Si esto es &quot;true&quot;, entonces &quot;value&quot; será en realidad una representación JSON Web Encrypted del valor real. |
| `data` | Objeto | Un objeto JSON que contiene la representación de los metadatos |

 

La estructura del parámetro data, los valores varían de un tipo a otro:

| Clave | Tipo de valor | Ejemplo | Descripción |
| --- | --- | --- | --- |
| `zip` | Matriz JSON | \[&quot;77754&quot;, &quot;12345&quot;\] | Código postal |
| `householdID` | Cadena JSON | &quot;1o7241p&quot; | Identificador del hogar. Si el MVPD no admite subcuentas, esto será idéntico al `userID` |
| `maxRating` | Objeto JSON | { MPAA: &quot;NR&quot;, <br>  VCHIP: &quot;X&quot;,  <br>  URL: &quot;http://manage.my/parental&quot; } | Clasificación parental máxima para el usuario |
| `userID` | Cadena JSON | &quot;1o7241p&quot; | El identificador de usuario. En el caso de que un MVPD admita subcuentas y el usuario no sea la cuenta principal, `userID` será diferente a `householdID`. |
| `channelID` | Matriz JSON | \[&quot;channel-1&quot;, &quot;channel-2&quot; \] | Una lista de canales que un usuario puede ver |
| `is_hoh` | Cadena JSON | &quot;1&quot; | Un indicador que identifica si un usuario es cabeza de familia |
| `encryptedZip` | Cadena JSON | &quot;&quot; | Comcast expone el código postal cifrado |
| `typeID` | Cadena JSON | Principal | Un indicador que identifica si la cuenta de usuario es cuenta principal/secundaria |
| `primaryOID` | Cadena JSON | &quot;uuidd1e19ec9-012c-124f-b520-acaf118d16a0&quot; | Identificador del hogar. If `typeID` es principal, contiene el valor de la variable `userID` |
| hba_status | Booleano | &quot;true&quot; &quot;false&quot; | Un indicador booleano que indica si la autenticación basada en el hogar está habilitada para una integración determinada |
| allowMirroring | Booleano | &quot;true&quot; &quot;false&quot; | Indica si el reflejo de pantalla está permitido para este dispositivo o no |

>[!NOTE]
>
> **Nota:** Si el parámetro de datos está cifrado, como suele suceder con la variable **clave zip**, la representación de la clave de metadatos será una cadena JSON en lugar de una matriz o un objeto.


**Importante:** Los metadatos de usuario disponibles para un programador dependen de lo que un MVPD ponga a disposición.  Los acuerdos legales deben firmarse con MVPD antes de que los metadatos confidenciales del usuario (como el código postal) estén disponibles en el entorno de producción.

</br>


| Nombre | Detalles | Requiere cifrado | Comentarios |
| --- | --- | --- | --- |
| ID de usuario | Según lo previsto por la MVPD | No | Este es el valor que luego se coloca en hash mediante el Adobe y se expone en el token de medios y en la llamada de retorno sendTrackingData() .<br><br>El hash en este caso se hizo por razones históricas<br><br>Este ID puede ser un ID de hogar o de subcuenta. Normalmente no se especifica, solo se trata del ID vinculado al inicio de sesión que se utilizó en ese momento (que puede ser una cuenta principal o una subcuenta) |
| ID de usuario ascendente | Proporcionado por el MVPD para ser utilizado solamente para flujos de monitorización de concurrencia | No | Este valor se utiliza al aplicar límites de concurrencia en sitios y aplicaciones de MVPD y Programador. <br><br>El ID también puede contener directivas de monitorización de concurrencia<br><br>Para la mayoría de los MVPD, este valor es igual al ID de usuario |
| ID de usuario del hogar | Proporcionado por el MVPD para ser utilizado principalmente para flujos de Control Parental | No | ID que permite a los programadores comprender el uso de la casa frente al de la subcuenta.<br><br>A veces se utiliza como un sustituto del Control parental si no hay disponibles clasificaciones verdaderas (si el usuario ha iniciado sesión con la cuenta doméstica, puede ver, de lo contrario no se mostraría el contenido clasificado)<br><br>Hay muchas variaciones en los MVPD sobre cómo se representa esto: ID de usuario del hogar, ID del jefe de familia, indicador del jefe de familia, etc. |
| Jefe de familia | Indicador que señala si la cuenta corriente es cabeza de familia o no | No | consulte arriba |
| ID de tipo/ID principal | Identificadores de cuenta del hogar | No | Indicadores específicos de AT&amp;T para el jefe de familia.<br><br>Tipo ID = Indicador que identifica si la cuenta de usuario es principal/secundaria<br><br>OID primario = Identificador del hogar. Si TypeID es primario, contendrá el valor de userID |
| Clasificación máxima | Clasificación máxima permitida para la cuenta actual | No | Permite a los programadores filtrar el contenido que no es adecuado para la cuenta.<br><br>Tiene clasificaciones MPAA o VCHIP |
| Línea de canal arriba | Lista de canales disponibles en el paquete del usuario | No | Se usa para permitir/eliminar rápidamente varios canales de portales que agregan varias redes</br></br> *Tenga en cuenta que la autorización de comprobación previa generalmente permite una mayor flexibilidad para este uso y debe utilizarse en su lugar* <br><br>La especificación OLCA permite esto como una AttributeStatement en la respuesta AuthN |
| Estado del HBA | Indica si se ha producido autenticación mediante HBA | No |  |
| Código postal | Código postal de facturación del usuario | Sí | Se utiliza para la emisión o para eventos deportivos.<br><br>También se puede proporcionar con la respuesta de AuthZ para actualizaciones rápidas<br><br>Datos confidenciales, necesita acuerdos legales MVPD |
| Código postal cifrado | Código postal de facturación del usuario (Comcast) | Sí | Como se muestra arriba pero cifrado por Comcast |
| Idioma | Configuración de idioma del usuario | No | Se utiliza para mostrar los mensajes de acuerdo con las preferencias del usuario |
| Permitir creación de reflejo | Indica si el reflejo de pantalla está permitido para este dispositivo o no | No |  |



## Metadatos disponibles {#available_metadata}

La siguiente tabla muestra el estado actual de los metadatos de usuario en el ecosistema de autenticación de Adobe Primetime:


|  | **Información legal **<br><br>**Acuerdo **<br><br>**Firmado (solo zip)** | **ID de usuario **<br><br>**en AuthN** | **Zipcode **<br><br>**en AuthN/Z** | **Clasificación **<br><br>**en AuthN/Z** | **Hogar **<br><br>**ID en AuthN/Z** | **ID de canal en AuthN** | **Jefe de familia en AuthN** | **Escriba ID en AuthN** | **OID principal en AuthN** | Idioma | UserID ascendente **en AuthN** | Estado del HBA | OnNet | inHome | Permitir creación de reflejo en AuthZ | **Notas** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Nombre formal** | n.a | `userID` | `zip` | `maxRating` | `householdID` | `channelID` | is_hoh | typeID | primaryOID | language | upstreamUserID | hba_status | onNet | inHome | allowMirroring | 1. Para AuthN - OiosamlMetadataParser debe cambiarse para que todos los analizadores tengan este nuevo atributo habilitado <br>2.  Para AuthZ: no hay forma genérica, ya que la implementación de la autorización es específica de MVPD |
| **Cifrado obligatorio** | n.a | **No** | **Sí** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** |  |
| **Sensible** | n.a | **No** | **Sí** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** |  |  |
| **IdP de Adobe** | **Sí** | **Sí** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **Sí** | **Sí** | **Sí** | **Sí** | **No** | **Sí** | **No** | **No** | **No** | **No** | No se necesita ningún acuerdo legal, se puede habilitar. |
| **Synacor** | **Sí** | **Sí** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **Sí** | **Sí** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** | **Acuerdo jurídico que no cubre todos los MVPD reenviados a través de proxy.**   <br>Este es un soporte genérico para Synacor, posiblemente no resumido en todos sus MVPD. |
| Dish | **No** | **Sí** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **Sí** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** | Comparte la misma lista que todos los MVPD de Synacor, además de upstreamUserID. |
| Comcast | **No** | **Sí** | **No** | **Sí (solo AuthZ)** | **Sí (solo AuthZ)** | **No** | **No** | **No** | **No** | **No** | **Sí** | **Sí** | **No** | **No** | **No** |  |
| **AT&amp;T** | **Sí** | **Sí** | **Sí (solo AuthN)** | **No** | **Sí (solo AuthN)** | **No** | **No** | **Sí** | **Sí** | **No** | **Sí** | **No** | **No** | **No** | **No** | Acuerdo jurídico firmado. |
| **Cablevision** | **Sí** | **Sí** | **Sí (solo AuthN)** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** | Acuerdo jurídico firmado. |
| **HTC** | **No** | **Sí** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** |  |
| **Massilon proxy** | **Sí** | **Sí** | **Sí (solo AuthN)** | **No** | **Sí (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** | Acuerdo jurídico firmado. |
| **Eliminación de proxy** | **Sí** | **Sí** | **Sí (solo AuthN)** | **Sí (solo AuthZ)** | **No** | **No** | **No** | **No** | **No** | **Sí** | **Sí** | **No** | **No** | **No** | **No** | Acuerdo jurídico firmado. |
| Rogers | **No** | **Sí** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** |  |
| RCN | **Sí** | **Sí** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** |  |
| Carta | **Sí** | **Sí** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** |  |
| Verizon | **No** | **Sí** | **Sí (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Sí** | **Sí** | **No** | **No** | **No** |  |
| Eastlink | **No** | **Sí** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **Sí** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** |  |
| GLDS de proxy | **No** | **Sí** | **Sí (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** |  |
| DTV | **Sí** | **Sí** | **Sí (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** |  |
| COX | **No** | **Sí** | **Sí (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** |  |
| Cogeco | **No** | **Sí** | **Sí (solo AuthN)** | **No** | **Sí (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** |  |
| Videotron | **No** | **Sí** | **Sí (solo AuthN)** | **No** | **Sí*** | **No** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** | Expone householdID con el mismo valor que userID |
| Espectro | **Sí** | **Sí** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **Sí (solo AuthN)** | **No** | **No** | **No** | **No** | **No** | **Sí** | **Sí** | **No** | **No** | **Sí** |  |
| **Todos los demás **<br><br>**MVPD** | **No** | **Sí** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Sí** | **No** | **No** | **No** | **No** | **Aún no hay acuerdo legal, los metadatos confidenciales no están disponibles para la producción.**  <br>Para todos los MVPD, el ID de usuario está disponible sin trabajo adicional. |


La lista de tipos de metadatos de usuario se ampliará a medida que se pongan nuevos tipos a disposición y se añadan al sistema de autenticación de Adobe Primetime.

## Ejemplos de código {#code_samples}

- [Ejemplo de código 1](#code_sample1)
- [Ejemplo de código 2 (Mock getMetadata)](#code_sample2)


### Ejemplo de código 1 {#code_sample1}

```
    // Assuming a reference to the AccessEnabler has been previously obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
      if(status ==1) {
        // User is authenticated, request metadata
        ae.getMetadata("zip");
        ae.getMetadata("maxRating");
      } else {
        ...
      }
    }
     
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
      if(encrypted) {
        // The metadata value is encrypted
        // Needs to be decrypted by the programmer
         data = decrypt(data);
      }
      alert(key + "=" + data);
    }
```
 

### Ejemplo de código 2 (Mock getMetadata) {#code_sample2}

```
    // Assuming a reference to the AccessEnabler has been
    //   previously obtained and stored in the "ae" variable
     
    // Mock the getMetadata() method
    var aeMock = {
        getMetadata: function(key) {
          var data = null;
          // Set mock data based on the received key,
          // according to the format in the spec
          switch(key) {
            case 'zip': 
              data = [ "1235", "23456" ];
              break;
            case 'maxRating': 
              data = { "MPAA": "PG-13", "VCHIP": "TV-14" };
              break;
            default:
              break;
          }
          // Call the metadata status just like AccessEnabler does
          setMetadataStatus(key, false, data);
        }
     }
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
      if (status == 1) {
        // User is authenticated, request metadata using mock object
        aeMock.getMetadata("zip");
        aeMock.getMetadata("maxRating");
      } else {
        ...
      }
    }
     
    // Implement the  setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
      if (encrypted) {
        // The metadata value is encrypted, so it
        //   needs to be decrypted by the programmer
         data = decrypt(data);
      }
      alert(key + "=" + data);
    }
```
 

Para obtener más información sobre su plataforma en particular, o para obtener información sobre cómo se procesan los metadatos de usuario en el lado de MVPD, consulte el vínculo correspondiente en Información relacionada a continuación.  

<!---

## Related Information {#related}

- ActionScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- JavaScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- iOS - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaStatus)
- Android - [getMetadata()](#getMetadata), [setMetadataStatus()](#setMetadaStatus)
- Clientless - [AuthN Metadata](#authn_metadata)
- [MVPD Integration Guide: User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
-->
