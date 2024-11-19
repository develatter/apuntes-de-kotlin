# Índice
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

—-----------------------------------
~$ String
```
  
Un String sigue siendo una secuencia de caracteres, al igual que en Java, por lo que Kotlin permite recorrerla carácter a carácter de forma sencilla:
  
```kotlin
var nombre = "Pepe"

for (caracter in nombre ) {

    println(caracter)

}
—-----------------------------------
~$ P
~$ e
~$ p
~$ e
```
  
Que sea inmutable significa al asignarle un valor, no se pueden cambiar. Si se reasigna otra cadena a una variable String, la cadena anterior se desreferencia y el __garbage collector__ se encargará de eliminarla. 

Esto también implica que cualquier método que ejecute, no cambiará el valor de la cadena. En su lugar creará otra cadena en memoria con el resultado de dicho método:

  ```Kotlin
var nombre = "Pepe"

println(nombre.uppercase()) // el resultado no se guarda en nombre

println(nombre)

—-----------------------------------
~$ PEPE
~$ Pepe
 ```
  
Puedes concatenar cadenas usando el operador +, pero es preferible usar plantillas de cadenas o cadenas multilínea. Para hacer cadenas mutables, al igual que en Java, podemos usar la clase [StringBuilder](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-string-builder/).

```Kotlin
var nombre = "Pepe"

println("Buenos días, " + nombre) // 👍

println("Buenos días, $nombre") // 👍👍👍👍

—-----------------------------------
~$ Buenos días, Pepe
~$ Buenos días, Pepe
 ```
  
Cuando usamos el operador _“+”_ hablamos de  __concatenación__. Cuando usamos plantillas para _referenciar_ a una variable, hablamos de _expansión de variables_. Las plantillas, también llamadas **String Templates**, son muy útiles, ya que no solo nos permiten llamar al valor de una variable sino que también es posible usarlas para evaluar expresiones. 

Para evaluar una expresión con una plantilla debemos rodearla entre llaves _`(${expresión})`_.
```Kotlin 


val uno = 1

val dos = 2

println("La suma de $uno y $dos es ${uno + dos}")

—----------------------------

~$ La suma de 1 y 2 es 3
```
[Prueba este código ▶](https://pl.kotl.in/nKK9sA8gF)

## Literales de Cadenas

Kotlin tiene [cadenas escapadas](https://kotlinlang.org/docs/strings.html#escaped-strings) (contienen caracteres escapados con **`\`**) y [cadenas multilínea](https://kotlinlang.org/docs/strings.html#multiline-strings) (delimitadas por triple comillas).

- __Cadenas escapadas__: estas cadenas contienen caracteres especiales que implican una acción: retorno de carro, tabulador, etc.
  
```Kotlin
val saludo = "Hola, Pepe!\nCómo ha ido el día?"

println(saludo)
—-----------------------------------
~$ Hola, Pepe!
~$ Cómo ha ido el día?
```

- **Cadenas multilínea**: permiten escribir un texto sin necesidad de usar caracteres escapados. Para ello, dicha cadena se delimita por triples comillas dobles.
  
```Kotlin
val saludo = """Hola, Pepe!

Cómo ha ido el día?""" // no necesita \n

println(saludo)

—-----------------------------------

~$ Hola, Pepe!
~$ Cómo ha ido el día?
```


Un método muy útil para evitar problemas de formato con las cadenas multilínea es __`.trimIndent()`__, el cual nos permite eliminar todos los espacios en blanco al principio de cada línea del String. De esta forma podemos escribir el literal de forma más legible sin que eso afecte a lo que se muestra por pantalla.
  
  ```Kotlin
val saludo = """
				Hola, Pepe!
				Cómo ha ido el día?
			 """.trimIndent()            //Ignora espacios 

println(saludo)
—-----------------------------------
~$ Hola, Pepe!
~$ Cómo ha ido el día?
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

—-----------------------------------

~$ Array
~$ 1..6

```

[^4]: Arrays from Ranges. (2017, 1 noviembre). Kotlin Discussions. [https://discuss.kotlinlang.org/t/arrays-from-ranges/5216](https://discuss.kotlinlang.org/t/arrays-from-ranges/5216)

##### Con el constructor Array

Indicando el tamaño inicial (entre paréntesis) y un valor inicial (entre llaves) para todos los elementos.
  
```Kotlin
val arrayNotasExamen = Array<Int>(6){10}

println(arrayNotasExamen.joinToString())

—-----------------------------------

~$ 10, 10, 10, 10, 10, 10  
```

También podemos hacerlo indicando el tamaño inicial (entre paréntesis) y una función que genera cada elemento del array indicando su índice

```Kotlin
val arrayNumeros = Array(10, { i -> i + 10 })

println(arrayNumeros.joinToString())

val arrayTextos = Array(10, { i -> (i + 10).toString() })

println(arrayTextos.joinToString())

—-----------------------------------

~$ Array
~$ 10, 11, 12, 13, 14, 15, 16, 17, 18, 19
~$ Array
~$ 10, 11, 12, 13, 14, 15, 16, 17, 18, 19
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

—-----------------------------------
~$ 10, 11, 12, 13, 14, 15, 16, 17, 18, 19
~$ 15
~$ 10, 11, 12, 13, 14, 0, 16, 17, 18, 19

```

Aunque lo veremos en los [rangos](https://docs.google.com/document/d/1NBdPPQc5gSjRZnafi34eAk254KPwL30mNZIiQkW4XKM/edit?tab=t.0#heading=h.dulvthaoy0bf), se puede usar el operador in para comprobar si un elemento está incluido en un array:

```Kotlin
var arrayCorto = arrayOf(1, 24, 3)

println(24 in arrayCorto)

—-----------------------------------
~$ true
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

—---------

//Al imprimir la matriz se habrá modificado el valor

~$ ***
~$ *-*
~$ ***
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
~$ Pepe
~$ null
```
## Operador seguro (?.)

Kotlin usa el operador seguro `?.` en variables nullables (podrían ser nulas) para permitir acceder a sus miembros (propiedades y métodos) de forma segura. Si el valor es nulo, la expresión completa se evalúa a null:

```Kotlin
var cadena: String? = null
val longitud: Int? = cadena?.length

println(longitud)

//—-----------------------------------
~$ null
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

~$ Pepe Expósito Fernández
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

for (i in 1+1..<100) { ... } //final y principio cerrados

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
[^16]: Conditions and loops | Kotlin. (s. f.-b). Kotlin Help. [https://kotlinlang.org/docs/control-flow.html#while-loops](https://kotlinlang.org/docs/control-flow.html#while-loops)
