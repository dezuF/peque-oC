# Gramática de PequeñoC

PequeñoC es un subconjunto educativo de C. Los tipos de variable son `int` y
`float`. Los literales de cadena se aceptan únicamente como elementos de
`print`; no existe un tipo `string`.

## Gramática formal

Se define:

`G = (VT, VN, S, P)`

#### Terminales principales (VT):

- Palabras reservadas: `int`, `float`, `if`, `else`, `while`, `for`,
  `return`, `print`, `read`.
- Operadores aritméticos: `+`, `-`, `*`, `/`, `%`.
- Operadores relacionales: `<`, `>`, `<=`, `>=`, `==`, `!=`.
- Asignación: `=`.
- Delimitadores: `(`, `)`, `{`, `}`, `;`, `,`.
- Clases léxicas: `id`, `entero`, `real`, `cadena`.

#### No terminales principales (VN):

`<programa>`, `<funcion>`, `<tipo>`, `<parametros>`, `<parametro>`,
`<bloque>`, `<sentencia>`, `<declaracion>`, `<asignacion>`,
`<condicional>`, `<ciclo_while>`, `<ciclo_for>`, `<retorno>`,
`<impresion>`, `<lectura>`, `<llamada_funcion>`, `<expresion>`,
`<exp_aritmetica>`, `<termino>`, `<factor>`.

#### Símbolo inicial (S):

`S = <programa>`

#### Producciones (P):
---
## 1. Estructura general del programa

### Producción gramatical
```text
<programa> -> <lista_funciones>
```
Un programa está compuesto por una lista de una o más funciones. Esta regla establece el punto de partida de la gramática.
### Ejemplo
```C
int main() {
    return 0;
}
```
---
## 2. Lista de funciones

### Producción gramatical
```text
<lista_funciones> -> <funcion><lista_funciones>
<lista_funciones> -> <funcion>
```
Estas producciones permiten construir una lista de funciones.

- **Primera producción:** agrega una función y continúa la lista.
- **Segunda producción:** agrega la última función y termina la lista.

La lista nunca puede estar vacía, ya que debe contener al menos una función.
### Ejemplo
```C
int doble(int x) {
    return x * 2;
}

int main() {
    return doble(3);
}
```
---
## 3. Definición de una función

### Producción gramatical
```text
<funcion> -> <tipo> <id> "(" <parametros> ")" <bloque>
```
Define la estructura de una función mediante su tipo de retorno, identificador, parámetros y cuerpo.

| Elemento | Descripción |
|----------|--------|
| `<tipo>` | Tipo de dato que devuelve la función. |
| `<id>` | Nombre de la función. |
| `"(" ")"` | 	Delimitan los parámetros. |
| `<parametros>` | 	Parámetros que recibe la función. |
| `<bloque>` | Cuerpo de la función. |

### Ejemplo
```C
int suma(int a, int b) {
    return a + b;
}

float mitad(float x) {
    return x / 2.0;
}
```
---
## 4. Parámetros de una función

### Producción gramatical
```text
<parametros> -> <lista_parametros>
<parametros> -> λ
```
Una función puede recibir una lista de parámetros o no recibir ninguno.

- **Con parámetros:** se utiliza `<lista_parametros>`.
- **Sin parámetros:** λ representa una producción vacía.

### Ejemplo
```C
int f(int a) {
    return a;
}

int f() {
    return 0;
}
```
---
## 5. Lista de parámetros

### Producción gramatical
```text
<lista_parametros> -> <parametro> "," <lista_parametros>
<lista_parametros> -> <parametro>
```
Permite definir uno o varios parámetros separados por comas.
- **Primera producción:** define un parámetro seguido de una coma y otra lista de parámetros.
- **Segunda producción:** define el último parámetro de la lista.

### Ejemplo
```C
int calcular(int a, float b, int c) {
    return a;
}

int g(float y) {
     return 1;
}
```
---
## 6. Parámetro individual

