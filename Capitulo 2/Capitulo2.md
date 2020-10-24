<a href="http://cooltext.com" target="_top"><img src="https://cooltext.com/images/ct_pixel.gif" width="80" height="15" alt="Cool Text: Logo and Graphics Generator" border="0" /></a>

<a href="https://cooltext.com"><img src="https://images.cooltext.com/5474893.png" width="316" height="88" alt="Capitulo 2" /></a>

# Tipos de datos y sentencias de alto nivel

### Modos de direccionamiento del RAM

En la arquitectura ARM los accesos a memoria se hacen mediante instrucciones específicas ldr y str (luego veremos las variantes ldm, stm y las preprocesadas push
y pop). El resto de instrucciones toman operandos desde registros o valores inmediatos, sin excepciones. En este caso la arquitectura nos fuerza a que trabajemos de
un modo determinado: primero cargamos los registros desde memoria, luego procesamos el valor de estos registros con el amplio abanico de instrucciones del ARM,
para finalmente volcar los resultados desde registros a memoria. Existen otras arquitecturas como la Intel x86, donde las instrucciones de procesado nos permiten
leer o escribir directamente de memoria. Ningún método es mejor que otro, todo es cuestión de diseño. Normalmente se opta por direccionamiento a memoria en
instrucciones de procesado en arquitecturas con un número reducido de registros, donde se emplea la memoria como almacén temporal. En nuestro caso disponemos
de suficientes registros, por lo que podemos hacer el procesamiento sin necesidad de interactuar con la memoria, lo que por otro lado también es más rápido.

**Direccionamiento inmediato**

El operando fuente es una constante, formando parte de la instrucción.

![](https://github.com/MelchorLuis/LecturaYEjercicios/blob/main/Capitulo%202/imagenes/direccionamiento%20inmediato.png?raw=true)

**Direccionamiento inmediato con desplazamiento o rotación**

Es una variante del anterior en la cual se permiten operaciones intermedias sobre los registros.

![](https://github.com/MelchorLuis/LecturaYEjercicios/blob/main/Capitulo%202/imagenes/rotacion.png?raw=true)

Estas instrucciones también se usan implicitamente para la creación de constantes, rotando o desplazando constantes más pequeñas de forma transparente al usuario. 
Como todas las instrucciones ocupan 32 bits, es técnicamente imposible que podamos cargar en un registro cualquier constante de 32 bits con la instrucción mov. 
Por esta razón cuando se necesita cargar una constante más compleja en un registro (como una dirección a una variable de memoria) no podemos hacerlo con la instrucción 
mov, tenemos que recurrir a ldr con direccionamiento a memoria.

**Direccionamiento a memoria, sin actualizar registro puntero**

Es la forma más sencilla y admite 4 variantes. Después del acceso a memoria ningún registro implicado en el cálculo de la dirección se modifica.
[Rx, #+inmediato]
[Rx, #-inmediato]
Simplemente añade (o sustrae) un valor inmediato al registro dado para calcular la dirección. Es muy útil para acceder a elementos fijos de un array, ya que el 
desplazamiento es constante. Por ejemplo si tenemos r1 apuntando a un array de enteros de 32 bits int a[] y queremos poner a 1 el elemento a[3], lo hacemos así:

![](https://github.com/MelchorLuis/LecturaYEjercicios/blob/main/Capitulo%202/imagenes/direccionamiento%20a%20memoria.png?raw=true)

### Tipos de datos

Tipos de datos básicos. En la siguiente tabla se recogen los diferentes tipos de datos básicos que podrán aparecer en los ejemplos, así como sutamaño y rango de representación.

|      ARM      |                           Tipo en C                           |     Bits    |                                      Rango                                      |
|:-------------:|:-------------------------------------------------------------:|:-----------:|:-------------------------------------------------------------------------------:|
| .byte         | unsigned char (signed) char                                   | 8 8         | 0 a 255 -128 a 127                                                              |
| .hword .short | unsigned short int (signed) short int                         | 16 16       | 0 a 65.535 -32.768 a 32767                                                      |
| .word .int    | unsigned int (signed) int unsigned long int (signed) long int | 32 32 32 32 | 0 a 4294967296 -2147483648 a 2147483647 0 a 4294967296 -2147483648 a 2147483647 |
| .quad         | unsigned long long (signed) long long                         | 64 64       | 0 a 2^64 -2^63 a 2^63-1                                                         |

Nótese como en ensamblador los tipos son neutrales al signo, lo importante es la longitud en bits del tipo. La mayoría de las instrucciones (salvomultiplicación) hacen 
la misma operación tanto si se trata de un número natural como si es entero en complemento a dos. Nosotros decidiremos el tipo mediante las constantes que pongamos o 
según los flags que interpretemos delresultado de la operación.

**Punteros**

Un puntero siempre ocupa 32 bits y contiene una dirección de memoria. En ensamblador no tienen tanta utilidad como en C, ya que disponemos de registros
de sobra y es más costoso acceder a las variables a través de los punteros que directamente. En este ejemplo acceder a la dirección de var1 nos cuesta 2 ldrs a través
del puntero, mientras que directamente se puede hacer con uno sólo.

![](https://github.com/MelchorLuis/LecturaYEjercicios/blob/main/Capitulo%202/imagenes/nano%20punteros.s.png?raw=true)

![](https://github.com/MelchorLuis/LecturaYEjercicios/blob/main/Capitulo%202/imagenes/punteros.png?raw=true)
