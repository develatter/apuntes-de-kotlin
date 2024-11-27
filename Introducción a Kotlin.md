<!--# Índice Completar
- [Variables y constantes](#variables-y-constantes)
- [Inferencia de tipos](#inferencia-de-tipos)
- [Tipos de datos](#tipos-de-datos)
    - [String](#string)
        - [Literales de Cadenas](#literales-de-cadenas)
        - [Formato de String](#formato-de-string)
            - [Formateo de cadenas con `String.format()` en Kotlin](#formateo-de-cadenas-con-stringformat-en-kotlin)
            - [Especificadores de formato](#especificadores-de-formato)
            - [Ejemplos](#ejemplos)
            - [Ventajas y precauciones](#ventajas-y-precauciones)
    - [Números](#números)
        - [Tipos de números enteros](#tipos-de-números-enteros)
        - [Tipos de números de decimales](#tipos-de-números-de-decimales)
        - [Conversión de tipos numéricos](#conversión-de-tipos-numéricos)
        - [Operaciones con números](#operaciones-con-números)
        - [Constantes literales en números](#constantes-literales-en-números)
            - [Constantes literales para valores integrales](#constantes-literales-para-valores-integrales)
            - [Constantes literales para valores de punto flotante](#constantes-literales-para-valores-de-punto-flotante)
            - [Uso de guiones bajos para mejorar la legibilidad](#uso-de-guiones-bajos-para-mejorar-la-legibilidad)
            - [Constantes literales para enteros sin signo](#constantes-literales-para-enteros-sin-signo)
            - [Operaciones a nivel de bits](#operaciones-a-nivel-de-bits)
    - [Lógicos](#lógicos)
    - [Caracteres](#caracteres)
    - [Arrays](#arrays)
        - [Crear Arrays](#crear-arrays)
            - [Con la función arrayOf()](#con-la-función-arrayof)
            - [A partir de un rango](#a-partir-de-un-rango)
            - [Con el constructor Array](#con-el-constructor-array)
        - [Acceso y modificación](#acceso-y-modificación)
        - [Matrices](#matrices)
        - [Comparar arrays](#comparar-arrays)
- [Operadores](#operadores)
- [Null Safety](#null-safety)
	- [Operador seguro](#operador-seguro-)
	- [Operador Elvis](#operador-elvis-)
	- [Operador de no nulidad](#operador-de-no-nulidad-)
- [Rangos](#rangos)
- [Control de flujo](#control-de-flujo)
	- [Condicionales](#condicionales)
		- [if - else if - else](#if---else-if---else)
		- [when](#when)
	- [Bucles](#bucles)
	    - [for](#for)
	    - [while](#while)
	    - [do-while](#do-while)
---
-->
# Variables y constantes

Kotlin permite declarar variables[^1] usando las siguientes palabras reservadas: **val** (value) y **var** (variable).

_`val`_ permite declarar variables inmutables (constantes):

```Kotlin
val nombre = "Pepe"

val numero = 5

nombre = "Jose" // Error, porque nombre es inmutable.

numero = 5 // Error, porque numero es inmutable.
```

_`var`_ , en cambio, permite declarar variables mutables. Es decir, variables a las que se les pueden reasignar valores a lo largo del código.  

```Kotlin
var nombre = "Pepe"

var numero = 5

nombre = "Jose"

numero = 5
```

Se observa que en ningún caso se indica el tipo de dato de cada variable. Esto no quiere decir que no tengan tipo. Es más, Kotlin tiene tipado estático, es decir, que cada variable tiene un tipo de dato asociado que no cambia:

```Kotlin
var nombre = "Pepe" // String

var numero = 5 // Int

nombre = 4.5 // Error, porque nombre es de tipo String.

numero = 5.0 // Error, porque numero es de tipo Int.
```

Puedes consultar los tipos de datos que maneja Kotlin en la documentación oficial[^2].

[^1]: Basic syntax | Kotlin. (s. f.-b). Kotlin Help. [https://kotlinlang.org/docs/basic-syntax.html#variables]( https://kotlinlang.org/docs/basic-syntax.html#variables)
[^2]: Basic types | Kotlin. (s. f.). Kotlin Help. [https://kotlinlang.org/docs/basic-types.html](https://kotlinlang.org/docs/basic-types.html)

---
# Inferencia de tipos

En los casos anteriores hemos declarado variables sin indicar en ningún caso su tipo. Esto se debe a que las variables asumen el tipo de dato del valor que se les asigna. A esto se le conoce como **inferencia de tipo de dato**. En el ejemplo anterior se indican algunos tipos de datos inferidos en los comentarios:

```Kotlin
var nombre = "Pepe" // String

var entero = 5 // Int

val esCierto = true // Boolean
 ```
  
También es posible declarar una variable sin inicializar. En este caso se ha de indicar qué tipo de dato va a almacenar, ya que las variables deben tener asociado un tipo de dato en el momento en el que se declaran:

```Kotlin
var nombre: String

var numero: Int

nombre = "Jose"

numero = 5
```
# Tipos de datos

Hay que destacar que en Kotlin no existen tipos de datos primitivos, como ocurre en Java. Es decir, el int de Java no se encuentra en Kotlin.

Esto se debe a que todo en Kotlin es un objeto, incluyendo los tipos de datos.

```Kotlin
var nombre = "Pepe" // String

val enteroLargo = 123456L // Long

val decimalDouble = 1.32 // Double

val decimalFloat = 5.5F // Float

var entero = 5 // Int

val hexadecimal = 0xAB // Int

val binary = 0b01010101 // Int
```

Esto supone que el tipo de dato de una variable determina el tipo de métodos y operaciones que se pueden realizar con ella. Los tipos de datos básicos que maneja Kotlin son: Strings, enteros, decimales y booleanos. 

A partir de estos tipos de datos podemos construir tipos de datos más complejos (como veremos más adelante).

> [!NOTE]
> **¿Cómo identificar el tipo de dato?**
Para ver el tipo de dato de una variable, se puede usar la propiedad abstracta [simpleName](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.reflect/-k-class/simple-name.html) de la siguiente manera:
>```Kotlin
>variable::class.simpleName

## String

Las cadenas en Kotlin se representan con el tipo **String** y son inmutables.
Se expresan entre comillas dobles _(")_.
  
```kotlin
var nombre = "Pepe" // String

println(nombre::class.simpleName)

//—-----------------------------------
//~$ String
```
  
Un String sigue siendo una secuencia de caracteres, al igual que en Java, por lo que Kotlin permite recorrerla carácter a carácter de forma sencilla:
  
```kotlin
var nombre = "Pepe"

for (caracter in nombre ) {

    println(caracter)

}
//—-----------------------------------
//~$ P
//~$ e
//~$ p
//~$ e
```
  
Que sea inmutable significa al asignarle un valor, no se pueden cambiar. Si se reasigna otra cadena a una variable String, la cadena anterior se desreferencia y el __garbage collector__ se encargará de eliminarla. 

Esto también implica que cualquier método que ejecute, no cambiará el valor de la cadena. En su lugar creará otra cadena en memoria con el resultado de dicho método:

  ```Kotlin
var nombre = "Pepe"

println(nombre.uppercase()) // el resultado no se guarda en nombre

println(nombre)

//—-----------------------------------
//~$ PEPE
//~$ Pepe
 ```
  
Puedes concatenar cadenas usando el operador +, pero es preferible usar plantillas de cadenas o cadenas multilínea. Para hacer cadenas mutables, al igual que en Java, podemos usar la clase [StringBuilder](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-string-builder/).

```Kotlin
var nombre = "Pepe"

println("Buenos días, " + nombre) // 👍

println("Buenos días, $nombre") // 👍👍👍👍

//—-----------------------------------
//~$ Buenos días, Pepe
//~$ Buenos días, Pepe
 ```
  
Cuando usamos el operador _“+”_ hablamos de  __concatenación__. Cuando usamos plantillas para _referenciar_ a una variable, hablamos de _expansión de variables_. Las plantillas, también llamadas **String Templates**, son muy útiles, ya que no solo nos permiten llamar al valor de una variable sino que también es posible usarlas para evaluar expresiones. 

Para evaluar una expresión con una plantilla debemos rodearla entre llaves _`(${expresión})`_.
```Kotlin 


val uno = 1

val dos = 2

println("La suma de $uno y $dos es ${uno + dos}")

//—----------------------------
//~$ La suma de 1 y 2 es 3
```
[Prueba este código ▶](https://pl.kotl.in/nKK9sA8gF)

## Literales de Cadenas

Kotlin tiene [cadenas escapadas](https://kotlinlang.org/docs/strings.html#escaped-strings) (contienen caracteres escapados con **`\`**) y [cadenas multilínea](https://kotlinlang.org/docs/strings.html#multiline-strings) (delimitadas por triple comillas).

- __Cadenas escapadas__: estas cadenas contienen caracteres especiales que implican una acción: retorno de carro, tabulador, etc.
  
```Kotlin
val saludo = "Hola, Pepe!\nCómo ha ido el día?"

println(saludo)

//—-----------------------------------
//~$ Hola, Pepe!
//~$ Cómo ha ido el día?
```

- **Cadenas multilínea**: permiten escribir un texto sin necesidad de usar caracteres escapados. Para ello, dicha cadena se delimita por triples comillas dobles.
  
```Kotlin
val saludo = """Hola, Pepe!

Cómo ha ido el día?""" // no necesita \n

println(saludo)

//—-----------------------------------
//~$ Hola, Pepe!
//~$ Cómo ha ido el día?
```


Un método muy útil para evitar problemas de formato con las cadenas multilínea es __`.trimIndent()`__, el cual nos permite eliminar todos los espacios en blanco al principio de cada línea del String. De esta forma podemos escribir el literal de forma más legible sin que eso afecte a lo que se muestra por pantalla.
  
  ```Kotlin
val saludo = """
				Hola, Pepe!
				Cómo ha ido el día?
			 """.trimIndent()            //Ignora espacios 

println(saludo)

//—-----------------------------------
//~$ Hola, Pepe!
//~$ Cómo ha ido el día?
```


## Formato de String

La función [String.format()](https://kotlinlang.org/docs/strings.html#string-formatting) permite formatear cadenas con especificadores de formato, similar a Java.
### Formateo de cadenas con `String.format()` en Kotlin

La función `String.format()` acepta una cadena de formato (_con placeholders_) y uno o más argumentos. La cadena de formato contiene un marcador de posición o placeholder (_indicado por `%`_) para un argumento específico, seguido de especificadores de formato, los cuales veremos más adelante.  
#### Especificadores de formato
Los especificadores de formato son instrucciones de formateo para el argumento correspondiente, y están compuestos por:  
- **Flags:** Opciones de alineación y formato.  
- **Width (ancho):** Longitud mínima del resultado.  
- **Precision (precisión):** Número de decimales o caracteres a mostrar.  
- **Conversion type (tipo de conversión):** Especifica el tipo de dato (entero, flotante, cadena, etc.).  

Algunos especificadores comunes incluyen:  
- `%d` para enteros.  
- `%f` para números de punto flotante.  
- `%s` para cadenas.  

También puedes usar la sintaxis `argument_index$` para referenciar el mismo argumento varias veces en diferentes formatos dentro de la misma cadena.

> [!TIP]
> Para una lista completa de especificadores de formato, consulta la [documentación de la clase Formatter de Java](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Formatter.html).

#### Ejemplos

```kotlin
// Formatea un entero, añadiendo ceros a la izquierda hasta 7 caracteres
val integerNumber = String.format("%07d", 31416)
println(integerNumber)
// Salida: 0031416

// Formatea un número decimal para mostrar un signo '+' y 4 decimales
val floatNumber = String.format("%+.4f", 3.141592)
println(floatNumber)
// Salida: +3.1416

// Formatea dos cadenas en mayúsculas, cada una ocupando un marcador de posición
val helloString = String.format("%S %S", "hello", "world")
println(helloString)
// Salida: HELLO WORLD

// Mete el número negativo entre paréntesis y luego lo repite
val negativeNumberInParentheses = String.format("%(d means %1\$d", -31416)
println(negativeNumberInParentheses)
// Salida: (31416) means -31416

```
[Prueba este código ▶](https://pl.kotl.in/5DJCOOZ5x?theme=darcula)

#### Ventajas y precauciones

La función `String.format()` ofrece una funcionalidad similar a las plantillas de cadenas, pero es más versátil debido a las opciones de formateo adicionales.

Además, puedes asignar la cadena de formato a una variable, lo cual es útil cuando el formato debe cambiar, como en casos de localización que dependen del idioma o región del usuario.

> [!CAUTION]
>Al usar `String.format()`, ten cuidado de no equivocarte con la cantidad o posición de los argumentos y los placeholders.


## Números
### Tipos de números enteros  

Para los números[^8] enteros, existen cuatro tipos con diferentes tamaños y rangos de valores: 

| Tipo  | Tamaño (bits) | Valor mínimo                      | Valor máximo                        |     |
| ----- | ------------- | --------------------------------- | ----------------------------------- | --- |
| Byte  | 8             | -128                              | 127                                 |     |
| Short | 16            | -32,768                           | 32,767                              |     |
| Int   | 32            | -2,147,483,648 (-2³¹)             | 2,147,483,647 (2³¹ - 1)             |     |
| Long  | 64            | -9,223,372,036,854,775,808 (-2⁶³) | 9,223,372,036,854,775,807 (2⁶³ - 1) |     |

Cuando inicializas una variable sin especificar explícitamente el tipo, el compilador infiere automáticamente el tipo más pequeño que pueda representar el valor, comenzando desde **Int**. Si el valor excede el rango de **Int**, el tipo será **Long**. Para especificar un valor como **Long**, añade el sufijo `L` al valor.  

```kotlin
val one = 1 // Int  
val threeBillion = 3000000000 // Long  
val oneLong = 1L // Long  
val oneByte: Byte = 1  
```

> [!TIP]
> Además de los tipos enteros, Kotlin también proporciona tipos enteros sin signo. Para más información, consulta los [tipos enteros sin signo](https://kotlinlang.org/docs/unsigned-integers.html).  

---
### Tipos de números de decimales 
Kotlin también proporciona los tipos de números reales **Float** y **Double**, que cumplen con el estándar IEEE 754. 

| Tipo   | Tamaño (bits) | Bits significativos | Bits de exponente | Dígitos decimales |  
|--------|---------------|---------------------|--------------------|-------------------|  
| Float  | 32            | 24                  | 8                  | 6-7               |  
| Double | 64            | 53                  | 11                 | 15-16             |  

Puedes inicializar variables de tipo **Double** y **Float** con números que tengan una parte fraccionaria separada por un punto (`.`). El compilador infiere el tipo **Double** para estos valores:  

```kotlin
val pi = 3.14 // Double  
val oneDouble = 1.0 // Double  
```

Para especificar explícitamente un valor como **Float**, añade el sufijo `f` o `F`. Si el número tiene más de 6-7 dígitos decimales, será redondeado:  

```kotlin
val e = 2.7182818284 // Double  
val eFloat = 2.7182818284f // Float, valor real: 2.7182817  
```

---
### Conversión de tipos numéricos  
En Kotlin, **no hay conversiones automáticas** entre tipos numéricos más pequeños y más grandes. Por ejemplo, si una función admite como parámetro un Double, no podremos invocarla con argumentos de tipo _Int_ o _Double_:  

```kotlin
fun main() { 
	fun printDouble(d: Double) { 
		print(d) 
	} 

	val i = 1 
	val d = 1.0 
	val f = 1.0f 
	
	printDouble(d) 
	// printDouble(i) // Error: Type mismatch 
	// printDouble(f) // Error: Type mismatch 
}
```

Todos los tipos numéricos soportan conversiones a otros tipos mediante funciones como
- `toByte(): Byte`
- `toShort(): Short`
- `toInt(): Int`
- `toLong(): Long`
- `toFloat(): Float` 
- `toDouble(): Double`

---
### Operaciones con números  
Kotlin soporta las operaciones aritméticas estándar: `+`, `-`, `*`, `/`, `%`. Estas operaciones están sobrecargadas para realizar las conversiones necesarias automáticamente:  

```kotlin
println(1 + 2)  
println(2_500_000_000L - 1L)  
println(3.14 * 2.71)  
println(10.0 / 3)  
```

Para obtener divisiones precisas entre enteros, convierte explícitamente uno de los operandos a un tipo decimal:  

```kotlin
val x = 5 / 2.toDouble()  
println(x == 2.5)  
```

---
### Constantes literales en números  

En Kotlin, puedes usar diferentes tipos de constantes literales para números integrales y de punto flotante. 

----
#### Constantes literales para valores integrales

- **Decimales**: Se escriben directamente como números.  
  
```kotlin
val decimalValue = 123
```  
  
- **Long**: Se identifican con una `L` al final del número.  
  
```kotlin
val longValue = 123L
```  
  
- **Hexadecimales**: Se prefijan con `0x` o `0X`.

```kotlin
val hexValue = 0x0F
```  

- **Binarios**: Se prefijan con `0b` o `0B`. 
   
```kotlin
val binaryValue = 0b00001011
```  

> [!WARNING]
> **Octales**:
> No están soportados en Kotlin.  

---
#### Constantes literales para valores de punto flotante
- **Double**: Es el tipo predeterminado para valores con parte decimal o en notación científica. 
   
```kotlin
val doubleValue = 123.5
val scientificDouble = 123.5e10
```  
  
- **Float**: Se identifican con un sufijo `f` o `F`.  
  
```kotlin
val floatValue = 123.5f
```  

---
#### Uso de guiones bajos para mejorar la legibilidad
Puedes usar guiones bajos (`_`) en números para hacerlos más legibles. Esto no afecta el valor numérico.  

```kotlin
val oneMillion = 1_000_000
val creditCardNumber = 1234_5678_9012_3456L
val socialSecurityNumber = 999_99_9999L
val hexBytes = 0xFF_EC_DE_5E
val bytes = 0b11010010_01101001_10010100_10010010
```  

---
#### Constantes literales para enteros sin signo
Kotlin también admite constantes literales específicas para enteros sin signo. Consulta [tipos enteros sin signo](https://kotlinlang.org/docs/unsigned-integers.html) para más detalles.  

### Operaciones a nivel de bits  
Kotlin también proporciona operaciones a nivel de bits (bitwise) para los tipos **Int** y **Long**, como: 

- `shl(bits)` – desplazamiento a la izquierda con signo  
- `shr(bits)` – desplazamiento a la derecha con signo  
- `ushr(bits)` – desplazamiento a la derecha sin signo  
- `and(bits)` – AND a nivel de bits  
- `or(bits)` – OR a nivel de bits  
- `xor(bits)` – XOR a nivel de bits  
- `inv()` – inversión de bits  

Ejemplo:  

```kotlin
val x = (1 shl 2) and 0x000FF000  
```

[^8]: Numbers - Kotlin Programming Language. (s. f.). Kotlin. https://kotlinlang.org/docs/numbers.html

---
## Lógicos

Un objeto booleano[^9] puede representar dos valores _`true`_ y _`false`_. Recuerda que a diferencia de Java, _`Boolean`_ no puede ser nulo. Su contraparte *nullable* es _`Boolean`_.

> [!NOTE]
> *¡No ocupan un bit!*
>En la JVM, los objetos `Boolean` que se guardan como el primitivo `boolean` típicamente ocupan 1 byte.

### Las operaciones booleanas son

| _Operación_ | _Operador_ | _Lógica_ |
| :---------: | :--------: | :------: |
| Disyunción  |  **\|\|**  |    OR    |
| Conjunción  |   **&&**   |   AND    |
|  Negación   |   **!**    |   NOT    |

>[!TIP]
>**Operadores vagos**:
>Los operadores booleanos funcionan de forma "perezosa", por lo que...
>   - Si el primer operando es `true`, `||` no evaluará el segundo  operando.
>   - Si el primer operando es `false`, `&&` no evaluará el segundo operando.

## Caracteres

Los caracteres en Kotlin son representados con el tipo _`Char`_ y sus literales pueden ir entre comillas simples _`'C'`_.  Aunque normalmente los literales de caracteres suelen ser de un único carácter, también podemos encontrar secuencias escapadas de Unicode entre comillas simples cumpliendo con la misma función.

> [!NOTE]
> En la JVM los objetos de tipo `Char` se guardan como el primitivo `char`, representando un carácter Unicode de 16 bits.

Los caracteres especiales pueden ser escapados con una barra invertida _`\`_.

- `\t` - Tabulación
- `\b` - Barra de retroceso
- `\n` - Nueva línea
- `\r` - Retorno de carro
- `\'` - Comilla simple
- `\"` - Comilla doble
- `\\` - Barra invertida
- `\$` - Signo de dólar

También es posible codificar los caracteres utilizando una secuencia escapada de Unicode:

```Kotlin
println('\uFF00')
```

[^9]: Boolean - Kotlin Programming Language. (s. f.). Kotlin. https://kotlinlang.org/docs/booleans.html

----

## Arrays

Los arrays son estructuras estáticas de datos que se almacenan en posiciones contiguas en la memoria principal (RAM).

Son estáticas porque no pueden/deben ampliar su tamaño. Esto se debe a que una nueva posición en el array debería ubicarse al final, en la posición adyacente a la de la última que haya en ese momento. El problema es que no se puede saber si dicha posición estará ocupada por otros datos de ese u otros programas.

>[!WARNING]
>*Array vs ArrayList* [^3]:
>Es importante tener clara la diferencia entre un Array (estático) y un ArrayList (dinámico). En este vídeo de nuestro amigo [Brais Moure](https://mouredev.com/brais-moure/) , a la hora de definir un array, realmente está declarando un ArrayList.
>

[^3]: MoureDev by Brais Moure. (2019c, agosto 22). KOTLIN: Curso ANDROID desde CERO -ARRAYS/ARREGLOS - Lección 5 [2020] | Español | MoureDev [Vídeo]. YouTube. [https://www.youtube.com/watch?v=VHhc-ndfI-Y](https://www.youtube.com/watch?v=VHhc-ndfI-Y)


#### Crear arrays

Podemos crear un array de varias formas.

##### Con la función `arrayOf()`:

```Kotlin
var arrayCorto = arrayOf(1, 2, 3)

println(arrayCorto.joinToString())

/*
 * Si necesitamos un array más grande
 */
arrayCorto = arrayOf(1, 2, 3, 4, 5, 6)

/*
 * El array anterior (1, 2, 3) queda desreferenciado
 * en memoria hasta que el garbage collector se
 * ocupe de él.
 */
println(arrayCorto.joinToString())

```
  [Prueba este código ▶](https://pl.kotl.in/-c6kBqB7Y?from=3&to=17)
##### A partir de un rango: 
Un _rango_[^4] es un intervalo con un valor de inicio y otro de fin. Se puede definir estableciendo ambos valores y separándolos con el operador _`..`_.

  ```Kotlin
val arrayNotasExamen = arrayOf(1..6)

println(arrayNotasExamen::class.simpleName)

println(arrayNotasExamen.joinToString())

//—-----------------------------------
//~$ Array
//~$ 1..6

```

[^4]: Arrays from Ranges. (2017, 1 noviembre). Kotlin Discussions. [https://discuss.kotlinlang.org/t/arrays-from-ranges/5216](https://discuss.kotlinlang.org/t/arrays-from-ranges/5216)

##### Con el constructor Array

Indicando el tamaño inicial (entre paréntesis) y un valor inicial (entre llaves) para todos los elementos.
  
```Kotlin
val arrayNotasExamen = Array<Int>(6){10}

println(arrayNotasExamen.joinToString())

//—-----------------------------------
//~$ 10, 10, 10, 10, 10, 10  
```

También podemos hacerlo indicando el tamaño inicial (entre paréntesis) y una función que genera cada elemento del array indicando su índice

```Kotlin
val arrayNumeros = Array(10, { i -> i + 10 })

println(arrayNumeros.joinToString())

val arrayTextos = Array(10, { i -> (i + 10).toString() })

println(arrayTextos.joinToString())

//—-----------------------------------
//~$ Array
//~$ 10, 11, 12, 13, 14, 15, 16, 17, 18, 19
//~$ Array
//~$ 10, 11, 12, 13, 14, 15, 16, 17, 18, 19
```
[Prueba este código ▶](https://pl.kotl.in/KPxkKs-50)

Internamente, Kotlin usa clases para abstraer arrays de distintos tipos de datos para evitar el [boxing-unboxing](https://www.arquitecturajava.com/java-boxing-y-sus-curiosidades/) de sus elementos y convertirlos en datos primitivos, que son los que finalmente usará la JVM.

Estas clases son: [ByteArray](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin/-byte-array/), [CharArray](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin/-char-array/), [ShortArray](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin/-short-array/), [IntArray](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin/-int-array/), [LongArray](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin/-long-array/), [BooleanArray](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin/-boolean-array/), [FloatArray](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin/-float-array/) y [DoubleArray](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin/-double-array/).


>[!WARNING]
>**Recomendación**:
>En la [documentación oficial](https://kotlinlang.org/docs/arrays.html) se recomienda limitar el uso de arrays a situaciones muy específicas. 
>El motivo es que los arrays son estructuras estáticas de datos, es decir, que son inmutables y no cambian durante la ejecución del programa. Al igual que el String, si se necesita otro array de distinto tamaño al establecido inicialmente, hay que crearlo en memoria y desreferenciar al anterior. 
>
>En Kotlin se aconseja usar [colecciones](https://kotlinlang.org/docs/collections-overview.html) en lugar de arrays, por lo que es preferible utilizarlos.

#### Acceso y modificación

Leer o modificar los elementos de un array se hace de forma similar a Java.

  ```Kotlin
val arrayNumeros = Array(10, { i -> i + 10 })

println(arrayNumeros.joinToString())

println(arrayNumeros[5])

arrayNumeros[5] = 0

println(arrayNumeros.joinToString())

//—-----------------------------------
//~$ 10, 11, 12, 13, 14, 15, 16, 17, 18, 19
//~$ 15
//~$ 10, 11, 12, 13, 14, 0, 16, 17, 18, 19
```

Aunque lo veremos en los [rangos](https://docs.google.com/document/d/1NBdPPQc5gSjRZnafi34eAk254KPwL30mNZIiQkW4XKM/edit?tab=t.0#heading=h.dulvthaoy0bf), se puede usar el operador in para comprobar si un elemento está incluido en un array:

```Kotlin
var arrayCorto = arrayOf(1, 24, 3)

println(24 in arrayCorto)

//—-----------------------------------
//~$ true
```

Podemos recorrer un array de distintas formas:

```Kotlin
val arrayNumeros = Array(10, { i -> i + 10 })

println("Elemento a elemento -------------------------------")

// Elemento a elemento del array
for (numero in arrayNumeros)
	println(numero)

println("Rango de índices –---------------------------------")

// A través de su RANGO DE ÍNDICES
for (indice in arrayNumeros.indices) {
	//println(arrayNumeros[indice])
	println(arrayNumeros.get(indice))
}

println("Índices -------------------------------------------")

// A través de los índices hasta el último
for (indice in 0 .. arrayNumeros.size - 1) {
	println(arrayNumeros[indice])
	//println(arrayNumeros.get(indice))
}
```
  [Prueba este código ▶](https://pl.kotl.in/WVa7aLIUx)

#### Matrices

Podemos crear una matriz[^5] de diferentes formas:
##### Mediante el uso del `arrayOf()`

```Kotlin
//Creación de matriz a partir de arrayOf()
var matrizForma1 = arrayOf(arrayOf(1, 2, 3),
                           arrayOf(4, 5, 6),
                           arrayOf(7, 8, 9))

/** 
 * Creación de matriz a partir de un arrayOf(),y dentro, constructores,
 * inicializándolos a 0.
 */
var matrizForma2 = arrayOf(Array<Int>(3) {0},
                           Array<Int>(3) {0},
                           Array<Int>(3) {0})
  
```
[Prueba este código ▶](https://pl.kotl.in/epnz7Q_P-)

[^5]: Nested Arrays | Kotlin. (s. f.). Kotlin Help. [https://kotlinlang.org/docs/arrays.html#nested-arrays](https://kotlinlang.org/docs/arrays.html#nested-arrays)

##### Mediante el constructor `Array()`
Podemos utilizar _`Array()`_ de forma genérica para facilitar la construcción de matrices. Si creamos una función auxiliar facilitaremos bastante la creación de matrices de distintos tipos.

```Kotlin
fun main() {
    val matrizStrings = crearMatriz(3, 3, "*")
    //Podemos acceder al valor de la matriz y modificarlo/Imprimirlo
    matrizStrings[1][1] = "-"
    // Recorrer y mostrar la matriz de Strings
    for (fila in matrizStrings) {
        for (elemento in fila) {
            print(elemento)
        }
        println()
    }
}

fun crearMatriz(filas: Int, columnas: Int, valorInicial: String) = Array(filas) { 
    Array(columnas) { valorInicial } 
}

//Al imprimir la matriz se habrá modificado el valor

//—---------
//~$ ***
//~$ *-*
//~$ ***
 ```
[Prueba este código ▶](https://pl.kotl.in/_bSOztIaH?theme=darcula)

> [!TIP]
> _¡Ojo!_ 
Con el bucle de arriba recorreremos los elementos de la matriz, pero… ¿Y si queremos acceder a los índices para modificar el valor de los elementos, igual que hacíamos en Java? Para ello podemos acceder a la propiedad indices, presente en las colecciones
> ```Kotlin
> for (i in matrizStrings.indices) {
>     for (j in matrizStrings[i].indices) {
>         println("matrizStrings[$i][$j] = ${matrizStrings[i][j]}")
>     }
> }

Observa que aunque hemos declarado la matriz como inmutable con un _`val`_ podemos modificar su contenido. Esto es porque la referencia en memoria no cambia, ya que NO reasignamos en ningún momento la variable.

En muchas ocasiones es necesario hacer una matriz que sea irregular, para ello, lo más sencillo sería hacer lo siguiente 

```Kotlin
fun main() {
        //Creación de matriz irregular
    val matriz = arrayOf(
	    arrayOf(1, 2, 3), 
	    arrayOf(4, 5), 
	    arrayOf(6, 7, 8, 9)
    )

    //Imprimir la matriz
    for (row in matriz) {
        println(row.contentToString())
    }
}
```
[Prueba este código ▶](https://pl.kotl.in/MnTSXOUx3)

Es importante también mencionar que podremos hacer matrices de más de dos dimensiones o multidimensionales. Este es un ejemplo de una matriz de tres dimensiones.

```Kotlin
//Creación de matriz 3 dimensiones, inicializada a 0
val matrizTresDimensiones = Array(3) {
    Array(3) { Array<Int>(3) { 0 } }
}
```
[Prueba este código ▶](https://pl.kotl.in/ZEyi7fIyW)

> [!NOTE]
> **¿Sabías que...?**
>Para poder visualizar una matriz en consola, es recomendable usar el método `contentToString()`. Pero con más de 2 dimensiones sólo mostrarán las direcciones de memoria en cada caso.
Para estos últimos, el método `contentDeepToString()` que permite ver la matriz en su totalidad:
>```kotlin
>for (fila in matriz) {
>	println(fila.contentToString())
>}

#### Comparar arrays

Para comparar los elementos que contienen dos arrays (en el mismo orden) usaremos los métodos `contentEquals()` y `contentDeepEquals()`.

- _`contentEquals()`_[^6]: para comparar si son estructuralmente iguales, es decir, que tengan tanto el mismo tamaño, como que sus elementos aparezcan en la misma posición y que sean iguales. Devuelve `true`/`false`.

```Kotlin
val arrayFruta = arrayOf("manzana", "naranja", "limón")

//mismo tamaño, mismos elementos 
println(
	arrayFruta.contentEquals(
		arrayOf("manzana", "naranja", "limón")
	)
)
// true

// diferente tamaño
println(
	arrayFruta.contentEquals(
		arrayOf("apple","orange")
	)
)

// false

// los elementos están intercambiados
println(
	arrayFruta.contentEquals(
		arrayOf("manzana", "limón", "naranja")
	)
)
// false
```
[Prueba este código ▶](https://pl.kotl.in/ZWrtZg2p9)

- _`contentDeepEquals()`_[^7]: para comparar si son estructuralmente iguales de forma profunda, esto es que tengan el mismo tamaño y además si tienen arrays como elementos, los compara. Devuelve `true`/`false`.

```Kotlin
val primerArray = arrayOf(intArrayOf(1, 0), intArrayOf(0, 1
val segundaArray = arrayOf(intArrayOf(1, 0), intArrayOf(0, -1)
  
// Los elementos de la posición [1][1] no son iguales
println(
	primerArray.contentDeepEquals(
		segundaArray
	)
) 
// false

segundaArray[1][1] = 1

println(
	primerArray.contentDeepEquals(
		segundaArray
	)
) 
// true
 ```
[Prueba este código ▶](https://pl.kotl.in/O6mvA93Nz)


> [!WARNING]
> **Importante**:
>En el caso de los arrays, los operadores de comparación `==` y `!=` comprueban si ambas variables hacen referencia al mismo array (a la misma posición de memoria). Es decir, el contenido de dos arrays no debe compararse con estos operadores.

[^6]: ContentEquals - Kotlin Programming Language. (s. f.). Kotlin. [https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/content-equals.html](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/content-equals.html)
[^7]: ContentDeepEquals - Kotlin Programming Language. (s. f.). Kotlin.[https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/content-deep-equals.html](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/content-deep-equals.html)

# Operadores

Los operadores[^10] en Kotlin son los habituales en otro lenguajes:

| Categoría               |          Operadores          | Descripción                                                                                                             |
| ----------------------- | :--------------------------: | ----------------------------------------------------------------------------------------------------------------------- |
| Aritméticos             |   `+`, `-`, `*`, `/`, `%`    | Operaciones matemáticas básicas                                                                                         |
| Asignación              |             `=`              | Asignación simple                                                                                                       |
| Asignaciones aumentadas | `+=`, `-=`, `*=`, `/=`, `%=` | Combinan operación y asignación                                                                                         |
| Incremento/Decremento   |          `++`, `--`          | Incrementar o decrementar en 1                                                                                          |
| Lógicos[^11]            |       `&&`, \|\| , `!`       | Operadores AND, OR y NOT                                                                                                |
| Igualdad                |          `==`, `!=`          | Igualdad estructural (equivalente a `equals()`)                                                                         |
| Igualdad referencial    |         `===`, `!==`         | Comprueban si se referencia al mismo objeto                                                                             |
| Comparación             |     `<`, `>`, `<=`, `>=`     | Comparaciones (equivalente a `compareTo()`)                                                                             |
| Acceso a índice         |          `[index]`           | Equivalente a `get()` y `set()`                                                                                         |
| Nulabilidad             |    `!!`, `?.`, `?:`, `?`     | Operadores para manejo de nulos:<br>- `!!`: Not-null assertion<br>- `?.`: Safe call<br>- `?:`: Elvis<br>- `?`: Nullable |
| Referencia              |             `::`             | Crea referencia de miembro o clase                                                                                      |
| Rangos                  |         `..`, `..<`          | Crea rangos con/sin final inclusivo                                                                                     |
| String templates        |          `$`, `${}`          | Referencias a variables/expresiones en Strings                                                                          |

Los operadores de nulabilidad serán muy útiles dada la característica _null safe_ de Kotlin. Más adelante los veremos en profundidad, pero ahí va un pequeño resumen:
- `!!` : Afirma que una expresión no es nula. Solo debemos usarlo en caso de haber comprobado manualmente que un valor no es nulo para decirle al compilador que es seguro utilizarlo.
- `?.` : Llama a métodos o propiedades solo si el objeto no es nulo. Lo que se conoce como una _Safe call_.
- `?:` : Usa el valor de la derecha si el de la izquierda es nulo. Se conoce como operador _Elvis_.
- `?` : Marca un tipo como _nullable_.

[^10]: Operators and Special Symbols - Kotlin Programming Language. (s. f.). Kotlin. https://kotlinlang.org/docs/keyword-reference.html#operators-and-special-symbols
[^11]: Equality - Kotlin Programming Language. (s. f.). Kotlin. https://kotlinlang.org/docs/equality.html

---
# Collections

En Java estudiamos estructuras de datos como _List, Set o Map_. Kotlin también las contempla como colecciones[^20].

La _Biblioteca Estándar de Kotlin_ proporciona herramientas completas para gestionar colecciones: grupos de elementos que son significativos para el problema que se está resolviendo.

Hay que tener en cuenta que a la hora de declarar cualquier colección hay que indicar si queremos que sea mutable desde su misma declaración, ya que por defecto son inmutables. Normalmente una colección contiene elementos del mismo tipo.

La librería estándar de Kotlin ofrece una serie de interfaces genéricas, clases y funciones para crear, rellenar y administrar colecciones independientemente de su tipo.

La interfaz **`Collection<T>`** es la raíz de la jerarquía de colecciones. Proporciona operaciones típicas para la lectura de sus elementos. Las colecciones heredan de **`Iterable<T>`**, que proporciona operaciones para iterar sobre los elementos de la colección.

Para poder tener operaciones de escritura, se debe usar o la interfaz **`MutableCollection<T>`** o las clases que la implementen.

>[!IMPORTANT]
>Los tipos de colecciones de *solo lectura* son *[covariantes](https://kotlinlang.org/docs/generics.html#variance)*. Esto significa que, si una clase `<T>` hereda de `<E>`, puedes usar un `List<T>` en cualquier lugar donde se requiera un `List<E>`. Los tipos de colección tienen la misma relación de subtipo que los tipos de elementos. 
>
>Los *mapas son covariantes en el tipo de valor*, pero no en el tipo de clave.
>
>Por otra parte, las *colecciones mutables no son covariantes*; de lo contrario, esto conduciría a errores en tiempo de ejecución. Si `MutableList<T>` fuera un subtipo de `MutableList<E>`, podrías insertar otros herederos de `E` en él, violando así su argumento de tipo `T`.
## Tipos de Colecciones

### 1. List (Lista)

`List<T>` es una **Colección** ordenada con acceso a elementos por índices, los cuales van desde el 0 hasta `lastIndex`. Los elementos pueden repetirse varias veces en la misma lista. Dos listas se consideran iguales si tienen el mismo tamaño y elementos estructuralmente idénticos en la misma posición.

```kotlin
val numeros = listOf("uno", "dos", "tres", "cuatro")
println(numeros[2]) // Imprime "tres"
```

Propiedades:
- `size`: Devuelve el número de elementos en la lista.

Métodos importantes:
- `contains(element : <E>)`: Evalúa si un elemento se encuentra en la lista.
- `get(index: Int)`: Devuelve el elemento en la posición indicada.
- `indexOf(element: <E>)`: Devuelve la posición de la primera ocurrencia del elemento en la lista.
- `isEmpty()`:  Evalúa si la lista está vacía.
- `subList(fromIndex: Int, toIndex: Int)`: Devuelve una vista de la lista desde la posición `fromIndex` hasta `toIndex`. Los cambios no estructurales en la vista se reflejan en la lista original.
- `lastIndexOf(element: <E>)`: Devuelve la posición de la última ocurrencia del elemento en la lista.

#### MutableList
Una **lista mutable** _`MutableList<T>`_ es un tipo de lista que permite las operaciones de escritura de las listas. En Kotlin la implementación por defecto de una `MutableList`es **`ArrayList`**.
Los métodos más importantes de la lista mutable son:
- `add(element: <E>)`: Añade un elemento al final de la lista.
- `remove(element: <E>)`: Elimina la primera ocurrencia del elemento en la lista.
- `removeAt(index: Int)`: Elimina el elemento en la posición indicada.
- `clear()`: Elimina todos los elementos de la lista.
- `addAll(collection: Collection<E>)`: Añade todos los elementos de la colección a la lista.
- `removeAll(collection: Collection<E>)`: Elimina todos los elementos de la colección de la lista.)
- `set(index: Int, element: <E>)`: Reemplaza el elemento en la posición indicada. Es lo mismo que utilizar la notación `[]`.
- `shuffle()`: Baraja los elementos de la lista.

```Kotlin
fun main() {
	val numbers = mutableListOf(1, 2, 3, 4)
	numbers.add(5)
	numbers.removeAt(1)
	numbers[0] = 0
	numbers.shuffle()
	println(numbers.joinToString())
}
```
[Prueba este código ▶](https://pl.kotl.in/ZwyfM5Ui8)

### 2. Set (Conjunto)

Un conjunto o [`Set`](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.collections/-set/) es una colección de elementos únicos en la que el orden generalmente no es significativo. Representa la idea matemática de un conjunto. Dos sets son iguales si tienen los mismos elementos.

>[!NOTE]
>Como no se pueden repetir objetos, solamente puede contener un elemento nulo.

Propiedades:
- `size`: Devuelve el número de elementos en el conjunto.

Métodos importantes:
- `contains(element: <E>)`: Evalúa si un elemento se encuentra en el conjunto.
- `containsAll(elements: Collection<E>)`: Evalúa si todos los elementos de la colección están en el conjunto.
- `isEmpty()`: Evalúa si el conjunto está vacío.

#### MutableSet
`MutableSet` es una interfaz de conjunto que permite operaciones de escritura, extendiendo las capacidades de `MutableCollection`. 

La implementación por defecto del conjunto mutable, `LinkedHashSet`, preserva el orden de inserción de los elementos. Las funciones que dependen del orden (como `first()` o `last()`) devuelven resultados predecibles.

```kotlin
val numeros = setOf(1, 2, 3, 4)
val numerosInversos = setOf(4, 3, 2, 1)

// Estos ejemplos mostrarán comportamientos diferentes según la implementación
println(numeros.first() == numerosInversos.first())
println(numeros.first() == numerosInversos.last())
```

Una implementación alternativa, `HashSet`, no garantiza ningún orden específico, pero requiere menos memoria para almacenar el mismo número de elementos.

- `add(element: <E>)`: Añade un elemento al conjunto.
- `addAll(collection: Collection<E>)`: Añade todos los elementos de la colección al conjunto.
- `remove(element: <E>)`: Elimina un elemento del conjunto.
- `removeAll(collection: Collection<E>)`: Elimina todos los elementos de la colección del conjunto.
- `clear()`: Elimina todos los elementos del conjunto.
- `retainAll(collection: Collection<E>)`: Elimina todos los elementos del conjunto que no están en la colección introducida como argumento.
### 3. Map (Diccionario)
Aunque no hereda de la interfaz `Collection`, `Map<K,V>`forma parte de los tipos de colección de Kotlin. La interfaz `Map` funciona mediante pares clave-valor, donde cada clave es única y se mapea a un único valor, que puede estar repetido. Dos mapas que contengan los mismos pares clave-valor son iguales independientemente de su orden.

```kotlin
val mapaNumeros = mapOf("clave1" to 1, "clave2" to 2)
println(mapaNumeros.keys) // Imprime las claves
println(mapaNumeros.values) // Imprime los valores
```

Propiedades:
- `size`: Devuelve el número de pares clave-valor en el mapa.
- `keys`: Devuelve un conjunto de las claves usadas en el mapa.
- `values`: Devuelve una colección de los valores del mapa.
- `entries`: Devuelve un set con todos los pares clave-valor del mapa. Este set es de tipo `Map.Entry<K, V>`, siendo `Entry`una interfaz anidada que representa uno de estos pares.

>[!TIP]
>Puedes consultar la implementación de todas estas clases en la [documentación oficial](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/). Por ejemplo, esta es la implementación de `Map.Entry<K,V>`:
>
>```Kotlin
>public interface Entry<out K, out V> {
>   /**
>    * Returns the key of this key/value pair.
>    */
>    public val key: K
>  
>   /**
>    * Returns the value of this key/value pair.
>    */
>    public val value: V
>}
>```

Métodos importantes:
- `size()`: Devuelve el tamaño del mapa.
- `containsKey(key: <K>)`: Evalúa si una clave se encuentra en el mapa.
- `containsValue(value: <V>)`: Evalúa si un valor se encuentra en el mapa.
- `isEmpty()`: Evalúa si el mapa está vacío.
- `get(key: <K>)`: Devuelve el valor asociado a la clave indicada.
- `getOrDefault(key: <K>, defaultValue: <V>)`: Devuelve el valor asociado a la clave indicada o un valor por defecto si no existe.
#### MutableMap
`MutableMap` es una interfaz de mapa que permite operaciones de escritura, extendiendo las capacidades de `Map`. La implementación por defecto de `MutableMap` es `LinkedHashMap`, que preserva el orden de inserción de los elementos. La implementación alternativa `HashMap`sin embargo no toma en consideración el orden de los elementos.
- `put(key: <K>, value: <V>)`: Añade un par clave-valor al mapa. Es lo mismo que utilizar la notación `[]`.
- `putAll(from: Map<out K, V>)`: Añade todos los pares clave-valor de otro mapa al mapa.
- `remove(key: <K>)`: Elimina un par clave-valor del mapa.
- `clear()`: Elimina todos los pares clave-valor del mapa.

```Kotlin
val mapaNumeros = mutableMapOf("uno" to 1, "dos" to 2)
mapaNumeros["tres"] = 3 // Añade un nuevo par clave-valor
mapaNumeros.put("cuatro", 4) // Añade un nuevo par clave-valor
mapaNumeros.remove("uno") //Borra el elemento con clave "uno"
```

## ArrayDeque
`ArrayDeque`es una implementación de cola de doble extremo que permite agregar o eliminar elementos al principio o final. Por tanto, puede funcionar como Pila y Cola. Es una estructura *mutable*.

```kotlin
val cola = ArrayDeque(listOf(1, 2, 3))
cola.addFirst(0)
cola.addLast(4)
println(cola) // [0, 1, 2, 3, 4]
```

Propiedades:
- `size`: El tamaño de la colección.
- `modCount`: El número de modificaciones realizadas en la cola a nivel estructural.

Métodos importantes:
- `add(element: <E>)`: Añade un elemento al final de la cola.
- `add(index: Int, element: <E>)`: Añade un elemento en la posición indicada.
- `addAll(elements: Collection<E>)`: Añade todos los elementos de la colección a la cola.
- `addAll(index: Int, elements: Collection<E>)`: Añade todos los elementos de la colección en la posición indicada.
- `addFirst(element: <E>)`: Añade un elemento al principio de la cola.
- `addLast(element: <E>)`: Añade un elemento al final de la cola.
- `clear()`: Elimina todos los elementos de la colección.
Puedes consultar el resto de métodos [a través de este enlace](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.collections/-array-deque/)

[^20]: _Collections overview | Kotlin_. (s. f.). Kotlin Help. [https://kotlinlang.org/docs/collections-overview.html](https://kotlinlang.org/docs/collections-overview.html)

---
# Null Safety

¿Qué es la seguridad de nulos o **Null Safety**? El valor nulo (`null`) está extendido en todos (o casi todos) los lenguajes de programación. Se usa para indicar la ausencia de un valor.

En _Java_, si se intenta operar sobre un elemento nulo sin haberlo comprobado previamente, salta una excepción de puntero nulo ([NullPointerException](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/NullPointerException.html)). Si el código no atrapa esta excepción, el programa detiene su ejecución de forma inmediata (crash).

_Kotlin_, en cambio, tiene un sistema de seguridad de nulos para evitar este tipo de errores. Esto se logra al comprobar la posibilidad de nulos en tiempo de compilación, en lugar de dejarlo para el tiempo de ejecución.

Para empezar, por defecto Kotlin no admite valores nulos:
```Kotlin
var nombre = "Pepe"
nombre = null // Error de compilación
```

Si se quiere indicar que una variable podría ser nula (_nullable_) hay que expresarlo en su tipo con el operador `?` .

```Kotlin
var nombre: String? = "Pepe"
println(nombre)
  
nombre = null
println(nombre)

//—-----------------------------------
//~$ Pepe
//~$ null
```
## Operador seguro (?.)

Kotlin usa el operador seguro `?.` en variables nullables (podrían ser nulas) para permitir acceder a sus miembros (propiedades y métodos) de forma segura. Si el valor es nulo, la expresión completa se evalúa a null:

```Kotlin
var cadena: String? = null
val longitud: Int? = cadena?.length

println(longitud)

//—-----------------------------------
//~$ null
```

## Operador Elvis (?:)

El operador Elvis `?:` sirve para proporcionar un valor por defecto en caso de que el valor a la izquierda sea nulo:

```Kotlin
val nombre : "Pepe"
val apellido1: String? = null
val apellido2: String? = "Fernández"
val nombreCompleto: String = nombre
        + " "
        + apellido1 ?: "Expósito"
        + apellido2 ?: "Expósito"

println(nombreCompleto)

//—-----------------------------------
//~$ Pepe Expósito Fernández
 ```
  
Otros ejemplos del uso del operador Elvis: [ejemplo 1](https://pl.kotl.in/52M0snJsu), [ejemplo 2](https://pl.kotl.in/ZjiCPjZi1).

## Operador de no nulidad (!!)
El operador de no nulidad `!!` indica que la variable a la que acompaña no es nula:
```Kotlin
// Asume que apellido no es nulo
val longitud: Int = apellido!!.length
```

> [!WARNING]
> El operador `!!` podría provocar un `NullPointerException` si la variable es nula. Se recomienda evitar en la medida de lo posible este operador.

### Más información
A continuación tienes referentes documentales de las webs oficiales tanto de Kotlin como de Android sobre null safety:

<div style="display: flex; flex-direction: column">
	<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeb3XCD0Xy65MUlLIqr1KFb6zRXgoVX1LHiXLVV8JgEyz9Qbb3dUfzLrt848syyKYBvoa8mi-Sxnge3b487k59wtig87rwCJS7s1IdGUDj93UINFG-4w198LdMcVdGVfgpPEfPEz6JjA1ySE6nvEZRNA4Q?key=XNFZp9MjZe1FDQoomJ2CJA" width="100" style="margin: 0 auto 20"/>
	<hr/>
</div>

##### Documentación Oficial
- **Null safety | Kotlin** (Kotlin Help)
  - [Documentación completa](https://kotlinlang.org/docs/null-safety.html)

##### Recursos de Desarrollo
- **Nulabilidad en Kotlin** (Android Developers)
  - [Codelabs de Nulabilidad](https://developer.android.com/codelabs/basic-android-kotlin-compose-nullability?hl=es-419#0)

---
# Rangos

Un rango[^12] no es un tipo de dato como tal. Se trata de un intervalo con un valor de inicio y otro de fin. Se puede definir estableciendo ambos valores y separándolos con el operador `..` :

  
```Kotlin
val abecedarioMinusculas = "a".."z"

println(abecedarioMinusculas)
println(abecedarioMinusculas::class.simpleName)

//—-----------------------------------
//~$ a..z
//~$ ComparableRange
```

Se puede definir un intervalo con cualquier tipo que sea comparable.(números, letras, etc.).
El operador in permite comprobar si un valor dado se encuentra en un rango:

```Kotlin
val abecedarioMinusculas = "a".."z"

println(abecedarioMinusculas)
println("n" in abecedarioMinusculas)
println("N" in abecedarioMinusculas)
  
//—-----------------------------------
//~$ a..z
//~$ true
//~$ false
```

Es importante entender que, aunque Kotlin infiere muchas cosas, no es consciente de que un rango sea decreciente:

```Kotlin
val abecedarioMinusculas = "z".."a"

println(abecedarioMinusculas)
println("n" in abecedarioMinusculas) //no encuentra el carácter!!

  

//—-----------------------------------
//~$ a..z
//~$ false

```
  
Cuando un rango sea decreciente, hay que indicarlo. Para mostrar un ejemplo, usaremos rangos de enteros ya que los de String no son rangos ordenados:

```Kotlin
val rangoNumeros = (1..10).reversed()

println(rangoNumeros)

//—-----------------------------------
//~$ 10 downTo 1 step 1

```

En [este enlace](https://pl.kotl.in/Qx7AOj6I0) puedes probar código de ejemplo de usos de los rangos.

Hasta ahora todos los rangos que hemos visto son inclusivos, es decir, incluyen el primer y el último valor del rango. Para hacer rangos excluyentes (que no incluyan alguno de los límites) podemos hacerlo de varias formas:

```Kotlin
val rangoExclusivo = 1 until 6 
println("Primera forma")
for (i in rangoExclusivo) print(i)

val rangoExclusivo2 = 1.until(6)
println("\nSegunda forma")
for (i in rangoExclusivo2) print(i)

val rangoExclusivo3 = 1 ..< 6
println("\nTercera forma")
for (i in rangoExclusivo3) print(i)

//------------------------—------
//Todas las variantes generan el mismo rango
//~$ 12345
 ```
 [Prueba este código ▶](https://pl.kotl.in/4usCSdBuZ) 

Esta forma de generar rangos solo excluye el final. Si queremos excluir el principio, deberemos hacerlo a la antigua usanza:

```Kotlin
val start = 0
val end = 10
val rangoExclusivo = (start + 1)..< end
rangoExclusivo.forEach{i -> print(i)}

//---------—---------
//~$ 123456789
```
[Prueba este código ▶](https://pl.kotl.in/yQlqoespk)

Esto funciona también con rangos de **caracteres**:
```Kotlin
val rango = 'a'+ 1 ..< 'z'
for (letra in rango) {
	print(letra)
}

//-----------------------------
//~$ bcdefghijklmnopqrstuvwxy
```
 [Prueba este código ▶](https://pl.kotl.in/-uJ2huliG)

> [!NOTE]
> Igual a estas alturas ya te has dado cuenta, pero si creas un rango de Strings (“a”..”z”) Kotlin te permite imprimirlo o comprobar si algún elemento está incluido en él, pero no iterar en él.

Por resumir, estas son algunas de las formas con las que podríamos iterar un rango[^13]. 

```Kotlin
for (i in 1..100) { ... }  // final cerrado: Incluye el 100

for (i in 1..<100) { ... } // final abierto: No incluye el 100

for (i in 1+1..<100) { ... } //final y principio abiertos

for (x in 2..10 step 2) { ... } //ascendente con paso 2

for (x in 10 downTo 1) { ... } //descendente

(1..10).forEach { ... } //de forma declarativa
```

[^12]: Basic syntax | Kotlin. (s. f.-c). Basic Syntax. Ranges. [https://kotlinlang.org/docs/basic-syntax.html#ranges](https://kotlinlang.org/docs/basic-syntax.html#ranges)
[^13]: Idioms. (2024, September 25). Kotlin. Retrieved October 3, 2024, from [https://kotlinlang.org/docs/idioms.html#iterate-over-a-range](https://kotlinlang.org/docs/idioms.html#iterate-over-a-range)

# Control de flujo

Como ya sabemos de otros lenguajes de programación (p.e. Java), podemos controlar la ejecución de determinados bloques de código para que se ejecuten de forma condicional o repetitiva. 
## Condicionales
### if - else if - else
La sentencia if en Kotlin funciona como en otros lenguajes:


```Kotlin
val a = 3
val b = 78
var valorMaximo = 0

if (a > b)
    valorMaximo = a
else
    valorMaximo = b

// Lo anterior, en una sola línea:

valorMaximo = if (a > b) a else b

// Lo anterior, en bloques de código:

valorMaximo = if (a > b) {
    println("El máximo es $a")
    a
} else {
    println("El máximo es $b")
    b
}

//—-----------------------------------
//~$ Opción 1:
//~$ El máximo es 78
//~$ Opción 2:
//~$ El máximo es 78
//~$ Opción 3:
//~$ El máximo es 78

```
  [Prueba este código ▶ ](https://pl.kotl.in/CfaYA5h7G)
  
En la opción 3 del ejemplo anterior, donde el if se usa como una expresión (es decir, una sentencia que devuelve un resultado) es obligatorio el uso de else para garantizar que dicha expresión devuelve un valor.

> [!TIP]
> El funcionamiento  del `if-else` es tan versátil que Kotlin no necesita usar el operador ternario ?, por lo que no lo tiene implementado.
### when
El switch que se usa en Java para ejecutar un bloque de código de entre varios según el valor de un dato se conoce como [when](https://kotlinlang.org/docs/control-flow.html#when-expression) en Kotlin.[^14]

Esta sentencia permite mostrar de forma más sencilla la evaluación de varias condiciones, en lugar de usar una cascada de sentencias `if - else if - else`:

```Kotlin
val posicion = 3

when (posicion) {
	1 -> print("Medalla de ORO")
	2 -> print("Medalla de PLATA")
	3 -> print("Medalla de BRONCE")
	else -> {
		print("No obtiene medalla")
	}
}
//—-----------------------------------
//~$ Medalla de BRONCE
```
[Prueba este código ▶](https://pl.kotl.in/GZOLn7Eqc)

También pueden usarse expresiones en las ramas de condiciones:

```Kotlin
val posicion = 3
when {
	posicion == 1 -> print("Medalla de ORO")
	posicion == 2 -> print("Medalla de PLATA")
	posicion == 3 -> print("Medalla de BRONCE")
	else -> {
		 print("No obtiene medalla")
	}
}

//—-----------------------------------
//~$ Medalla de BRONCE  
```

Además de en una sentencia como la anterior, when se puede usar como una expresión:

```Kotlin
val posicion = 3
val medalla = when (posicion) {
	1 -> "ORO"
	2 -> "PLATA"
	3 -> "BRONCE"
	else -> "-"
}

println(medalla)

//—-----------------------------------
//~$ BRONCE

```
  [Prueba este código ▶](https://pl.kotl.in/ipcJCYwYv)

> [!NOTE] 
>  Cuando se usa `when` como una expresión es obligatorio el `else`, salvo que se evalúen todas las posibles opciones (todos los valores de un array o de un enum, etc.).

Pueden combinarse varios valores para que ejecuten el mismo bloque de código:

```Kotlin
val posicion = 3
val mensaje = when (posicion) {
	1, 2, 3 -> "Ha ganado medalla!"
	else -> "Lo sentimos mucho. Que no decaiga el ánimo!"
}

println(mensaje)  

//—-----------------------------------
//~$ Ha ganado medalla!
```

También pueden usarse expresiones en las condiciones:

```Kotlin
val numeroGanador = "8"
val numero = 3
val mensaje = when (numero) {
	numeroGanador.toInt() -> "Has ganado!"
	else -> "Lo sentimos mucho. Sigue intentándolo."
}
println(mensaje)

//—-----------------------------------
//~$ Lo sentimos mucho. Sigue intentándolo.

```

Se puede usar el operador in para rangos y colecciones:

```Kotlin
val numero = 8
val delUnoAlDiez = 1..10
val mensaje = when (numero) {
	in delUnoAlDiez -> "Está entre los 10 primeros!"
	else -> "No está en la mejor clasificación."
}

println(mensaje)

// Otra forma
val numero = 8
val delUnoAlDiez = 1..10
val mensaje = when (numero) {
	!in delUnoAlDiez -> "No está en la mejor clasificación."
	else -> "Está entre los 10 primeros!"
}

println(mensaje)

//—-----------------------------------
//~$ Está entre los 10 primeros!
//~$ Está entre los 10 primeros!
    
```

  También se puede utilizar el operador `is` para ejecutar determinadas acciones según el tipo de dato:

```Kotlin
fun main() {
    val nombre1 = "Pepe"
    val nombre2 = "Ana"
    val numero = 10
    var empiezaPorAOEsDiez = hasPrefix(nombre1)

    println(empiezaPorAOEsDiez)
    empiezaPorAOEsDiez = hasPrefix(nombre2)
    println(empiezaPorAOEsDiez)

    empiezaPorAOEsDiez = hasPrefix(numero)
    println(empiezaPorAOEsDiez)

}
 
fun hasPrefix(x: Any) = when(x) {
    is String -> x.startsWith("A")
    is Int -> x == 10
    else -> false
}
```
[Prueba este código ▶](https://pl.kotl.in/gHd7UOjVk)

[^14]:MoureDev by Brais Moure. (2019b, agosto 8). KOTLIN: Curso ANDROID desde CERO - SENTENCIA WHEN - Lección 4 [2020] | Español | MoureDev [Vídeo]. YouTube. [https://www.youtube.com/watch?v=ufsrPf7vao4](https://www.youtube.com/watch?v=ufsrPf7vao4)
## Bucles
Los bucles son similares a Java, al igual que las [expresiones para interrumpirlos](https://kotlinlang.org/docs/returns.html).

Los bucles son estructuras de control fundamentales en la programación que nos permiten ejecutar una serie de instrucciones repetidamente mientras se cumpla una determinada condición. En Kotlin, al igual que en Java, los tipos más comunes de bucles son:
- **For**
- **While**
- **Do-While**

Muchas veces para modificar el flujo de ejecución usaremos las conocidas expresiones:
- **break**: termina inmediatamente la ejecución de las instrucciones dentro del bucle, saltando a la siguiente línea después del bucle.
- **continue**: salta el código que haya dentro del cuerpo del bucle, a la siguiente iteración.

### For
Se utiliza cuando se conoce de antemano el número de iteraciones. En Kotlin, para crear bucles de tipo for, usaremos los ya conocidos `forEach`.

```Kotlin
for (item in collection) print(item)
```

Pero nos preguntaremos cómo hacer el `for` con iteraciones que sabemos hacer de Java, pues en este caso usaremos los Rangos que vimos anteriormente. En el ejemplo de abajo podemos observar un bucle `for`, donde se le asignará a la variable numero, en cada iteración, el valor del 1 al 10.

```Kotlin
for (numero in 1..10)
    println(numero)
```
[Prueba este código ▶](https://pl.kotl.in/WZQrEIaFU)
  
Es importante mencionar que el bucle de arriba irá de 1 en 1, si queremos que vaya de 2 en 2, entonces al final del rango le pondremos `step 2`:

```Kotlin
for (numero in 1..10 step 2)
    println(numero)
```
[Prueba este código ▶](https://pl.kotl.in/dAKZxyt0M)
  
Pero, ¿cómo podremos ir en vez de forma ascendente, descendente?, muy sencillo haremos uso del `downTo`, también podemos ayudarnos del `step` en estos casos.

```Kotlin
for (numero in 10 downTo 0 step 2)
    println(numero)
```
[Prueba este código ▶](https://pl.kotl.in/mcUo-pohy)
  
Si queremos recorrer un array podemos hacerlo de dos formas:

```Kotlin
for (i in array.indices) 
    println(array[i])
```
[Prueba este código ▶](https://pl.kotl.in/vgpXrz312)
  
```Kotlin
for ((i, v) in array.withIndex())
    println("the element at $i is $v")
```
[Prueba este código ▶](https://pl.kotl.in/HXy0k3chi)

En este último caso **`array.withIndex()`** devuelve un par de valores, el índice y el valor del elemento. `(i, v)` es una _desestructuración_ de este par.

### While
Se ejecuta mientras una condición sea verdadera.[^15]

```Kotlin
var x = 7
while ( x > 0 ){
    println(x)
    x--
}
```
[Prueba este código ▶](https://pl.kotl.in/nG6FERQwa)
### Do-While
Es similar al _`While`_ pero se garantiza que al menos se ejecutará una vez.[^16]

```Kotlin
var x: Int = 0

do {
    println(x)
    x++
} while( x < 10 )
```
[Prueba este código ▶](https://pl.kotl.in/lypOJ7d1T)


[^15]: Conditions and loops | Kotlin. (s. f.-b). Kotlin Help. [https://kotlinlang.org/docs/control-flow.html#while-loops](https://kotlinlang.org/docs/control-flow.html#while-loops)
[^16]: Conditions and loops | Kotlin. (s. f.-b). Kotlin Help. [https://kotlinlang.org/docs/control-flow.html#while-loops](https://kotlinlang.org/docs/control-flow.html#while-loops

---
# Funciones

Una **función** es un conjunto de instrucciones que realizan una tarea específica y se encuentran empaquetadas como una unidad. En **Kotlin**, las funciones son lo que se conoce como _[ciudadanos de primera clase](https://en.wikipedia.org/wiki/First-class_function)_, lo que permite tratarlas como objetos que pueden ser almacenados en variables, pasados como argumentos a otras funciones y devueltos como resultado de funciones, dándoles una flexibilidad y expresividad funcional que facilita la _creación de código modular y reutilizable_.

Para declarar funciones en Kotlin, usamos la palabra reservada fun:

```Kotlin
fun double(x: Int): Int {
    return 2 * x
}
```

## Partes de una función
Las funciones en Kotlin tienen las siguientes partes:
- **Declaración**: se inicia con la palabra reservada `fun`.
- **Nombre**: es el identificador de la función.
- **Parámetros**: son los valores que la función recibe para realizar su tarea.
- **Tipo de retorno**: es el tipo de dato que la función devuelve como resultado.
- **Cuerpo**: es el bloque de código que contiene las instrucciones que la función ejecuta.

<div align="center">
    <img  src="https://i.imgur.com/tDHEmSr.png" width="50%" />
</div>

Habrás observado que _no hay un modificador de acceso_ . En Kotlin todas las funciones son _públicas por defecto_, a no ser que se le diga lo contrario.

Existe un tipo de retorno que igual no conoces, **Unit**. El funcionamiento de Unit es _similar al de void en Java_, salvo que a diferencia de este último no es una palabra reservada, sino un tipo de valor más. En muchas ocasiones Unit estará implícito y no será necesario ponerlo:

```Kotlin
fun imprimirMensaje(mensaje: String): Unit { 
    println(mensaje) 
}
  
//Equivalentes

fun imprimirMensaje(mensaje: String){ 
    println(mensaje) 
}
```

Unit es un tipo de valor con una _única instancia llamada Unit_. Esto significa que puedes tratarlo como un objeto y devolverlo explícitamente, algo que igual ahora no te dice mucho, pero te resultará útil más adelante cuando comprendas cómo utilizar funciones de orden superior.
## Funciones como expresión

Si la función[^17] que estás declarando retorna una única expresión, puedes ahorrarte las llaves (`{}`) y la palabra reservada `return` y sustituirlas por un `=`. Cuando el tipo de retorno pueda ser inferido por el compilador también puedes ahorrártelo. Las siguientes funciones son totalmente equivalentes:

```Kotlin
//Como expresión con tipo
fun double(x: Int): Int = x * 2

//Como expresión con tipo inferido
fun double(x: Int)= x * 2

//Forma tradicional
fun double(x: Int): Int {
    return x * 2
}
```

## Funciones con número variable de argumentos
Una función puede tener un número [variable de parámetros](https://kotlinlang.org/docs/arrays.html#pass-variable-number-of-arguments-to-a-function). Usando el modificador `vararg` se puede pasar un número variable de argumentos a una función. Para pasar un array con un número variable de elementos a una función, puedes usar el _operador de propagación_ (`*`). El operador de propagación pasa cada elemento del array como argumentos individuales a la función:

```Kotlin
fun main() {
    val lettersArray = arrayOf("c", "d")
    printAllStrings("a", "b", *lettersArray)
    // Equivalente a poonr printAllStrings("a", "b", "c", "d")
}

//Puede recibir un número variable de argumentos individuales.
fun printAllStrings(vararg strings: String) {
    for (string in strings) {
        print(string)
    }
}
```

## Argumentos por defecto
En Kotlin, puedes asignar valores por defecto a los parámetros de una función. De esta manera, si no se proporciona un valor para un parámetro, se usará el valor por defecto:

```Kotlin
fun main() {
    printMessage("Hola")
    println()
    printMessage("Hola", 3)
}

fun printMessage(message: String, count: Int = 1) {
    for (i in 0 until count) {
        println(message)
    }
}
```
[Prueba este código ▶](https://pl.kotl.in/1fs1-TgkY)

### Herencia y valores por defecto

Cuando se sobrescribe un método que tiene parámetros con valores por defecto, es importante tener en cuenta que:

- La función que sobrescribe siempre utiliza los valores por defecto del método base.
- No se permite especificar valores por defecto en la declaración del método que sobrescribe.

Ejemplo:

```kotlin
open class A {
    open fun foo(i: Int = 10) { /*...*/ }
}

class B : A() {
    override fun foo(i: Int) { /*...*/ }  // No se permite valor por defecto
}
```

### Lambdas y parámetros por defecto

Si el último argumento después de parámetros con valores por defecto es una lambda, existen varias formas de realizar la llamada:

```kotlin
fun foo(
    bar: Int = 0,
    baz: Int = 1,
    qux: () -> Unit,
) { /*...*/ }

// Diferentes formas de llamar a la función:

foo(1) { println("hola") }     
// Usa el valor por defecto baz = 1

foo(qux = { println("hola") }) 
// Usa ambos valores por defecto (bar = 0 y baz = 1)

foo { println("hola") }        
// Usa ambos valores por defecto (bar = 0 y baz = 1)
```
## Llamar argumentos por su nombre

Cuando invocas a una función, puedes asignar un valor a un argumento llamándolo por su nombre. Esto permite cambiar el orden de los argumentos y proporcionar solo los argumentos que necesitas:

```kotlin
fun reformat(
    str: String,
    normalizeCase: Boolean = true,
    upperCaseFirstLetter: Boolean = true,
    divideByCamelHumps: Boolean = false,
    wordSeparator: Char = ' ',
) {
    /*...*/
}

reformat("hola") // Usa los valores por defecto

reformat("hola mundo", divideByCamelHumps = true) 
// Usa los valores por defecto y divideByCamelHumps = true
```

### Orden y llamadas con argumentos nombrados

Cuando un parámetro con valor por defecto precede a un parámetro sin valor por defecto, el valor por defecto solo puede utilizarse mediante llamadas con argumentos nombrados:

```kotlin
fun foo(
    bar: Int = 0,
    baz: Int,
) { /*...*/ }

foo(baz = 1) // Se usa el valor por defecto bar = 0
```

## Ámbito de las funciones

### Funciones de nivel superior
Una característica distintiva de Kotlin es la capacidad de _declarar funciones a nivel superior_ en un archivo, sin necesidad de crear una clase contenedora. Esto contrasta con otros lenguajes como Java.

Además de las funciones de nivel superior, Kotlin permite declarar funciones como:
- Funciones locales
- Funciones miembro
- Funciones de extensión
### Funciones locales

Kotlin soporta funciones locales, que son funciones definidas dentro de otras funciones. Veamos un ejemplo práctico:

```kotlin
fun busquedaProfundidad(grafo: Grafo) {
    fun buscar(actual: Vertice, visitados: MutableSet<Vertice>) {
        if (!visitados.add(actual)) return
        for (v in actual.vecinos)
            buscar(v, visitados)
    }
    buscar(grafo.vertices[0], HashSet())
}
```

Una característica poderosa de las funciones locales es que pueden acceder a las variables locales de las funciones externas (closure). Por ejemplo, podemos refactorizar el ejemplo anterior:

```kotlin
fun busquedaProfundidad(grafo: Grafo) {
    val visitados = HashSet<Vertice>()
    fun buscar(actual: Vertice) {
        if (!visitados.add(actual)) return
        for (v in actual.vecinos)
            buscar(v)
    }

    buscar(grafo.vertices[0])
}
```

### Funciones miembro
Las funciones miembro son aquellas que se definen dentro de una clase u objeto:

```kotlin
class Ejemplo {
    fun saludar() { print("Hola") }
}
```

Para invocar funciones miembro se utiliza la notación de punto:

```kotlin
Ejemplo().saludar() // crea una instancia de la clase Ejemplo y llama a saludar
```

### Funciones de extensión
Las funciones de extensión[^19] permiten añadir a una clase o interfaz funcionalidad extra sin necesidad de usar herencia o decoradores. 

Declarar funciones de extensión es bastante sencillo, solo es necesario declarar la función con el prefijo del tipo que va a recibir la extensión, como en el siguiente ejemplo:

```Kotlin
fun String.repetir(n: Int): String {
    return (1..n).joinToString("") { this }
}

printl("Hola".repetir(3)) // Imprime "HolaHolaHola"
```

En este contexto la palabra reservada **`this`** corresponde al objeto que invoca a la función de extensión. Esto también podríamos hacerlo con funciones con _tipos genéricos_:

```Kotlin
fun <T> List<T>.penultimo(): T {
    return this[size - 2]
}
//Devuelve el penúltimo objeto de una lista del tipo que se declare
```

> [!IMPORTANT]
> **Las funciones de extensión se resuelven estáticamente.**
> Las extensiones no modifican las clases ni les añaden nuevos miembros. Por ello, qué extensión de función se va a llamar se decide en tiempo de compilación basándose en el tipo del objeto receptor.
> ```Kotlin
> open class Shape
>class Rectangle: Shape()
>
>fun Shape.getName() = "Shape"
>fun Rectangle.getName() = "Rectangle"
>fun printClassName(s: Shape) {
>    println(s.getName())
>}
>
>printClassName(Rectangle()) //Imprime 'Shape'
>```

Si se define una función de extensión de la misma manera exacta que una función miembro de una clase, la función miembro siempre tendrá prioridad.  

```Kotlin
class Example {
    fun printFunctionType() { println("Class method") }
}

fun Example.printFunctionType() { println("Extension function") }

Example().printFunctionType() // Imprime "Class method"
```

Para funciones de extensión de objetos _que puedan ser nulos_ utilizamos el [operador `?`](#operador-seguro-):

```Kotlin
fun Any?.toString(): String { 
    if (this == null) return "null" 
    /* Después de esta comprobación, el tipo receptor 
    se castea a su versión no nullable.*/
    return toString() 
}
```


> [!NOTE]
> Generalmente las funciones de extensión se declaran a nivel superior, aunque es posible declararlas como miembros de una clase. Cuando esto ocurre, existen **múltiples receptores implícitos** dentro de la clase. 
> - _Receptor de despacho_: Instancia de la clase en la que se declara la extensión.
> - _Receptor de extensión_: Instancia del tipo receptor del método de la extensión.

Por ejemplo:

```kotlin
class Host(val hostname: String) {
    fun printHostname() { print(hostname) }
}

class Connection(val host: Host, val port: Int) {
    fun printPort() { print(port) }

    fun Host.printConnectionString() {
        printHostname()   // llama Host.printHostname() (Receptor de extensión)
        print(":")
        printPort()   // llama Connection.printPort() (Receptor de despacho)
    }

    fun connect() {
        /*...*/
        host.printConnectionString()   //  llama a la función de extensión
    }
}

fun main() {
    Connection(Host("kotl.in"), 443).connect()
    //Host("kotl.in").printConnectionString()  
    /*Provoca error puesto que la función de extensión 
    no es visible fuera de Connection */
}
```

Pueden existir conflictos entre los dos receptores, por lo que es importante tener en cuenta cómo se resuelven. El receptor de extensión **siempre** tiene prioridad. Para hacer referencia al miembro del receptor de despacho se utiliza la palabra reservada `this@`:

```kotlin
class Connection { 
    fun Host.getConnectionString() { 
        toString() // llama Host.toString() 
        this@Connection.toString() // llama Connection.toString() 
    } 
}
```

>[!NOTE]
>Además, las funciones de extensión miembro de una clase pueden ser declaradas como **`open`** y por tanto sobreescritas en las subclases. Una función de extensión declarada fuera de su tipo receptor _no puede acceder a sus miembros declarados como`private`o `protected`_.

Las funciones se desarrollan más [en su apartado correspondiente](#conceptos-avanzados)

[^17]: _Functions | Kotlin_. (s. f.). Kotlin Help. [https://kotlinlang.org/docs/functions.html](https://kotlinlang.org/docs/functions.html)
[^18]: Revelo, J. (2021, 25 agosto). Funciones en Kotlin - develou. _Develou_. [https://www.develou.com/funciones-en-kotlin/](https://www.develou.com/funciones-en-kotlin/)
[^19]: _Extensions | Kotlin_. (s. f.). Kotlin Help. [https://kotlinlang.org/docs/extensions.html](https://kotlinlang.org/docs/extensions.html)

# POO - Clases y objetos

Kotlin, al igual que Java, está orientado a objetos y por tanto permite encapsular en objetos tanto su estado (valor de las propiedades) como su funcionalidad (métodos).

>[!NOTE]
>Cuando se crea una clase en Kotlin por defecto será **public** y **final**. Para que se pueda heredar de ella tendremos que declararlo explícitamente con el modificador **`open`**.

Podemos crear una clase de la siguiente forma:
```Kotlin
//Fichero Persona.kt
class Persona {
    var soltera = true
      
    fun casarse() {
        soltera = false
    }
}
```

E instanciarla de la siguiente manera:
```Kotlin
val anselmo = Persona()
```

En el ejemplo vemos cómo se ha usado el constructor por defecto. Además, a diferencia de Java, _no se usa la palabra reservada `new`_. Y, por supuesto, se infiere que `anselmo` será de tipo `Persona`.
## Conceptos básicos
### Constructores
Podemos crear un constructor en la misma cabecera de la clase, de forma similar a como se definen los parámetros de una función. A este constructor se le conoce como _constructor primario_:
```Kotlin
//Fichero Persona.kt
class Persona(var nombre: String = "", //constructor primario
              var dni: String? = null,
              var edad: Int = 0) {
              
    var soltera = true
    
    fun casarse() {
        this.soltera = false
    }
}
```

En el caso anterior decimos que la clase Persona tiene los atributos: `nombre`, `dni`, `edad` y `soltera`. Y todos ellos son públicos por defecto. También serán mutables, puesto que los hemos declarado usando la palabra reservada **`var`**.


>[!WARNING]
>Si `nombre`, `dni` y `edad` no tienen el modificador `var`/`val`, no serían visibles ni siquiera dentro de la propia clase. En la sección de [Bloques de inicialización](#bloques-de-inicializacion) veremos la utilidad de estos parámetros.

Para instanciar un objeto a partir de la clase anterior:
```Kotlin
//Fichero Main.kt
val persona = Persona("Anselmo", "12345678A", 33)
```

Se puede observar que cada propiedad tiene un _valor por defecto_. Aquellos que lo tengan se conocen como _propiedades o parámetros opcionales_ ya que, si se crea un objeto sin pasar valores (constructor por defecto), se le asignan esos valores por defecto.

Si necesitamos otros constructores (como ocurría en Java), conocidos como constructores secundarios, podemos definirlos con la palabra reservada **`constructor`** de la siguiente forma:
```Kotlin
//Fichero Persona.kt
class Persona(var nombre: String = "",
              var dni: String? = null,
              var edad: Int = 0) {

    var soltera = true
    constructor(nombre: String,
                dni: String,
                edad: Int,
                soltera: Boolean
    ) : this(nombre, dni, edad) { //Referencia al constructor primario
        this.soltera = soltera
    }
    
    fun casarse() {
        this.soltera = false
    }
}
```

Así, el constructor primario inicializa los atributos `nombre`, `dni`y `edad` usando el constructor primario (`this(nombre, dni, edad)`) mientras que el constructor secundario inicializa, además de los anteriores, el atributo `soltera`.

Para instanciar objetos usando todos los constructores posibles:

```Kotlin
val maria = Persona("María Pérez", "00000000Z", 45)

val pelayo = Persona("Pelayo López", "111111111A", 45, false)

val anonimo = Persona()
 ```
  
### Getters y Setters

Podríamos implementar setters y getters como se hacía en Java. Así, para el ejemplo anterior:
```Kotlin
class Persona...    
    // getters
    fun getNombre(): String { return this.nombre }
    fun getDni(): String { return this.dni }
    fun getEdad(): Int { return this.edad }
    fun getSoltera(): Boolean { return this.soltera }
  
    // setters
    fun setNombre(nuevoNombre: String) { this.nombre = nuevoNombre }
    fun setDni(nuevoDni: String) { this.dni = nuevoDni }
    fun setEdad(nuevaEdad: Int) { this.edad = nuevaEdad }
    fun setSoltera(soltera: Boolean) { this.soltera = soltera }

. . .
```

Y esto funciona correctamente, pero no son los getters y setters reales.

Por defecto, las propiedades en Kotlin no necesitan setters y getters ya que son públicas. Es decir, esto:
```Kotlin
var nombre: String = "Pepe"
```

sería equivalente a esto otro:

```Kotlin
var nombre: String = "Pepe"
    get() {
        return field
    }
    
    set(value) {
        field = value
    }
```

Donde **`field`** hace referencia a la propiedad nombre y **`value`** se refiere al valor asignado.

Cada propiedad que definimos está referenciada por un campo al que solo se puede acceder dentro de sus métodos **`get()` y `set()`** mediante la palabra reservada `field`. Ésta se utiliza para acceder o modificar el valor de la propiedad. Esto nos permite definir una lógica personalizada dentro de los métodos `get()` y `set()`:

  ```Kotlin
var nota: Int = 4
    get() {
        if (field < 5)
            println("Suspenso.")
            return field
    }
    
    set(value) {
        field = when{
            value > 10 -> 10
            value < 0 -> 0
            else -> value
        }
    } 
```

Podemos modificar el acceso de las propiedades. Por ejemplo, para el ejemplo anterior, si ponemos el set como privado:

```Kotlin
private set(value) { 
    . . . 
}
```

Permitimos que se vea la propiedad desde fuera de la clase, pero el _`set` sólo podrá utilizarse dentro del objeto_.

En el siguiente ejemplo se puede ver cómo las propiedades `x` e `y` pueden modificarse sólo desde dentro de la clase `Plane`. En este caso no tendremos una condición dentro del setter, por lo que podremos omitir el cuerpo y el parámetro `value`, dejando la declaración como `private set`:

```Kotlin
class Plane {
    var x: Int = 0 
        private set
    var y: Int = 0
        private set
        
    fun moveLeft() {
        x -= if (x == 0) 0 else 1
    }

    fun moveRight() {
        x += if (x == 300) 0 else 1
    }

    fun moveUp() {
        y -= if (y == 0) 0 else 1
    }

    fun moveDown() {
        y += if (y == 300) 0 else 1
    }
}
```
### Bloques de inicialización
Llegados a este punto podemos encontrar sentido a un constructor primario como este:

```Kotlin
//Fichero Persona.kt
class Persona(
    nombre: String = "",
    dni: String? = null,
    edad: Int = 0
) {
. . .
}
```

Los parámetros del constructor sin un modificador `var`/`val` *no pueden ser usados ni fuera ni dentro de la clase*. Son simplemente parámetros locales del constructor.

Los bloques `init` sirven para realizar lógicas de inicialización complejas que no se pueden hacer directamente en la declaración de propiedades. Algunos ejemplos son validaciones, cálculos o lógicas condicionales que requieren más de una línea. Puede haber varios bloques `init`, que se ejecutarán por orden.

Antes de las versiones más recientes de Kotlin, era común usar bloques `init` para inicializar propiedades:

```Kotlin
class Persona(
    nombre: String = "",
    dni: String? = null,
    edad: Int = 0
) {
    var nombre: String
    var dni: String?
    var edad: Int
    var soltera: Boolean
    
    init {
        this.nombre = nombre
        this.dni = dni ?: ""
        this.edad = if (edad < 0) 0 else edad
        this.soltera = false
    }
. . .
}
```

En la actualidad, Kotlin permite inicializar directamente las propiedades en su declaración, lo que simplifica el código:

```Kotlin
class Persona(
    nombre: String = "",
    dni: String? = null,
    edad: Int = 0
) {
    var nombre: String = nombre
    var dni: String? = dni
    var edad: Int = if (edad < 0) 0 else edad
    var soltera: Boolean = false 
}
```

>[!TIP]
>Utiliza los bloques `init` siguen siendo útiles para lógicas de inicialización más complejas que no se pueden resolver en una línea.

## Herencia

En Kotlin las clases son finales por defecto. Es decir, no se puede heredar de ellas. Para evitar esto, hay que indicar que la clase sea **`open`**:

```Kotlin
open class Persona(
            var nombre:String,
            var dni:String,
            var edad:Int
            )

class Empleado(nombre:String,
              dni:String,
              edad:Int,
              var sueldo: Float): Persona(nombre, dni, edad) 

fun main() {
    val persona1 = Persona("Anselmo", "88888888X", 32)
    val empleado1 = Empleado("Pelayo", "11111111A", 41, 1500f)
    println(persona1.nombre)
    println(empleado1.nombre)
}

//—------------------------------------------
//~$ Anselmo
//~$ Pelayo
```
[Prueba este código ▶](https://pl.kotl.in/M2Tm9IOMr)

Como ya hemos comentado antes, no es necesario hacer getters o setters, siempre y cuando en el constructor primario se haya escrito var o val antes de las propiedades de la clase, esto también incluye las clases que han heredado.

Para más información consulta los siguientes enlaces:
- [https://www.develou.com/herencia-en-kotlin/](https://www.develou.com/herencia-en-kotlin/
- [https://kotlinlang.org/docs/inheritance.html](https://kotlinlang.org/docs/inheritance.html)

## Interfaces

En Kotlin, las interfaces sirven para definir comportamientos comunes que pueden compartirse o implementarse en varias clases que no necesariamente tienen que estar relacionadas las unas con las otras.
### Definición de interfaces
Para definir una interfaz en Kotlin, tendremos que hacer uso de la palabra clave `interface`. Una interfaz permite declarar métodos y propiedades. Las clases que implementan dicha interfaz deben cumplir con lo definido en la interfaz ya sea implementando el método o propiedad tal y como se definió en la interfaz, o sobreescribiendo para cambiar su comportamiento.

En Kotlin, una interfaz puede contener:
- **Métodos abstractos**: métodos que no tienen implementación. Las clases que implementen el interfaz deben codificar dichos métodos para definir su comportamiento.
- **Métodos con implementación**: estos métodos ya tienen un comportamiento predeterminado, según la clase en la que se implemente la interfaz se puede sobreescribir el método o usar el comportamiento predeterminado.

Ejemplo de una interfaz con un método abstracto y un método con implementación:
```Kotlin
interface Coche {
    fun Arrancar() //Método abstracto
    fun Parar() { //Método con implementación
        println("El coche se detiene.")
    }
}
```

- **Propiedades abstractas**: una propiedad abstracta no tiene un estado real (no almacena un valor), sino que la clase que implemente la interfaz debe proporcionarle un valor.
- **Propiedad con implementación**: una propiedad con implementación es simplemente una propiedad que tiene un valor predeterminado que puede ser modificado en la clase en la que se implemente la interfaz.
- 
Ejemplo de una interfaz con una propiedad abstracta y una propiedad con implementación:
```Kotlin
interface ComportamientoEducado {
    var nombre: String       // Propiedad abstracta
    val edad: Int get() = 19 // Propiedad con implementación 
    
    fun saludar() {
        println(
        "Hola, soy $nombre y tengo $edad años")
    }
}
```

### Implementación de una interfaz en una clase
Como ya hemos mencionado, si una clase implementa una interfaz, esta clase debe de definir los métodos y las propiedades abstractas que se han declarado en la interfaz.

Por ejemplo:
```Kotlin
/**
 * Indicamos que la propiedad abstracta nombre debe de ser 
 * proporcionada cuando se cree un objeto Maestro
 */
class Maestro(override val nombre: String): ComportamientoEducado {

   /** 
    * Sobreescribimos el método saludar para que nos dé la 
    * salida que deseamos
    */
    override fun saludar() {
        println("Hola soy $nombre, tengo $edad años y soy maestro.")
    }
}
```

Si observamos la clase anterior, podremos ver que para indicar que implementaremos la interfaz `ComportamientoEducado`, debemos hacerlo en la cabecera de la clase:

```Kotlin
class Maestro : ComportamientoEducado { . . . }
```

Pero como en la interfaz `ComportamientoEducado` hemos declarado la propiedad `nombre`, que es abstracta, para asegurar que se le da un valor debemos incluirla en el constructor primario del objeto `Maestro`, indicando con la palabra reservada **`override`** que sobreescribe la propiedad `nombre` de la interfaz:

```Kotlin
class Maestro(override val nombre: String) : Persona {. . .}
```

### Implementación de múltiples interfaces en una clase
En Kotlin, una clase puede implementar _múltiples interfaces_, lo que podría llegar a suponer un problema si dichas interfaces tuvieran métodos con el mismo nombre. Kotlin necesitaría una forma de saber a cuál de estos métodos tratamos de referirnos.

La responsable de resolver el conflicto es la clase en la que se implementan las interfaces, indicando explícitamente qué método usará y a qué interfaz pertenece el método en cuestión.

```Kotlin
// Declaramos la interfaz Caminante 
interface Caminante {
    fun moverse() {
        println("Caminando")
    }
}

// Declaramos la interfaz Nadador 
interface Nadador {
    fun moverse() {
        println("Nadando")
    }
}

// Implementamos las interfaces Caminante y Nadador 
class Triatleta : Caminante, Nadador {
    override fun moverse() {
       /*Indicamos que usaremos el método moverse() de la 
        * interfaz Caminante 
        */
        super<Caminante>.moverse()
    }
}
```
## Data classes
Las clases de datos son usadas para guardar información. Aquí tenemos un ejemplo de cómo nombrar una Data Class:

```Kotlin
data class Persona (val nombre: String, var edad: Int)
```

El compilador automáticamente, derivará los siguientes métodos teniendo en cuenta las propiedades del constructor primario:

- `equals()`: Dos objetos serán iguales si el contenido significativo de los mismos también lo son, esto es que sus valores son iguales.
- `hashCode()`: Devuelve un número entero que representa el objeto.
- `toString()`: Devuelve una cadena que representa el objeto.
- `componentN()`: Es una función usada para obtener la información de la propiedad en orden de declaración, en el caso del ejemplo de arriba el `component1()` de esa clase `Persona` es el `nombre` que se le haya asignado al crear el objeto. Se utiliza en la declaraciones destructuradas. 
- `copy()`: usado para crear la copia de un objeto ya creado, además entre paréntesis podremos cambiar alguno de los datos.

```Kotlin
val user = User("Jane", 35) 
val (name, age) = user //Asignación destructurada
println("$name, $age años") // Jane, 35 años
```

A continuación un ejemplo de `data class`:

```Kotlin
data class Persona(val nombre:String, var edad:Int)

fun main(){
    val persona1 = Persona("Anselmo", 30)
    //toString()
    println(persona1.toString())
    
    //componentN()
    println(persona1.component1())
    
    println(persona1.component2())
    
    //copy()
    //Vamos a cambiar el nombre, pero dejaremos la misma edad
    val persona2 = persona1.copy(nombre = "Pepe")
    println(persona2.component1())
    
    println(persona2.component2())
    val persona3 = Persona("Anselmo", 30)
    //Usamos el equals
    println(persona1.equals(persona2))
    println(persona1.equals(persona3))
}
```
[Prueba este código ▶](https://pl.kotl.in/BAUoJ0l4G)


>[!IMPORTANT]
>Es importante remarcar que para garantizar la coherencia y el comportamiento significativo del código generado, se tienen que cumplir los siguientes requisitos:
>- El constructor primario tiene que tener al menos un parámetro
>- Todos los parámetros del constructor primario tienen que ser precedidos por var o val.
>- Las clases de datos _no pueden ser abstractas, abiertas, selladas o internas_.

Podremos excluir propiedades de este tipo de clases. El compilador usará solo aquellos atributos que se encuentren en el constructor principal para crear los métodos de utilidad vistos y dichos anteriormente.

```Kotlin
data class Persona(val nombre:String, var edad:Int){
    var colorPelo: String? = null //No incluido en los métodos
}

fun main(){
    var perso1 = Persona("Juan", 21)
    var perso2 = perso1.copy()
    
    perso1.colorPelo = "Verde"
    perso2.colorPelo = "Amarillo"
    println(perso1.equals(perso2))
}
//—-------------------------------------
//~$ true
```
[Prueba este código ▶](https://pl.kotl.in/fboZK7wiH)

Como puedes observar, el valor de `colorPelo` no afecta a la igualdad entre los dos objetos, porque no se tiene en cuenta en el método `equals()`.

Este tipo de clases se suelen usar para crear modelos de almacenamiento sin tener que escribir código repetitivo. Una `data class`es más fácil y rápida de manipular y comparar.

Para más información consulta los siguientes artículos:
- [https://kotlinlang.org/docs/data-classes.html](https://kotlinlang.org/docs/data-classes.html
- [https://www.develou.com/data-classes-en-kotlin/](https://www.develou.com/data-classes-en-kotlin/)
## Enum  
Los `enum`[^22] en Kotlin proporcionan una forma de crear conjuntos de constantes de tipo seguro, ofreciendo una implementación robusta y flexible de enumeraciones.

El caso de uso más básico para un `enum` es representar un conjunto de tipos seguros.

```kotlin
enum class Direction {
    NORTH, SOUTH, WEST, EAST
}
```

Cada constante dentro de un `enum` es un objeto. Como a su vez los `enum`son instancias de la clase `Enum`, pueden ser inicializados con un constructor.

```kotlin
enum class Color(val rgb: Int) {
    RED(0xFF0000),
    GREEN(0x00FF00),
    BLUE(0x0000FF)
}
```

Dentro de cada constante de un `enum` es posible declarar clases anónimas con sus propios métodos, e incluso sobreescribir métodos ya existentes.

```kotlin
enum class ProtocolState {
    WAITING {
        override fun signal() = TALKING
    },
    TALKING {
        override fun signal() = WAITING
    };

    abstract fun signal(): ProtocolState
}
```

>[!NOTE]
>Observa que la declaración de las constantes se separa del resto de código del `enum`, como las funciones del mismo, mediante un **punto y coma** `;`.

Los enums no pueden extender de otras clases, pero sí implementar interfaces, bien mediante una implementación genérica para todas las constantes del enum o mediante una implementación específica para cada constante mediante clases anónimas.

```kotlin
enum class IntArithmetics : BinaryOperator<Int>, IntBinaryOperator {
    PLUS {
        override fun apply(t: Int, u: Int): Int = t + u
    },
    TIMES {
        override fun apply(t: Int, u: Int): Int = t * u
    };

    override fun applyAsInt(t: Int, u: Int) = apply(t, u)
}
```

>[!TIP]
>Las clases `enum` en Kotlin implementan por defecto la interfaz `Comparable`.

### Métodos y Propiedades Sintéticos
Las clases enum tienen una serie de métodos y propiedades sintéticos que se generan automáticamente y sirven para listar las constantes del enum, obtener un enum por su nombre, o acceder a sus propiedades.

```kotlin
enum class RGB { RED, GREEN, BLUE }

fun main() {
    // Iterar sobre todas las entradas
    for (color in RGB.entries) {
        println(color.toString())
    }

    // Obtener un enum por su nombre
    println(RGB.valueOf("RED"))
}
```

Desde **Kotlin 1.9.0** se accede a las entradas de un enum con la propiedad `entries`. También podemos obtener el nombre de una constante con la propiedad `name` y su posición de declaración con la propiedad `ordinal`.

```kotlin
println(RGB.entries)     // Imprime [RED, GREEN, BLUE]
println(RGB.RED.name)    // Imprime "RED"
println(RGB.RED.ordinal) // Imprime 0
```

Con la función `enumEntries<T>()` podemos obtener las constantes de un enum de un tipo específico `T`.

[^22]:_Enum classes | Kotlin_. (s. f.). Kotlin Help. [https://kotlinlang.org/docs/enum-classes.html](https://kotlinlang.org/docs/enum-classes.html)
# Conceptos avanzados

Kotlin ofrece algunas opciones para mejorar y fortalecer nuestro código. Veamos algunas.
## Funciones de extensión

Las funciones de extensión en Kotlin permiten agregar nuevas funcionalidades a clases existentes sin modificar su código fuente. Veámoslo con un ejemplo.  Aunque las funcionalidades pueden ser innecesarias, si son ilustrativas y ayudan a entender en qué consisten estas funciones.

Supongamos que necesitamos un par de funcionalidades específicas para las cadenas de texto en nuestra aplicación: una eliminará todos los espacios en blanco y la otra pondrá la primera letra de la cadena en mayúscula. Para ello crearemos estas dos funciones o métodos en alguna de las clases:

```Kotlin 
fun String.sinEspacios(): String {
    return this.replace(" ", "")
}

fun String.primeraMayuscula(): String {
    return this.replaceFirstChar{ it.uppercase() }
}

fun String.esPalindromo(): Boolean {
    return this == this.reversed()
}
```

De esta forma hemos añadido a la clase `String` las funcionalidades `sinEspacios()` y `primeraMayuscula()` y las puedo usar con cualquier objeto `String`:

```Kotlin
val quiniela = "          1  x         2 ".sinEspacios()
//quiniela = "1x2"
. . .
var nombre = "pepe".primeraMayuscula() 
// Pepe
. . .
var palindromo = "opo".esPalindromo() 
// true
```
  
Veamos más ejemplos con otras clases conocidas:

```Kotlin
//Crea un rango desde el nº hasta el final indicado:
fun Int.rangeTo(hasta: Int): IntRange {
    return this..hasta
}

//Repite una cadena de texto tantas veces como indique el entero:
fun Int.repetir(cadena: String): String {
    return cadena.repeat(this)
}

//Indica si un nº es par
fun Int.esPar(): Boolean {
    return this % 2 == 0
}

//Invierte el valor booleano
fun Boolean.not(): Boolean {
    return !this
}

//—--------------------------
// Cómo se usan:

for (i in 3.rangeTo(12) {
    . . .
}
. . .

println(3.repetir("textoRepetido "))
//Imprime: textoRepetido textoRepetido textoRepetido 
. . .
println(7.esPar())
//false
. . .

val esMenor = false

println(esMenor) //false

println(esMenor.not()) //true
```

>[!TIP]
>Puedes ver más ejemplos de funciones de extensión [aquí](https://cursokotlin.com/funciones-de-extension-en-kotlin-capitulo-36/)[^20]
  
[^20]:Aris. (2023, 15 enero). _Funciones de extensión en Kotlin – Capítulo 36_. Curso Kotlin Para ANDROID. https://cursokotlin.com/funciones-de-extension-en-kotlin-capitulo-36/

## Funciones de orden superior
Son funciones que cumplen alguna de estas condiciones:
- Reciben otras funciones como parámetros.
- Devuelven una función como resultado.

En esencia, las funciones de orden superior tratan a las funciones como ciudadanos de primera clase, permitiéndote manipularlas y pasarlas como datos.
Existen algunas funciones predefinidas, como:

### `map()`
Aplica una transformación a cada elemento de una colección y devuelve una nueva lista con los resultados.

```Kotlin
val numeros= listOf(1, 2, 3, 4)
val numerosDobles = numeros.map { it * 2 } // [2, 4, 6, 8]
```

En este ejemplo, `map()` toma una función como argumento (en este caso, `{ it * 2 }`) y la aplica a cada elemento de la lista.

### `filter()`
Filtra los elementos de una colección según una condición.

```Kotlin
val numeros = listOf(1, 2, 3, 4, 5)
val numerosPares = numeros.filter { it % 2 == 0 } // [2, 4]
```

Aquí, `filter()` toma una función que devuelve un booleano y filtra los elementos que cumplen la condición.

### `reduce()`  
Combina todos los elementos de una colección en un único valor.

```Kotlin
val numeros = listOf(1, 2, 3, 4, 5)
val suma = numeros.reduce { acc, element -> acc + element }
println(suma) // Imprime: 15
```

`reduce()` toma una función como argumento que tiene dos parámetros:
- `acc`: el valor acumulado hasta el momento.
- `element`: el elemento actual de la lista.
La función que pasamos a `reduce()` en el ejemplo suma el elemento actual al valor acumulado.
La operación de reducir comienza con el primer elemento como valor acumulado y luego aplica la función a cada elemento sucesivo.

### `forEach()`  
Ejecuta una acción para cada elemento de una colección.

```Kotlin
val nombres = listOf("Ana", "Pedro", "Laura", "David")

nombres.forEach { nombre ->
    println(nombre)
}
```

El `forEach()` recorre la lista de nombres y los imprime línea a línea. El argumento de la función lambda es el elemento actual de la colección.
### Funciones como parámetros
También podemos definir funciones propias. Por ejemplo:

```Kotlin
fun calcular(
            num1: Int,
            num2: Int,
            operacion: (Int, Int)->Int
            ): Int {
    return operacion(num1, num2)
}
```

El último parámetro de la función calcular es una función llamada `operacion` que recibe dos enteros y devuelve un entero. Podremos introducir cualquier función que admita dos enteros como parámetros y devuelva un entero como resultado, sea la que sea.

Ahora definimos algunas funciones que cumplan con dicha cabecera:

```Kotlin
fun sumar(a: Int, b: Int): Int { return a + b }
fun restar(a: Int, b: Int) = a - b
fun multiplicar(a: Int, b: Int): Int { return a * b }
fun dividir(a: Int, b: Int) = if (b != 0) a/b else 0
```

Todas las funciones devuelven el resultado, aunque el `return` se exprese de distintas formas.
Veamos cómo pasar cualquiera de estas funciones como parámetro en la función `calcular`:

```Kotlin
val suma = calcular(4, 5, ::sumar)
val resta = calcular(4, 5, ::restar)
val producto = calcular(4, 5, ::multiplicar)
val division = calcular(4, 5, ::dividir)
```

Veamos otro ejemplo, esta vez dentro de la clase `Persona` que hemos definido anteriormente. Añadimos en ella el siguiente método:

```Kotlin
fun puedeConducir(conducir: (Int) -> Boolean): Boolean {
    return conducir(edad)
}
```

Ahora imaginemos que definimos fuera de la clase varias funciones que cumplan con esa cabecera (admite un entero como parámetro y devuelve un valor lógico):

```Kotlin
fun enFrancia(edad: Int): Boolean {
    return edad >= 19
}

fun enEspana(edad: Int): Boolean {
    return edad >= 18
}

fun enIslandia(edad: Int): Boolean {
    return edad >= 16
}  

val juanito = Persona("Juanito Pérez", "00000000Z", 16)

println(juanito.puedeConducir(::enFrancia))  //false
println(juanito.puedeConducir(::enEspana))   //false
println(juanito.puedeConducir(::enIslandia)) //true
```

¿Y si la clase `Persona` fuera de una librería que no podemos tocar? En tal caso podemos implementar `puedeConducir` como una _función de extensión_ de `Persona`:

```Kotlin
// En algún lugar de nuestro código:
fun Persona.puedeConducir(conducir: (Int) -> Boolean): Boolean {
    return conducir(edad)
}
```

### Funciones como resultado
También podemos definir el tipo de dato de salida de una función como otra función:
  
  ```Kotlin
fun crearSaludo(prefijo: String): (String) -> String {
    return { nombre -> "$prefijo $nombre" }
}
```

La función anterior devuelve una función que toma un nombre y devuelve un saludo personalizado.

El prefijo se captura en el momento de llamar a la función:

```Kotlin
val saludoFormal = crearSaludo("Estimado/a")

println(saludoFormal("Ana")) // Imprime: Estimado/a Ana
```

En este caso, la variable `saludoFormal` es de tipo `(String) -> String` (una función). Es decir, admite una cadena de texto como parámetro de entrada y devuelve un texto.
## Lambdas
En los apartados anteriores hemos visto cómo una función puede pasarse como parámetro a otra función. De la misma forma, _una función puede asignarse a una variable_. Hasta ahora hemos usado las variables para almacenar datos de distintos tipos, pero las variables también pueden almacenar bloques de código. Por ejemplo:

```Kotlin 
var imprimirMensaje: (String) -> Unit = { nombre ->
    println("Te damos la bienvenida, $nombre !")
}

imprimirMensaje("Pepe")    // Te damos la bienvenida, Pepe !
```

En estos casos, el tipo de dato se define como una función con esta forma:
```Kotlin
(Tipo_param_1, Tipo_param2, …) -> Tipo_retorno
```

La flecha `->` equivale al `return` de la función.
En caso de que la función no vaya a devolver ningún dato, se utiliza el tipo `Unit`.

>[!NOTE]
> Recuerda que `Unit`es un tipo de dato especial con una única instancia. Se utiliza para indicar que una función no devuelve nada. En Java, el equivalente sería `void`, con la diferencia de que en Kotlin sí que devuelves algo, un objeto de tipo `Unit`. En la mayoría de contextos `Unit`está implícito y no hace falta indicarlo.

Otro ejemplo donde se ve la estructura del tipo de dato función:

```Kotlin
var opAritmetica: (Int, Int) -> Int = { x, y -> x + y }
println(opAritmetica(3, 4))
```

En este caso, la variable `opAritmetica` almacena un bloque de código (`{}`) correspondiente a una función con dos parámetros enteros de entrada (`x` e `y`) que devuelve la suma entera de ambos.

Al tratarse de una función, podría usarse con la función `calcular` de ejemplos anteriores:

```Kotlin
var opAritmetica: (Int, Int) -> Int = { x, y -> x + y }
println(calcular(3, 4, opAritmetica))
```

>[!NOTE]
>Al tratarse de una variable, no hay que referenciarla con el operador de referencia [`::`](#operadores).

De esta forma, al tratarse de una variable, puede cambiar su valor o, en este caso, su funcionalidad simplemente asignándole otra función:

```Kotlin
var opAritmetica: (Int, Int) -> Int = { x, y -> x + y }
println(calcular(3, 4, opAritmetica)) //7

opAritmetica = { x, y -> x - y }
println(calcular(25, 7, opAritmetica)) //18
```

Si no usamos variables e introducimos directamente el código de la función en el parámetro, decimos que estamos usando una _lambda o función anónima_ (ya que no tiene nombre):

```Kotlin
println(calcular(25, 7, {x: Int, y: Int -> x + y}))
println(calcular(25, 7, {x: Int, y: Int -> x - y}))
```

Otro ejemplo con un cuerpo algo más extenso, en este caso para calcular una pontencia:

```Kotlin
println(
    calcular(2, 8, { base, exp ->
            var producto = 1
            for(i in 1..exp) producto *= base
            producto
        }
    )
)
```

En este código se puede observar:
- *La cabecera* (`base` y `exp`, que se entiende que serán los enteros 2 y 8 respectivamente).
- *El cuerpo de la función*, entre llaves.
- *El valor de retorno* pero sin usar la palabra `return`, ya que va implícito en la flecha `->`. 

Al implementar esta lambda, el propio editor nos sugiere que la saquemos del paréntesis. Al hacerlo quedaría así:

  ```Kotlin
println(
    calcular(2, 8)) { base, exp ->
        var producto = 1
        for(i in 1..exp) producto *= base
        producto
    }
)    //quitamos un paréntesis, ya que se ha cerrado arriba
```

El sacar la lambda de los paréntesis puede hacer creer que ya no se trata de un parámetro de la función calcular, pero no es así. La lambda sigue siendo un parámetro en dicha función.

Esto explica cosas como la declaración de un array de enteros con todos los valores inicializados a un valor. En el siguiente ejemplo, el segundo parámetro del constructor es una lambda:

```Kotlin
val numeros = IntArray(5, {1}) // {1, 1, 1, 1, 1}

//Al ser una lambda, puede sacarse de los paréntesis:
val numeros2 = IntArray(5) {1} // {1, 1, 1, 1, 1}

val numeros3 = IntArray(5) {it} // {0, 1, 2, 3, 4}
```

Es decir, `IntArray` es una función de orden superior ya que admite funciones como parámetros y cuyo parámetro de entrada (`it`) es el índice del array. También podríamos llamar a la función de la siguiente forma:

```Kotlin
val numeros3 = IntArray(5) {i -> i * 2} // {0, 2, 4, 6, 8}
```

#### Niveles de acceso
Las variables que se declaren dentro de un bloque de código pueden ser usadas dentro del mismo (_lo que se conoce como ámbito_). Aunque las variables que declaramos dentro de una lambda no pueden salir de su ámbito, sí que se puede acceder a las variables declaradas en el ámbito donde se declara la lambda desde dentro de esta. Veámoslo con el siguiente ejemplo:

```Kotlin
fun recorrerArray(listaNumeros: IntArray, fn: (Int) -> Unit){
    for (numero in listaNumeros)
        fn(numero)
}
```

Podemos llamar a esta función pasándole por parámetro la siguiente lambda:

```Kotlin
var suma = 0
var producto = 1
var arrayNumeros = IntArray(5){it}
  
recorrerArray(arrayNumeros){
    suma += it
    producto *= it
}
```

Podemos renombrar el parámetro de entrada:
```Kotlin
recorrerArray(arrayNumeros){ numero ->
    suma += numero
    producto *= numero
}
```

## Type alias
Los type aliases (alias de tipos) en Kotlin permiten crear nombres alternativos para tipos existentes, lo que puede simplificar el código y hacerlo más legible. [^21]

Podemos usarlos por ejemplo para simplificar declaraciones de tipos genéricos largas.
```kotlin
// Alias para un conjunto de nodos de red
typealias NodeSet = Set<Network.Node>

// Alias para un mapa de archivos
typealias FileTable<K> = MutableMap<K, MutableList<File>>
```

Otro caso de uso sería el de dar nombres más simples a los tipos de función.

```kotlin
// Alias para un manejador de eventos
typealias MyHandler = (Int, String, Any) -> Unit

// Alias para un predicado genérico
typealias Predicate<T> = (T) -> Boolean
```

También se pueden usar para hacer referencia a clases anidadas (`nested`e `inner`).

```kotlin
class A {
    inner class Inner
}
class B {
    inner class Inner
}

// Creando alias para clases internas
typealias AInner = A.Inner
typealias BInner = B.Inner
```

>[!TIP]
>- Los type aliases no crean tipos completamente nuevos
>- Son equivalentes a sus tipos subyacentes
>- El compilador de Kotlin los expande automáticamente

```kotlin
// Definición del type alias
typealias Predicate<T> = (T) -> Boolean

// Función que usa el type alias
fun foo(p: Predicate<Int>) = p(42)

fun main() {
    // Uso directo de función lambda
    val f: (Int) -> Boolean = { it > 0 }
    println(foo(f)) // Imprime "true"

    // Usando el type alias
    val p: Predicate<Int> = { it > 0 }
    println(listOf(1, -2).filter(p)) // Imprime "[1]"
}
```

[^21]:_Type aliases | Kotlin_. (s. f.). Kotlin Help. [https://kotlinlang.org/docs/type-aliases.html](https://kotlinlang.org/docs/type-aliases.html)
## Fechas
Las fechas en Kotlin pueden ser tratadas con las clases **`LocalDate`y `LocalDateTime`** del paquete `java.time`.

```Kotlin
import java.time.LocalDateTime

fun main() {
    val fechaHoraActual = LocalDateTime.now()
    println(fechaHoraActual)
}
//—-----------------------------------
//~$ 2024-10-13T11:00:39.219977120
```

Estos datos son difíciles de interpretar para los humanos, por lo que podemos darles otro formato usando la clase *`DateTimeFormatter`*:

```Kotlin
import java.time.LocalDateTime
import java.time.format.DateTimeFormatter
  
fun main() {
    val fechaHoraActual = LocalDateTime.now()
    val formatoFecha1 = DateTimeFormatter
                        .ofPattern("EEEE, MMMM dd, yyyy")
    val formatoFecha2 = DateTimeFormatter
                        .ofPattern("dd-MM-yyyy")
    var fechaFormateada = fechaHoraActual
                        .format(formatoFecha1)
    println(fechaFormateada)
    fechaFormateada = fechaHoraActual
                    .format(formatoFecha2)
    println(fechaFormateada)
}
//—-----------------------------------
//~$ Sunday, October 13, 2024
//~$ 13-10-2024
```

Lo mismo ocurre con las horas, con la clase `LocalTime`:

```Kotlin
import java.time.LocalTime

fun main() {
    val horaActual = LocalTime.now()
    println(horaActual)
}

//—-----------------------------------
//~$ 11:12:16.308689063
```

Y aplicando formatos:

```Kotlin
import java.time.LocalTime
import java.time.format.DateTimeFormatter

fun main() {
    val horaActual = LocalTime.now()
    val formato24Horas = DateTimeFormatter
                        .ofPattern("HH:mm:ss")
                        
    val formato12Horas = DateTimeFormatter
                        .ofPattern("hh:mm a")
                        
    var horaFormateada = horaActual
                        .format(formato24Horas)
    
    println(horaFormateada)
    horaFormateada = horaActual.format(formato12Horas)
    println(horaFormateada)
}
  
//—-----------------------------------
//~$ 11:16:48
//~$ 11:16 AM
```