### Producción gramatical
```text
<parametro> -> <tipo><id>
```
Cada parámetro de una función está compuesto por un tipo de dato y un identificador que representa su nombre.

### Ejemplo
```C
int x
float altura
```
---
## 7. Tipo de dato

### Producción gramatical
```text
<tipo> -> "int"
<tipo> -> "float"
```
Esta regla establece los tipos de datos permitidos por el lenguaje.
- **int:** representa números enteros.
- **float:** representa números de punto flotante.
### Ejemplo
```C
int edad;
float precio;
```
---
## 8. Bloque de instrucciones

### Producción gramatical
```text
<bloque> -> "{" <lista_sentencias> "}"
```
Un bloque agrupa una lista de sentencias delimitada por llaves. Puede contener cero o más instrucciones.

### Ejemplo
```C
{
}

{
    int x;
    x = 4;
}
```
---
## 9. Lista de sentencias

### Producción gramatical
```text
<lista_sentencias> -> <sentencia><lista_sentencias>
<lista_sentencias> -> λ
```
Permite construir una secuencia de sentencias dentro de un bloque o representar una lista vacía.

- **Primera producción:** agrega una sentencia y continúa con el resto.
- **Segunda producción:** termina la lista sin agregar más instruccio

### Ejemplo
```C
{
    int x;
    x = 2;
    print(x);
}

{
}
```
---
## 10. Sentencia

### Producción gramatical
```text
<sentencia> -> <declaracion> ";"
<sentencia> -> <asignacion> ";"
<sentencia> -> <condicional>
<sentencia> -> <ciclo_while>
<sentencia> -> <ciclo_for>
<sentencia> -> <retorno> ";"
<sentencia> -> <impresion> ";"
<sentencia> -> <lectura> ";"
<sentencia> -> <llamada_funcion> ";"
```
Define las nueve clases de sentencias admitidas por el lenguaje: declaraciones, asignaciones, condicionales, ciclos while, ciclos for, retornos, impresiones, lecturas y llamadas a funciones.

Las instrucciones simples terminan con punto y coma, mientras que las estructuras de control con bloques no lo necesitan después de la llave de cierre.

### Ejemplo
```C
int n;
n = 3;
if (n > 0) { print(n); }
while (n > 0) { n = n - 1; }
for (n = 0; n < 3; n = n + 1) { print(n); }
return n;
print("hola", n);
read(n);
saludar();
```
---
## 11. Declaración de variables

### Producción gramatical
```text
<declaracion> -> <tipo> <id>
<declaracion> -> <tipo> <id> "=" <expresion>
```
Estas producciones permiten declarar variables con o sin un valor inicial.
- **Primera producción:** declara una variable indicando su tipo y su identificador.
- **Segunda producción:** declara una variable y le asigna un valor inicial mediante una expresión.

El punto y coma no forma parte de estas producciones, ya que se agrega mediante la regla `<sentencia>`.

### Ejemplo
```C
int contador;
float promedio = 7.5;
int negativo = -5;
```
---
## 12. Asignación

### Producción gramatical
```text
<asignacion> -> <id> "=" <expresion>
```
Esta producción permite asignar un valor a una variable mediante una expresión. El identificador representa la variable cuyo valor se desea establecer o modificar.

La expresión puede contener números, identificadores, operaciones aritméticas, paréntesis o llamadas a funciones.

### Ejemplo
```C
x = 10;
x = -a + doble(2);
resultado = suma(3, 4);
```
---
## 13. Condicional

### Producción gramatical
```text
<condicional> -> "if" "(" <expresion> ")" <bloque>
<condicional> -> "if" "(" <expresion> ")" <bloque> "else" <bloque>
```
Estas producciones permiten ejecutar instrucciones dependiendo del resultado de una expresión condicional.

- **Primera producción:** permite ejecutar un bloque cuando la condición se cumple.
- **Segunda producción:** permite ejecutar un bloque alternativo mediante else cuando la condición no se cumple.

Ambas producciones requieren que los bloques estén delimitados por llaves.

