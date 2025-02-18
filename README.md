# 1.0 Apuntes PL/SQL
Apuntes que tengo del Grado Superior, y que he añadido recientemente.

## 1.1.0 Tipos de datos en PL/SQL.
- CHAR (n) Cadena de longitud fija.
- VARCHAR2(n) Cadena de longitud variable.
- NUMBER(p, s) Números con precisión.

>[!IMPORTANT]
> `p` (Precisión). Es el número total de dígitos que puede tener el número, tanto a la izquierda como a la derecha del punto decimal.
>
> `s` (Escala). Es el número de dígitos que se reservan para la parte decimal (a la derecha del punto).
>
>`NUMBER(5,2)` permite almacenar números con hasta 5 dígitos en total, de los cuales 2 son decimales. Esto significa que puedes tener números como `123.45` o `-99.99`.
>
>- Si intentas almacenar `1234.56`, excederías la precisión total de 5 dígitos.
>- Si intentas almacenar `12.345`, excederías la escala permitida (más de 2 dígitos decimales).
Esta notación ayuda a controlar la cantidad y la precisión de los datos numéricos que se almacenan en la base de datos.
>
>Cuando se intenta almacenar un valor que excede la precisión o la escala definida, Oracle no realiza un ajuste o truncamiento automático, sino que lanza un error en tiempo de ejecución. Algunos ejemplos de errores que podrías ver son:
>
>- ORA-06502: PL/SQL: numeric or value error: Indica que el valor numérico no se ajusta al formato esperado.
>- ORA-12899: value too large for column (si es en una columna de tabla): Indica que el valor es mayor que el tamaño permitido.


- DATE
- BOOLEAN ( Que pueden ser `TRUE`, `FALSE` y `NULL`.
- CLOB/BLOB, para datos grandes como textos muy extensos o imágenes.

## 1.2.0 Estructuras de Control:

### 1.2.1 IF:

### 1.2.2 Bucle LOOP:

### 1.2.3 Bucle WHILE:

## 1.3 Cursores:

## 1.4 Excepciones o manejos de errores:

# 2.0 Preguntas Entrevista:

- **Conceptos básicos de PL/SQL**
  - ¿Qué es PL/SQL y en qué se diferencia de SQL?
  - Explica la estructura básica de un bloque PL/SQL.
  - ¿Qué son las excepciones en PL/SQL? ¿Cuáles son las más comunes?
  
- **Procedimientos, Funciones y Paquetes**
  - ¿Cuál es la diferencia entre un procedimiento y una función en PL/SQL?
  - ¿Qué ventajas tiene usar paquetes en PL/SQL?
  - ¿Cómo se declara y ejecuta un procedimiento almacenado?
- **Cursores y Manejo de Datos**
  - ¿Qué es un cursor en PL/SQL? ¿Cuál es la diferencia entre un cursor implícito y un cursor explícito?
  - ¿Cómo se usa un cursor FOR LOOP?
  - ¿Cuáles son las diferencias entre %ROWTYPE y %TYPE?

- **Triggers y Excepciones**
  - ¿Qué es un trigger y para qué se usa?
  - ¿Cuáles son los tipos de triggers en PL/SQL?
  - ¿Cómo manejas excepciones en PL/SQL?

- **Optimización y Buenas Prácticas**
  - ¿Cómo mejorar el rendimiento de un bloque PL/SQL?
  - ¿Qué es la colección BULK y cuándo se usa?
  - ¿Cómo optimizar el uso de cursores para mejorar la performance?

- **DML y Transacciones**
  - ¿Qué es un SAVEPOINT y cómo se usa en PL/SQL?
  - ¿Cómo funciona el COMMIT y el ROLLBACK?
  - ¿Qué diferencia hay entre DELETE y TRUNCATE?

- **Consultas Prácticas**
  - "Escribe un procedimiento almacenado que reciba un ID de empleado y devuelva su salario."

## PREGUNTA 1: ¿Qué es PL/SQL y en qué se diferencia de SQL?

No es que se diferencie, es un lenguaje procedimental. Un lenguaje adicional a SQL. SQL tiene varios sublenguajes, entre ellos:
- DML
- DDL
- DCL
- TCL

y entre ellos **NO ESTÁ el PL/SQL.**

- PL/SQL

PL/SQL es entonces, un lenguaje de programación desarrollado por Oracle, que amplica las posibilidades y funcionalidades de SQL, al poder manipular memoria y usar estrucutras de control, como los For, While, If.

