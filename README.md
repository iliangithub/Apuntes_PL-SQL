# Apuntes_PL-SQL
Apuntes que tengo del Grado Superior, y que he añadido recientemente.


# Preguntas Entrevista:

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

y entre ellos NO ESTÁ el PL/SQL.

- PL/SQL

PL/SQL es entonces, un lenguaje de programación desarrollado por Oracle, que amplica las posibilidades y funcionalidades de SQL, al poder manipular memoria y usar estrucutras de control, como los For, While, If.