### Ejemplo
```C
if (x > 0) {
    print(x);
}

if (x == 0) {
    print("cero");
} else {
    print("otro");
}
```
---
## 14. Ciclo while

### Producción gramatical
```text
<ciclo_while> -> "while" "(" <expresion> ")" <bloque>
```
Esta producción permite repetir un bloque de instrucciones mientras una expresión condicional se evalúe como verdadera.

La estructura contiene la palabra reservada while, una condición entre paréntesis y un bloque delimitado por llaves.

### Ejemplo
```C
int main() {
    int x = 3;

    while (x > 0) {
        print(x);
        x = x - 1;
    }

    return 0;
}
```
---
## 15. Ciclo for

### Producción gramatical
```text
<ciclo_for> -> "for" "(" <asignacion> ";" <expresion> ";" <asignacion> ")" <bloque>
```
Esta producción define una versión simplificada del ciclo for de C. Está formada por tres componentes dentro de los paréntesis:

- **Asignación inicial:** establece el valor inicial de una variable.
- **Expresión condicional:** determina si el ciclo continúa.
- **Asignación de actualización:** modifica una variable al finalizar cada iteración.

El cuerpo del ciclo está delimitado por llaves.

### Ejemplo
```C
int main() {
    int i;

    for (i = 0; i < 10; i = i + 1) {
        print(i);
    }

    return 0;
}
```
> **Nota:** No admite for(int i = 0; ...), i++ ni componentes omitidos.
---
## 16. Retorno de una función

### Producción gramatical
```text
<retorno> -> "return" <expresion>
```
Esta producción permite devolver el resultado de una expresión desde una función. La expresión puede ser un valor literal, un identificador, una operación aritmética o una llamada a una función.

El punto y coma se incorpora mediante la producción `<sentencia>`.

### Ejemplo
```C
return 0;
return x;
return x + 1;
return -x;
```
> **Nota:** No se admite return; sin una expresión, ya que esta gramática no contempla funciones de tipo void.
---
## 17. Impresión

### Producción gramatical
```text
<impresion> ->"print" "(" <lista_impresion> ")"
```
Esta producción permite imprimir uno o varios elementos mediante la palabra reservada print.

Los elementos que se imprimen se especifican mediante `<lista_impresion>` y pueden ser cadenas de caracteres o expresiones.

### Ejemplo
```C
print("hola");
print(x);
print("resultado:", x + 1);
```
> **Nota:** No se admite print() vacío, porque la producción requiere una lista de impresión con al menos un elemento.
---
## 18. Lista de impresión

### Producción gramatical
```text
<lista_impresion> -> <elemento_impresion> "," <lista_impresion>
<lista_impresion> -> <elemento_impresion>
```
Estas producciones permiten construir una lista de elementos separados por comas para la instrucción print.

- **Primera producción:** agrega un elemento seguido de una coma y otra lista de elementos.
- **Segunda producción:** define el último elemento de la lista.

La lista debe contener al menos un elemento.

### Ejemplo
```C
print("a", x, x * 2);
print("texto");
```
---
## 19. Elemento de impresión

### Producción gramatical
```text
<elemento_impresion> -> cadena
<elemento_impresion> -> <expresion>
```
Esta producción establece los dos tipos de elementos que pueden aparecer en una lista de impresión:

- Una cadena de caracteres.
- Una expresión válida del lenguaje.

### Ejemplo
```C
print("edad:");
print(edad + 1);
print("resultado:", suma(2, 3));
```
---
## 20. Lectura de datos

### Producción gramatical
```text
<lectura> -> "read" "(" <id> ")"
```
Esta producción permite leer un dato mediante la palabra reservada read. Dentro de los paréntesis debe aparecer un identificador que indique la variable asociada a la lectura.

El punto y coma se incorpora mediante `<sentencia>`.

### Ejemplo
```C
read(edad);
read(valor);
```
> **Nota:** No se admiten expresiones ni valores literales como argumentos de read. Por ejemplo, read(5) no es válido porque la regla exige <id>.
---
## 21. Llamada a función

