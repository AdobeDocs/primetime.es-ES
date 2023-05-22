---
description: En esta sección se explica la gramática de la entrada de configuración, se destacan las opciones de entrada válidas y no válidas, y se explica cómo se interpretan los campos opcionales omitidos.
title: Gramática de RBOP
exl-id: 311194ec-e59b-4145-b22b-6983e212fcab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Gramática de RBOP {#rbop-grammar}

En esta sección se explica la gramática de la entrada de configuración, se destacan las opciones de entrada válidas y no válidas, y se explica cómo se interpretan los campos opcionales omitidos.

La gramática de protección de salida basada en resolución se define como una secuencia de reglas, donde cada regla puede tener varios formularios válidos:

```
Rule ::=       
 
    Form 
     
AnotherRule ::=     
 
    DifferentForm 
```

## Aplicación de las reglas gramaticales {#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>Para ayudar a mejorar la legibilidad de la gramática, las siguientes propiedades no se reflejan dentro de la gramática, pero siguen siendo verdaderas:

1. El orden de los pares definidos dentro de los objetos no es fijo; por lo tanto, cualquier permutación de los pares es válida.

   Por ejemplo, si definimos un objeto como este:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   entonces la siguiente estructura también se consideraría válida: =

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. Para cada par dentro de un objeto, se supone que solo existe 1 instancia de ese par dentro de una instancia determinada de un objeto determinado.

   Por ejemplo, si definimos un objeto como este:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   entonces la siguiente instancia no sería válida, ya que hay dos `foo` pares dentro del mismo objeto:

   ```
   { 
     "foo":<Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>,  
   } 
   ```

   Del mismo modo, tener dos objetos como:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   y:

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

   es válido, ya que son instancias independientes del mismo objeto.

1. En el caso de las definiciones en las que se puede elegir una o más secuencias de cadenas, trate las cadenas como un conjunto, en el que las entradas duplicadas se tratan como una sola entrada. Por ejemplo, `["foo", "bar", "foo", "baz"]` es equivalente a `["foo", "bar", "baz"]`

1. Para definir números, se utiliza un espacio entre las reglas (por ejemplo, `Digit Digits`), pero no debe utilizarse ese espacio al aplicar la regla.

   Por ejemplo, si expresamos el número *ciento veintitrés* según la regla NonZeroInteger, debe expresarse como `123` en lugar de `1 2 3`, aunque la regla contenga un espacio entre NonZeroDigit y Digits.

1. Algunas reglas permiten varios formularios. En estos casos, los diferentes formularios se separan mediante la variable `'|'` carácter.

   Por ejemplo, esta regla:

   ```
   Foo ::= "A" | "B" | "C"
   ```

   significa que una instancia de `Foo` puede sustituirse por &quot;A&quot;, &quot;B&quot; o &quot;C&quot;. Esto no debe confundirse con un formulario que abarque varias líneas; se trata de una función para que los formularios más largos sean más legibles.

## La gramática {#section_52189FD66B1A46BA9F8FDDE1D7C8E8E8}

```
PixelBasedOPConfig ::= 
      {} 
    | { "maxPixel": NonNegativeInteger } 
    | { "pixelConstraints": PixelConstraintsSeq } 
    | { "pixelConstraints": PixelConstraintsSeq, 
        "maxPixel": NonNegativeInteger } 
 
PixelConstraintsSeq ::= 
      [] 
    | [ PixelConstraints ] 
 
PixelConstraints ::= 
      PixelConstraint 
    | PixelConstraint, PixelConstraints 
 
PixelConstraint ::= 
      { "pixelCount": NonNegativeInteger } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
         "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
 
DigitalOutputRestrictionsSeq ::= 
      [] 
    | [ DigitalOutputRestrictions ] 
 
DigitalRestrictions ::= 
      DigitalRestriction 
    | DigitalRestriction, DigitalRestrictions 
 
DigitalRestriction ::= 
      { "output": DigitalOutputOption } 
    | { "output": DigitalOutputOption, "hdcp": HDCP } 
 
DigitalOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "REQUIRED" 
    | "NO_PLAYBACK" 
 
HDCP ::= 
    { "major": PositiveInteger, "minor": NonNegativeInteger } 
 
AnalogOutputRestriction ::= 
    { "output": AnalogOutputOption } 
 
AnalogOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "USE_IF_AVAILABLE_ACP" 
    | "USE_IF_AVAILABLE_CGMSA" 
    | "REQUIRED" 
    | "REQUIRED_ACP" 
    | "REQUIRED_CGMSA" 
    | "NO_PLAYBACK" 
 
OTAOutputRestriction ::= 
    { "whitelist": OTAWhitelistSeq } 
 
OTAWhitelistSeq ::= 
      [] 
    | [ OTAWhitelist ] 
 
OTAWhitelist ::= 
      OTAConnectionType 
    | OTAConnectionType, OTAWhitelist 
 
OTAConnectionType ::= 
      "MIRACAST" 
    | "AIRPLAY" 
    | "WIDI" 
    | "DLNA" 
 
NonNegativeInteger ::= 
      Digit 
    | NonZeroDigit Digits 
 
PositiveInteger ::= 
      NonZeroDigit 
    | NonZeroDigit Digits 
 
Digits ::= 
      Digit 
    | Digit Digits 
 
Digit ::= 
      0 
    | NonZeroDigit

NonZeroDigit ::= 
      1 
    | 2 
    | 3 
    | 4 
    | 5 
    | 6 
    | 7 
    | 8 
    | 9
```

## Semántica: configuraciones legales pero no válidas {#section_709BE240FF0041D4A1B0A0A7544E4966}

El *Configuración de protección de salida de muestra* Este tema presenta una configuración válida junto con su significado semántico. La sección anterior de *esta* Este tema presenta las reglas gramaticales para las configuraciones. Aunque la gramática ayuda a garantizar la corrección sintáctica, hay configuraciones legales sintácticas que no son semánticamente correctas (es decir, no son lógicas). Esta sección presenta las configuraciones que son *sintácticamente* legal, pero *semánticamente* incorrecto. Tenga en cuenta que los ejemplos de esta sección se han reducido a la estructura mínima necesaria para ilustrar el escenario en cuestión.

* No es válido definir varias restricciones de píxeles con el mismo recuento de píxeles.

   ```
   {  
     "pixelConstraints":  
       [  
         { "pixelCount": 720 }  
       ]  
    }  
   ```

* Un número de píxeles no debe superar la resolución de píxeles máxima especificada.

   ```
   { 
     "maxPixel": 720, 
     "pixelConstraints": 
       [ 
         {"pixelCount": 1080} 
       ] 
   } 
   ```
