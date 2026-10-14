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


#### Símbolo inicial:

`S = <programa>`

P = {
     '<programa>' -> <lista_funciones>
     <lista_funciones> -> <funcion><lista_funciones>
     <lista_funciones> -> <funcion>
     <funcion> -> <tipo> <id> "(" <parametros> ")" <bloque>
     <parametros> -> <lista_parametros>
     <parametros> -> λ
     <lista_parametros> -> <parametro> "," <lista_parametros>
     <lista_parametros> -> <parametro>
     <parametro> -> <tipo><id>
     <tipo> -> "int"
     <tipo> -> "float"
     <bloque> -> "{" <lista_sentencias> "}"
     <lista_sentencias> -> <sentencia><lista_sentencias>
     <lista_sentencias> -> λ
     <sentencia> -> <declaracion> ";"
     <sentencia> -> <asignacion> ";"
     <sentencia> -> <condicional>
     <sentencia> -> <ciclo_while>
     <sentencia> -> <ciclo_for>
     <sentencia> -> <retorno> ";"
     <sentencia> -> <impresion> ";"
     <sentencia> -> <lectura> ";"
     <sentencia> -> <llamada_funcion> ";"
     <declaracion> -> <tipo> <id>
     <declaracion> -> <tipo> <id>"=" <expresion>
     <asignacion> -> <id> "=" <expresion>
     <condicional> -> "if" "(" <expresion> ")" <bloque>
     <condicional> -> "if" "(" <expresion> ")" <bloque> "else" <bloque>
     <ciclo_while> -> "while" "(" <expresion> ")" <bloque>
     <ciclo_for> -> "for" "(" <asignacion> ";" <expresion> ";" <asignacion> ")" <bloque>
     <retorno> -> "return" <expresion>
     <impresion> ->"print" "(" <lista_impresion> ")"
     <lista_impresion> -> <elemento_impresion> "," <lista_impresion>
     <lista_impresion> -> <elemento_impresion>
     <elemento_impresion> -> cadena
     <elemento_impresion> -> <expresion>
     <lectura> -> "read" "(" <id> ")"
     <llamada_funcion> -> <id> "(" <argumentos> ")"
     <argumentos> -> <lista_argumentos>
     <argumentos> -> λ
     <lista_argumentos> -> <expresion> "," <lista_argumentos>
     <lista_argumentos> -> <expresion>
     <expresion> -> <exp_aritmetica>
     <expresion> -> <exp_aritmetica><op_relacional><exp_aritmetica>
     <op_relacional> -> "<"
     <op_relacional> -> ">"
     <op_relacional> -> "<="
     <op_relacional> -> ">="
     <op_relacional> -> "=="
     <op_relacional> -> "!="
     <exp_aritmetica> -> <termino>
     <exp_aritmetica> -> <exp_aritmetica> "+" <termino>
     <exp_aritmetica> -> <exp_aritmetica> "-" <termino>
     <termino> -> <factor>
     <termino> -> <termino> "*" <factor>
     <termino> -> <termino> "/" <factor>
     <termino> -> <termino> "%" <factor>
     <factor> -> id
     <factor> -> entero
     <factor> -> real
     <factor> -> <llamada_funcion>
     <factor> -> "(" <expresion> ")"
     <id> -> <inicio_id><continuacion_id>
     <inicio_id> -> <letra>
     <inicio_id> -> "_"
     <continuacion_id> -> <caracter_id><continuacion_id>
     <continuacion_id> -> λ
     <caracter_id> -> <letra>
     <caracter_id> -> <digito>
     <caracter_id> -> "_"
     <entero> -> <digito><resto_digito>
     <resto_digito> -> <digito><resto_digito>
     <resto_digito> -> λ
     <real> -> <entero> "." <entero>
     <cadena> -> '"' <contenido_cadena> '"'
     <contenido_cadena> -> <caracter_cadena><contenido_cadena>
     <contenido_cadena> -> λ
     <caracter_cadena> -> cualquier carácter permitido dentro de una cadena, excepto las comillas dobles sin escapar
     <letra> -> [a-zA-Z]
     <digito> -> [0-9]
    }