### Producción gramatical
```text
<llamada_funcion> -> <id> "(" <argumentos> ")"
```
Esta producción permite invocar una función mediante su identificador y una lista opcional de argumentos encerrada entre paréntesis.

La llamada puede realizarse con argumentos o sin ellos. Cuando aparece como una sentencia independiente, termina con punto y coma.

### Ejemplo
```C
saludar();
suma(2, 3);
doble(suma(1, 2));
```
---
## 22. Argumentos de una función

### Producción gramatical
```text
<argumentos> -> <lista_argumentos>
<argumentos> -> λ
```
Estas producciones permiten que una llamada a función incluya una lista de argumentos o no incluya ninguno.

- **Primera producción:** utiliza `<lista_argumentos>` cuando existen argumentos.
- **Segunda producción:** representa la ausencia de argumentos mediante λ.

### Ejemplo
```C
f();
f(2, x);
```
---
## 23. Lista de argumentos

### Producción gramatical
```text
<lista_argumentos> -> <expresion> "," <lista_argumentos>
<lista_argumentos> -> <expresion>
```
Estas producciones permiten construir una lista de uno o más argumentos separados por comas.

- **Primera producción:** define una expresión seguida de una coma y otra lista de argumentos.
- **Segunda producción:** define el último argumento.

Cada argumento puede ser cualquier expresión válida del lenguaje.

💻 Ejemplos

### Ejemplo
```C
suma(2, 3);
f(x, 2 + 1, -a);
```
---
## 24. Expresión

### Producción gramatical
```text
<expresion> -> <exp_aritmetica>
<expresion> -> <exp_aritmetica> <op_relacional> <exp_aritmetica>
```
Estas producciones permiten representar dos clases de expresiones:

- **Primera producción:** una expresión aritmética sin comparación.
- **Segunda producción:** una comparación entre dos expresiones aritméticas mediante un operador relacional.

### Ejemplo
```C
a + 2
a * 2 >= b - 1
-x < 0
```
> **Nota:** La gramática no incluye los operadores lógicos && y ||, ni permite comparaciones encadenadas mediante una única aplicación de esta producción.
---
## 25. Operador relacional

### Producción gramatical
```text
<op_relacional> -> "<"
<op_relacional> -> ">"
<op_relacional> -> "<="
<op_relacional> -> ">="
<op_relacional> -> "=="
<op_relacional> -> "!="
```
Esta regla define los seis operadores relacionales admitidos por el lenguaje.

| Operador | Significado |
|----------|--------|
| `<` | Menor que. |
| `>` | Mayor que. |
| `<=` | 	Menor o igual que. |
| `>=` | 	Mayor o igual que. |
| `==` | 	Igual que. |
| `!=` | 		Distinto de. |

### Ejemplo
```C
a < b
a > b
a <= b
a >= b
a == b
a != b
```
---
## 26. Expresión aritmética

### Producción gramatical
```text
<exp_aritmetica> -> <termino>
<exp_aritmetica> -> <exp_aritmetica> "+" <termino>
<exp_aritmetica> -> <exp_aritmetica> "-" <termino>
```
Estas producciones permiten construir expresiones aritméticas utilizando términos, sumas y restas.

- **Primera producción:** una expresión aritmética puede estar formada por un solo término.
- **Segunda producción:** permite agregar un término mediante el operador +.
- **Tercera producción:** permite agregar un término mediante el operador -.

### Ejemplo
```C
a
a + b
a - b + 3
```
---
## 27. Término aritmético

### Producción gramatical
```text
<termino> -> <factor>
<termino> -> <termino> "*" <factor>
<termino> -> <termino> "/" <factor>
<termino> -> <termino> "%" <factor>
```
Estas producciones permiten construir términos aritméticos mediante factores y los operadores de multiplicación, división y módulo.

