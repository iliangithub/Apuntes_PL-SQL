# 1.0 Apuntes PL/SQL
Apuntes que tengo del Grado Superior, y que he añadido recientemente.
## 1.1.0 Bloques. ¿Qué son?

Un bloque, es donde se escribe el código PL/SQL.

**NO PUEDES** hacer un `SELECT * FROM tabla` y luego poner un bloque (Poner el `BEGIN` y el `END`), el bloque sirve solo si quiero manejar el "output" del SELECT usando PL/SQL, es decir, que el bloque sólo sirve para cuando se vaya a usar el PL/SQL.

**No puedo simplemente poner una sentencia SQL sin más.**
> [!IMPORTANT]
>Todas las instrucciones que pertenecen al bloque deben estar dentro de la estructura definida: la sección declarativa (opcional), la sección ejecutable (entre `BEGIN` y `END`) y la sección de excepciones (opcional). Esto es porque el compilador PL/SQL espera encontrar esa estructura completa para interpretar y compilar el código.
>
>Si colocas una sentencia SQL (como `SELECT * FROM tabla`) fuera de un bloque PL/SQL, Oracle no sabe si esa instrucción forma parte de un bloque procedural o si es una sentencia SQL independiente. Es decir, **no puedes mezclar ambas en un solo contexto sin indicarle al sistema dónde termina un bloque y dónde empieza otro.**
>

>[!WARNING]
>Esto es incorrecto:
>```
>SELECT * FROM tabla
>
>BEGIN
>   DBMS_OUTPUT.PUT_LINE('Hola Mundo');
>END;
>```
>
>No es válido porque:
>- El SELECT * FROM tabla se está ejecutando como una sentencia SQL independiente, pero luego el compilador PL/SQL encuentra un bloque y se confunde por la mezcla.
>- Si lo que buscas es ejecutar ambos, deberías separarlos en diferentes ejecuciones o colocar el SELECT dentro de un bloque PL/SQL (usando, por ejemplo, un cursor o SELECT ... INTO ...).
>**En resumen, cada tipo de sentencia debe estar en el contexto correcto.**
>

## 1.1.1 El bloque en sí.

Es básicamente esto:

```
BEGIN

END;
```

A veces puedes declarar también variables.

```
DECLARE

BEGIN

END;
```

O poder controlar o manejar errores.

```
DECLARE

BEGIN

EXCEPTION

END;
```

Vamos a hacer entonces un bloque con un **Hello World**:

```
BEGIN

dbms_output.put_line('Hola mundo');

END;
```

>[!IMPORTANT]
> En PL/SQL (y en SQL en general), las cadenas de texto se definen utilizando comillas simples. Esto es parte de la sintaxis del lenguaje.
>
>- Comillas simples: Se usan para delimitar un literal de cadena. Por ejemplo, 'Hola mundo' indica que se trata de una secuencia de caracteres que se interpretará literalmente.
>  
>- Comillas dobles: Se utilizan en otros contextos, por ejemplo, para delimitar identificadores (como nombres de columnas o tablas) que son sensibles a mayúsculas/minúsculas o que contienen espacios.
>

### 1.1.0.1 Ejecución de programas:

![image](https://github.com/user-attachments/assets/a8ce28db-74cf-4692-8d39-0aa6d96519e7)

Si le doy arriba a "*Sentencia de Ejecución*". Me muestra eso, pero no el output que quiero, ¿Porqué?.

>[!WARNING]
>Si no habilitas DBMS_OUTPUT, el mensaje se envía a un buffer interno y no se muestra en la pantalla, por eso podrías ver solo el mensaje "Procedimiento PL/SQL terminado correctamente" sin el contenido que esperas.
>
>Debería de quedar algo así:
>```
>SET SERVEROUTPUT ON;
>BEGIN
>  DBMS_OUTPUT.PUT_LINE('Hola Mundo');
>END;
>/
>```
>
>Y para apagarlo pues con el OFF... 
>

>[!TIP]
>
> ![image](https://github.com/user-attachments/assets/72963d8f-48bc-4d0b-b6e6-fd74082045ca)
>
>Podemos hacerlo también así:
>
> ![image](https://github.com/user-attachments/assets/306d81d1-058b-4992-ab54-c019c60e9aae)
>
> Y así queda mucho más aislado.
>
> ![image](https://github.com/user-attachments/assets/61a883fb-6039-41ac-9bd0-954f9468730e)

### 1.1.0.2 Ejecución de programas SUPER IMPORTANTE POR FAVOR LEER:

>[!IMPORTANT]
>El Shortcut para ejecutar los scripts es **`F5`**.
>
>Hay en realidad, varias maneras, la que he estado haciendo hasta el momento y ejecutar todo el script:
>
> ![image](https://github.com/user-attachments/assets/24b6742d-7f97-4550-aab4-97067372aefe)
>
>Entonces, la primera opción ejecutaría solo 1 bloque o mejor dicho:
>Si no seleccionas todo el script antes de ejecutar (usando F5 o el botón de "Run Script"), SQL Developer ejecuta solo el bloque en el que se encuentre el cursor. Por ejemplo, si tu cursor está en el segundo bloque, se ejecutará únicamente ese bloque y verás solo el resultado de ese bloque.
>

## 1.1.2 Cómo tener varios bloques a la vez:

Tienen que estar separados por `/`

```
BEGIN
 DBMS_OUTPUT.PUT_LINE('Hola Mundo');
END;

/

BEGIN
 DBMS_OUTPUT.PUT_LINE('Hola Mundo2');
END;
```

**Y como hemos dicho anteriormente, ahora para mostrar los dos Holamundos, tenemos que darle a F5**.

## 1.1.3 Variables.

Se declaran arriba del todo:

```
DECLARE
   v_num NUMBER(2) := 10;
   v_cadena VARCHAR(10) := 'Fernando';
   v_fecha DATE := SYSDATE;
BEGIN
   DBMS_OUTPUT.PUT_LINE('El valor de la primera variable es ' || v_num  );
   DBMS_OUTPUT.PUT_LINE('El valor de la segunda variable es ' || v_cadena );
   DBMS_OUTPUT.PUT_LINE('El valor de la tercera variable es ' || v_fecha );
END;
```
*Y si, literalmente hay que poner `:=` como si fuera un xxxxxx.*

Entonces...

Acabamos de ver que para declarar variables se hace como se muestra arriba y para concatenar, se hace usando el **`||`**.


Que por cierto, también lo podríamos haber hecho así:

```
DECLARE
   v_num NUMBER(2) := 10;
   v_cadena VARCHAR(10) := 'Fernando';
   v_fecha DATE := SYSDATE;
BEGIN
   DBMS_OUTPUT.PUT_LINE('El valor de la primera variable es ' || v_num || ' El valor de la segunda variable es ' || v_cadena );
END;
```

Y también el valor de las variables, pues puede variar perfectamente sin problemas...

```
DECLARE
   v_num NUMBER(2) := 10;

BEGIN
   v_num NUMBER(2) := 15;
   DBMS_OUTPUT.PUT_LINE('El valor de la primera variable es ' || v_num );
END;
```

## 1.1.4 Variables 2, Pedir Datos al Usuario IMPORTANTE.

Para entender esto, es básicamente como un IMPUT que literalmente pide que el Usuario rellene para pues mostrarlo o lo que sea...

```
DECLARE
   v_opcion1 NUMBER(2) := &numero_que_va_a_poner_el_usuario1;
   v_opcion2 NUMBER(2) := &numero_que_va_a_poner_el_usuario2;
   v_suma_de_numeros NUMBER (3);

BEGIN
   v_suma_de_numeros := v_opcion1 + v_opcion2;
   DBMS_OUTPUT.PUT_LINE(v_opcion1 || ' + ' || v_opcion2 || ' es igual a: ' || v_suma_de_numeros);
END;
```

Y como podemos ver, nos aparece la ventanita:

![image](https://github.com/user-attachments/assets/9b3196c3-6bf1-42e1-9f27-5c1e2ea3a340)

Si vamos a poner texto en esa ventanita, tenemos que hacerlo con las '' comillas simples.

## 1.1.5 Tipos de datos en PL/SQL.
- `CHAR (n)` Cadena de longitud fija. *Tienes que saber de antemano la longitud*
- `VARCHAR2(n)` Cadena de longitud variable.
- `NUMBER` Sin especificar nada, permite almacenar números con hasta 38 dígitos y la escala es variable.
- `NUMBER(p, s)` Números con precisión.

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
>**Cuando se intenta almacenar un valor que excede la precisión o la escala definida**, Oracle no realiza un ajuste o truncamiento automático, sino que **lanza un error en tiempo de ejecución**. Algunos ejemplos de errores que podrías ver son:
>
>- ORA-06502: PL/SQL: numeric or value error: Indica que el valor numérico no se ajusta al formato esperado.
>- ORA-12899: value too large for column (si es en una columna de tabla): Indica que el valor es mayor que el tamaño permitido.


- `DATE` Para almacenar fechas y horas (hasta segundos).
- `TIMESTAMP` Fecha y hora con mayor precisión, incluyendo fracciones de segundo (milisegundos o incluso microsegundos). Ideal para aplicaciones donde se requiere una precisión más fina en el registro de eventos, como en logs, transacciones o cuando se necesita medir intervalos muy cortos.
- `BOOLEAN` ( Que pueden ser `TRUE`, `FALSE` y `NULL`. )
- `CLOB/BLOB`, para datos grandes como textos muy extensos o imágenes.
- `Tipos compuestos y colecciones` que trataremos más adelante.

## 1.2.0 Operadores Aritméticos:

Antes hemos hecho la suma, vamos a probarlas todas de nuevo:

### 1.2.0.1 Suma.

```
BEGIN
   DBMS_OUTPUT.PUT_LINE('Suma (2 + 3): ' || (2 + 3));
END;
/
```

### 1.2.0.2 Resta.

```
BEGIN
   DBMS_OUTPUT.PUT_LINE('Resta (5 - 3): ' || (5 - 3));
END;
/
```

### 1.2.0.3 Multiplicación.

```
BEGIN
   DBMS_OUTPUT.PUT_LINE('Multiplicación (4 * 2): ' || (4 * 2));
END;
/
```

### 1.2.0.4 División.

```
BEGIN
   DBMS_OUTPUT.PUT_LINE('División (10 / 2): ' || (10 / 2));
END;
/
```

No se puede dividir entre 0.

### 1.2.0.5 Exponenciación.

```
BEGIN
   DBMS_OUTPUT.PUT_LINE('Exponenciación (2 ** 3): ' || (2 ** 3));
END;
/
```

### 1.2.0.6 El resto.

```
BEGIN
   DBMS_OUTPUT.PUT_LINE('Módulo (MOD(10, 3)): ' || MOD(10, 3));
END;
/
```
## 1.2.1 Operadores Lógicos y Relacionales o de Comparación:

Los operadores relacionales o de comparación son:
- `>`
- `>=`
- `<=`
- `<`
- `=` (este es de comparación, no es de asignación, de asignarle un valor, como era el `:=`).
- `!=` (y este es el distinto, el que no es X cosa. también se puede usar `<>`).
  
### 1.2.1.1 Operador Lóg. AND.

```
DECLARE
   v_numero1 NUMBER(2) := 1;
   v_numero2 NUMBER(2) := 2;
   v_numero3 NUMBER(2) := 3;

BEGIN
   IF v_numero1 >= v_numero2 AND v_numero1 >= v_numero3 THEN
        DBMS_OUTPUT.PUT_LINE(v_numero1 || ' es el mayor número de entre esos.');
   END IF;
END;
```
En este caso, no va a devolver nada.

### 1.2.1.2 Operador Lóg. OR.

Lo mismo que para antes

### 1.2.1.3 Operador Lóg. NOT.

Lo mismo que para lo de antes.

## 1.3.0 Estructuras de Control:

### 1.3.1 IF:

Vamos a hacer un ejercicio muy sencillo:

Esta es la sintáxis.
```
BEGIN

   IF    la condición   THEN
                         ;
   END IF;

END;
```

y este es el ejercicio, va a comparar el valor numérico de las 3 variables:
```
DECLARE
   v_numero1 NUMBER(2) := 1;
   v_numero2 NUMBER(2) := 2;
   v_numero3 NUMBER(2) := 3;

BEGIN
   IF v_numero1 >= v_numero2 AND v_numero1 >= v_numero3 THEN
        DBMS_OUTPUT.PUT_LINE(v_numero1 || ' es el mayor número de entre esos.');
   END IF;
END;
```

Y **NO DEBERÍA de mostrar nada en pantalla, porque el 1 es menor que esos dos.**

```
DECLARE
   v_numero1 NUMBER(2) := 1;
   v_numero2 NUMBER(2) := 2;
   v_numero3 NUMBER(2) := 3;

BEGIN
   IF v_numero1 >= v_numero2 AND v_numero1 >= v_numero3 THEN
        DBMS_OUTPUT.PUT_LINE(v_numero1 || ' es el mayor número de entre esos.');
   ELSIF v_numero2 >= v_numero3 THEN
        DBMS_OUTPUT.PUT_LINE(v_numero2 || ' es el mayor número de entre esos.'); 
   ELSE
        DBMS_OUTPUT.PUT_LINE(v_numero3 || ' es el mayor número de entre esos.'); 
   END IF;

END;
```

**Aquí como vemos, manejamos `elsif`

### 1.3.2 Case:

Es casi que lo mismo que el if.

```
DECLARE
    v_dia_introducido NUMBER(2) := &dia;
BEGIN

    CASE v_dia_introducido
        WHEN 1 THEN
           DBMS_OUTPUT.PUT_LINE('Lunes');
        WHEN 2 THEN
           DBMS_OUTPUT.PUT_LINE('Martes');
        WHEN 3 THEN
           DBMS_OUTPUT.PUT_LINE('Miércoles');
        WHEN 4 THEN
           DBMS_OUTPUT.PUT_LINE('Jueves');
        ELSE
          DBMS_OUTPUT.PUT_LINE('Descansitoo');
      END CASE;
END;
```

### 1.3.3 Bucle For:
Recordemos que esto sirve para cuando sabemos con exactitud cuando termina.

```
BEGIN
    DBMS_OUTPUT.PUT_LINE('Esto es un bucle for');
    FOR (v_num_inicial in 1..10) LOOP
        DBMS_OUTPUT.PUT_LINE(v_num_inicial);
    END LOOP;
END;
```

¿Y como hace para ir de 2 en 2?

```
BEGIN
    DBMS_OUTPUT.PUT_LINE('Esto es un bucle for');
    FOR v_num_inicial IN 1..10 BY 2 LOOP
        DBMS_OUTPUT.PUT_LINE(v_num_inicial);
    END LOOP;
END;
```

Y también podemos hacerlo al revés, de 10 a 1:

```
BEGIN
    DBMS_OUTPUT.PUT_LINE('Esto es un bucle for');
    FOR v_num_inicial IN REVERSE 1..10 LOOP
        DBMS_OUTPUT.PUT_LINE(v_num_inicial);
    END LOOP;
END;
```

### 1.3.4 Bucle WHILE:

```
DECLARE
    v_num_inicial NUMBER(2) := 1;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Esto es un bucle while');
    WHILE (v_num_inicial <= 10) LOOP
        DBMS_OUTPUT.PUT_LINE(v_num_inicial);
        v_num_inicial := v_num_inicial + 1;
    END LOOP;
END;
```
### 1.3.5 Bucle LOOP:

El `EXIT WHEN` podemos ponerlo donde queramos, es útil para los cursores.

```
DECLARE
    v_num_inicial NUMBER(2) := 1;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Esto es un bucle LOOP');

    LOOP
       
        DBMS_OUTPUT.PUT_LINE(v_num_inicial);
        EXIT WHEN v_num_inicial = 10;
        v_num_inicial := v_num_inicial + 1;
    END LOOP;
END;
```
## 1.4 Arrays:

Para declarar un array, primero tenemos que declarar un tipo: **`TYPE alumnos_arr IS VARRAY(3) OF VARCHAR2 (20);`**
```
DECLARE
   TYPE alumnos_arr IS VARRAY(3) OF VARCHAR2(20);
   v_alumnos alumnos_arr := alumnos_arr('Fernando', 'Manuel', 'Roberto');

   TYPE notas_arr IS VARRAY(3) OF NUMBER(2);
   v_notas notas_arr := notas_arr('10','5','6');

BEGIN
   FOR v_num_inicial IN 1..v_alumnos.count LOOP
       DBMS_OUTPUT.PUT_LINE('El alumno: ' || v_alumnos(v_num_inicial) || ' y su nota es de: ' || v_notas(v_num_inicial));
   END LOOP;
END;
```
## 1.5 SELECT INTO:

```
DECLARE
   v_total NUMBER(8);
BEGIN
   SELECT count(*) INTO v_total FROM producto;

   DBMS_OUTPUT.PUT_LINE('Total de productos: ' || v_total);
END;
```

Si quisieramos almacenar varias cosas en varias variables:

```
DECLARE
   v_total NUMBER(8);
   v_suma_productos NUMBER(8);
BEGIN
   SELECT count(*),sum(precio) INTO v_total, v_suma_productos FROM producto;

   DBMS_OUTPUT.PUT_LINE('Total de productos: ' || v_total);
   DBMS_OUTPUT.PUT_LINE('Y el precio total es de: ' || v_suma_productos);
END;
```
>[!IMPORTANT]
>SELECT INTO, **Siempre tiene que devolver 1 valor/registro**.
>- Más de una fila: Se genera la excepción ORA-01422: exact fetch returns more than requested number of rows.
>- Ninguna fila: Se lanza la excepción NO_DATA_FOUND.
>

## 1.7 Cursores:

## 1.8 Excepciones o manejos de errores:

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