- **Primera producción:** un término puede estar formado por un factor.
- **Segunda producción:** permite multiplicar un término por un factor.
- **Tercera producción:** permite dividir un término entre un factor.
- **Cuarta producción:** permite calcular el módulo entre un término y un factor.

### Ejemplo
```C
x
a * b
a / 2
n % 2
```
> **Nota:** El operador % está permitido por la sintaxis. Sin embargo, las restricciones relacionadas con los tipos de sus operandos deben comprobarse durante el análisis semántico.
---
## 28. Factor

### Producción gramatical
```text
<factor> -> <id>
<factor> -> <entero>
<factor> -> <real>
<factor> -> <llamada_funcion>
<factor> -> "(" <expresion> ")"
<factor> -> "-" <factor>
```
Estas producciones definen los elementos básicos que pueden aparecer dentro de una expresión aritmética.

Un factor puede ser:

- Un identificador.
- Un número entero.
- Un número real.
- Una llamada a función.
- Una expresión entre paréntesis.
- Un factor precedido por el signo menos unario.

### Ejemplo
```C
x
123
3.14
suma(2, 3)
(a + b)
-x
-(a + b)
```
> **Nota:** El signo negativo no forma parte de los tokens `<entero>` o `<real>`. Se representa mediante la producción `<factor> → "-" <factor>`.
---
## 29. Identificador

### Producción gramatical
```text
<id> -> <inicio_id><continuacion_id>
```
Un identificador representa el nombre de una variable, función o parámetro.

Esta producción establece que un identificador está compuesto por un carácter inicial válido seguido de cero o más caracteres adicionales permitidos.

### Ejemplo
```C
x
variable2
_dato
total_2026
```
---
## 30. Inicio de un identificador

### Producción gramatical
```text
<inicio_id> -> <letra>
<inicio_id> -> "_"
```
Esta regla determina qué caracteres pueden aparecer al principio de un identificador.

El primer carácter debe ser una letra ASCII mayúscula o minúscula, o un guion bajo.

### Ejemplo
```C
a
Z
_
```
---
## 31. Continuación de un identificador

### Producción gramatical
```text
<continuacion_id> -> <caracter_id> <continuacion_id>
<continuacion_id> -> λ
```
Estas producciones permiten que un identificador contenga cero o más caracteres después de su posición inicial.

- **Primera producción:** agrega un carácter permitido y continúa la secuencia.
- **Segunda producción:* termina la secuencia mediante una producción vacía.

### Ejemplo
```C
a
abc123
_x_2
```
---
## 32. Carácter de un identificador

### Producción gramatical
```text
<caracter_id> -> <letra>
<caracter_id> -> <digito>
<caracter_id> -> "_"
```
Esta regla establece los caracteres que pueden aparecer después del primer carácter de un identificador.

Se aceptan letras ASCII, dígitos decimales y guiones bajos.

### Ejemplo
```C
x2
a_b
valor9
```
---
## 33. Número entero

### Producción gramatical
```text
<entero> -> <digito><resto_digito>
```
Esta producción permite representar un número entero formado por uno o más dígitos decimales.

El primer dígito se reconoce mediante `<digito>`, mientras que los dígitos adicionales se definen mediante `<resto_digito>`.

### Ejemplo
```C
0
7
123
0007
```
---
## 34. Resto digito

### Producción gramatical
```text
<resto_digito> -> <digito> <resto_digito>
<resto_digito> -> λ
```
Estas producciones permiten agregar dígitos a un número entero o terminar la secuencia.

- **Primera producción:** incorpora otro dígito y continúa.
- **Segunda producción:** finaliza la secuencia mediante una producción vacía.

### Ejemplo
```C
5
50
5021
```
---
## 35. Número real

### Producción gramatical
```text
<real> -> <entero> "." <entero>
```
Esta producción reconoce números reales que contienen una parte entera, un punto decimal y una parte fraccionaria. Ambas partes deben contener al menos un dígito.

### Ejemplo
```C
0.5
3.14
12.0
```
> **Nota:** No admite .5 ni 1. ni notación científica.
---
## 36. Cadena de caracteres

### Producción gramatical
```text
<cadena> -> "\"" <contenido_cadena> "\""
```
Esta producción establece que una cadena de caracteres comienza y termina con comillas dobles.

El contenido interior se define mediante `<contenido_cadena>`, que puede estar vacío o contener una secuencia de caracteres permitidos.

### Ejemplo
```C
"hola"
""
"Valor de x:"
```
---
## 37. Contenido de una cadena

### Producción gramatical
```text
<contenido_cadena> -> <caracter_cadena><contenido_cadena>
<contenido_cadena> -> λ
```
Estas producciones permiten construir el contenido de una cadena mediante cero o más caracteres.

- **Primera producción:** agrega un carácter y continúa con el resto del contenido.
- **Segunda producción:** permite que el contenido termine o que la cadena esté vacía.

### Ejemplo
```C
""
"abc"
"a b c"
```
---
## 38. Carácter de una cadena

### Producción gramatical
```text
<caracter_cadena> -> <caracter_ordinario>
<caracter_cadena> -> <escape>
```
Esta regla establece que cada carácter de una cadena puede ser un carácter ordinario permitido o una secuencia de escape.

Los caracteres ordinarios se definen mediante `<caracter_ordinario>`, mientras que las secuencias especiales se definen mediante `<escape>`.

### Ejemplo
```C
"A"
"Hola\n"
"Dijo: \"sí\""
```
---
## 39. Escape

### Producción gramatical
```text
<escape> -> "\" "n"
<escape> -> "\" "t"
<escape> -> "\" "\"
<escape> -> "\" '"'
```
Estas producciones permiten representar caracteres especiales dentro de las cadenas mediante una barra invertida seguida de otro carácter.

| Secuencia | Significado |
|----------|--------|
| `\n` | Salto de línea. |
| `\t` | Tabulación. |
| `\\` | Barra invertida. |
| `\"` | Comilla doble. |

### Ejemplo
```C
"linea1\nlinea2"
"a\tb"
"c:\\tmp"
"\"texto\""
```
---
## 40. Caracter ordinario

### Producción gramatical
```text
<caracter_ordinario> -> cualquier carácter permitido salvo comillas dobles, barra invertida y salto de línea
```
Esta regla define la clase de caracteres ordinarios que pueden aparecer dentro de una cadena.

Se admiten los caracteres permitidos que no sean comillas dobles sin escapar, barras invertidas ni saltos de línea literales. Estos casos especiales deben tratarse mediante las reglas correspondientes.

La producción representa una clase léxica, no una enumeración individual de todos los caracteres posibles.

### Ejemplo
```C
"Hola mundo"
"precio: 25"
"Texto ordinario"
```
---
## 41. Letra

### Producción gramatical
```text
<letra> -> "a"
            .
            .
            .
<letra> -> "z"
<letra> -> "A"
            .
            .
            .
<letra> -> "Z"
```
Esta producción representa cualquiera de las 52 letras del alfabeto inglés ASCII, incluyendo las letras minúsculas y mayúsculas.

Se utiliza para construir identificadores y definir los caracteres que pueden aparecer en ellos.

### Ejemplo
```C
a
m
Z
```
---
## 42. Digito

### Producción gramatical
```text
<digito> -> "0"
<digito> -> "1"
<digito> -> "2"
             .
             .
<digito> -> "9"
```
Esta producción representa cualquiera de los diez dígitos decimales, desde el cero hasta el nueve.

Se utiliza para construir números enteros, números reales e identificadores que contienen dígitos después de su primer carácter.

### Ejemplo
```C
0
4
9
```
---
---
> **IMPORTANTE:** Aunque la producción `<id>` describe cadenas de caracteres que pueden tener la misma forma que algunas palabras reservadas, estas palabras no pueden utilizarse como nombres de variables, parámetros o funciones.
> Además, los espacios en blanco que separan los tokens se gestionan fuera de estas producciones gramaticales, normalmente mediante el analizador léxico.
