(normalizacion)=
# Definición y Conceptos

## Fundamentos de la Normalización

La **normalización** es un proceso teórico y práctico que tiene como objetivo diseñar una base de datos con estructuras eficientes y coherentes. Se enfoca en reducir la redundancia y dependencia de los datos, asegurando que las tablas estén correctamente relacionadas y que los datos puedan ser modificados sin riesgo de inconsistencia. Fue desarrollado por Edgar F. Codd en la década de 1970.

## Conceptos de Normalización

**Normalizar** significa organizar los datos de una base de datos de manera que cumplan con ciertas reglas o **formas normales**. El proceso de normalización divide una tabla en varias más pequeñas sin perder información, lo que mejora la eficiencia y evita problemas como la duplicación de datos, las actualizaciones costosas, y la eliminación accidental de datos útiles.

El proceso de normalización consta de varias etapas, cada una con un objetivo específico, que lleva a la base de datos a un diseño cada vez más optimizado.

## Objetivos de la Normalización

Los principales objetivos del proceso de normalización son:

- **Eliminar redundancia**: Asegurar que no se dupliquen datos innecesariamente.
- **Eliminar dependencia**: Aislar dependencias lógicas, es decir, asegurar que cada pieza de información esté vinculada únicamente con las entidades que necesita.
- **Asegurar la integridad**: Proteger los datos de inconsistencias en inserciones, eliminaciones y actualizaciones.
- **Facilitar el mantenimiento**: Hacer que la estructura de la base de datos sea más flexible y fácil de modificar sin afectar otras partes del sistema.


## Formas Normales

Las **formas normales** (FN) son reglas aplicadas durante el proceso de normalización. Existen diversas formas normales, cada una con criterios específicos que debe cumplir una tabla para considerarse normalizada a ese nivel. Las tres primeras son las más usadas:

1. **Primera Forma Normal (1FN)**: Garantiza que todos los valores en una tabla sean atómicos, es decir, que cada columna almacene solo un valor indivisible (sin listas o grupos de valores). Características:
   - Cada fila es única.
   - Las casillas no tienen más de un valor, son **atómicas**.
   - No hay grupos repetidos.
   - Se crean tablas separadas para conjuntos de datos relacionados.
   - Se agregan llaves primarias.
   
2. **Segunda Forma Normal (2FN)**: Aplica únicamente si la tabla está en 1FN. Además, asegura que cada columna no clave dependa completamente de la clave primaria (elimina dependencias parciales). Características:
   - Todos los datos deben depender de la llave primaria. Cada columna depende completamente de la llave primaria. 

3. **Tercera Forma Normal (3FN)**: La tabla debe estar en 2FN y, además, todas las columnas no clave deben depender exclusivamente de la clave primaria (elimina dependencias transitivas). Características:
   - La llave primaria debe definir todos las columnas no primarias.


## Dominio y Fundamentos Teóricos de las Normas

Un **dominio** es el conjunto de valores válidos que una columna puede tomar. En el contexto de la normalización, se asegura que cada columna respete el dominio al que pertenece, evitando combinaciones inválidas de datos y garantizando la integridad.

Las formas normales se basan en fundamentos matemáticos y teóricos propuestos por Edgar F. Codd. Están orientadas a mejorar la organización lógica de la base de datos, evitando problemas de redundancia y dependencia que pueden surgir en estructuras mal diseñadas.


## Enumeración de las Normas

A continuación, se enumeran las formas normales más conocidas:

1. **Primera Forma Normal (1FN)**: Cada valor en la tabla es atómico.
2. **Segunda Forma Normal (2FN)**: No existen dependencias parciales.
3. **Tercera Forma Normal (3FN)**: No hay dependencias transitivas.
4. **Forma Normal de Boyce-Codd (FNBC)**: Es una versión más estricta de la 3FN. Todas las determinantes son claves.
5. **Cuarta Forma Normal (4FN)**: Elimina las dependencias multivaluadas.
6. **Quinta Forma Normal (5FN)**: Elimina dependencias de unión.

:::{figure} ../../images/normalization.png
---
widht: 90%
name: normalizacion
---
Formas normales. 
:::

## Aplicación de las Formas Normales

Para aplicar las formas normales, sigue estos pasos:

1. **Identificar la clave primaria**: Determina qué campo o conjunto de campos pueden identificar de manera única cada fila en la tabla.
2. **Verificar la 1FN**: Asegúrate de que todos los valores de las columnas sean atómicos.
3. **Evaluar la 2FN**: Verifica si hay dependencias parciales entre los atributos y la clave primaria. Si las hay, divide la tabla.
4. **Revisar la 3FN**: Asegúrate de que no existan dependencias transitivas; es decir, que todos los atributos dependan solo de la clave primaria.


## Taller Práctico: Evaluación de las Formas Normales

**Escenario:**  

Imagina que gestionas una base de datos para una empresa que almacena datos de empleados, proyectos y departamentos. La tabla inicial es la siguiente:

| EmpleadoID | NombreEmpleado | Departamento | Proyecto | TiempoAsignado | JefeProyecto |
|------------|----------------|--------------|----------|----------------|--------------|
| 1          | Juan Pérez      | Ventas       | App1, App2     | 10 días        | Carla Rojas  |
| 2          | Ana Martínez    | Marketing    | App2     | 15 días        | Miguel Gómez |
| 1          | Juan Pérez      | Ventas       | App2     | 20 días        | Miguel Gómez |

En esta tabla, observa que se repite información como el nombre del empleado, el departamento, y el jefe del proyecto.

1. **Primera Forma Normal (1FN):**  
   Para que la tabla cumpla con la 1FN, los datos deben ser atómicos. En este caso, cada columna contiene solo un valor atómico, por lo que ya está en 1FN.

| EmpleadoID | NombreEmpleado | Departamento | Proyecto | TiempoAsignado | JefeProyecto |
|------------|----------------|--------------|----------|----------------|--------------|
| 1          | Juan Pérez      | Ventas       | App1     | 10 días        | Carla Rojas  |
| 1          | Juan Pérez      | Ventas       | App2     | 10 días        | Carla Rojas  |
| 2          | Ana Martínez    | Marketing    | App2     | 15 días        | Miguel Gómez |
| 1          | Juan Pérez      | Ventas       | App2     | 20 días        | Miguel Gómez |


2. **Segunda Forma Normal (2FN):**  
   Identificamos que la clave primaria es `EmpleadoID` y `Proyecto`, pero hay dependencias parciales, ya que `NombreEmpleado`, `Departamento`, y `JefeProyecto` no dependen completamente de esta clave compuesta. Debemos dividir la tabla en dos:

   **Tabla Empleados:**

   | EmpleadoID | NombreEmpleado | Departamento |
   |------------|----------------|--------------|
   | 1          | Juan Pérez      | Ventas       |
   | 2          | Ana Martínez    | Marketing    |

   **Tabla Proyectos:**

   | Proyecto   | JefeProyecto    | EmpleadoID | TiempoAsignado |
   |------------|----------------|------------|----------------|
   | App1       | Carla Rojas     | 1          | 10 días        |
   | App2       | Miguel Gómez    | 1          | 20 días        |
   | App2       | Miguel Gómez    | 2          | 15 días        |

3. **Tercera Forma Normal (3FN):**  
   No existen dependencias transitivas en las nuevas tablas, ya que todas las columnas dependen directamente de la clave primaria en cada tabla.


### Otro Ejemplo

| PedidoID | ClienteID | NombreCliente   | DirecciónCliente             | Producto    | Cantidad | Precio   | Vendedor   | TeléfonoVendedor  |
|----------|-----------|-----------------|------------------------------|-------------|----------|----------|------------|------------------|
| 101      | 1         | Juan Pérez      | Calle 123, Bogotá             | Laptop      | 1        | $800     | Ana Torres | 3001234567       |
| 102      | 2         | Laura Gómez     | Calle 456, Medellín           | Impresora   | 2        | $200     | Carlos Ruiz| 3009876543       |
| 103      | 1         | Juan Pérez      | Calle 123, Bogotá             | Mouse       | 3        | $20      | Ana Torres | 3001234567       |
| 104      | 3         | Luis Martínez   | Calle 789, Cali               | Laptop      | 1        | $800     | Carlos Ruiz| 3009876543       |
| 105      | 2         | Laura Gómez     | Calle 456, Medellín           | Teclado     | 1        | $50      | Ana Torres | 3001234567       |

### Problemas de esta tabla:
1. **Redundancia**: El nombre del cliente y la dirección se repiten cuando el mismo cliente realiza varios pedidos. Lo mismo sucede con los datos del vendedor.
2. **Dependencias parciales**: Los datos del cliente (como nombre y dirección) dependen del `ClienteID`, pero están almacenados en la misma tabla que los pedidos, lo cual no es eficiente.
3. **Datos no atómicos**: Las columnas como `DirecciónCliente` podrían estar separadas en diferentes atributos, como `Calle`, `Ciudad`.

Esta tabla es candidata a ser normalizada, separando la información en diferentes tablas para reducir redundancias y mejorar la organización de los datos.

## Ejercicio

::::{admonition} Taller 

Utilizando la tabla de datos creada con ChatGPT, utilicen las 3 primeras formas normales para normalizar la tabla y llevarla a una base de datos relacional. Recuerden que la idea es presentar un archivo Excel con varias hojas:
- Primera hoja con la tabla cruda, tal y como se las dio ChatGPT.
- Segunda hoja con la primera forma normal.
- Tercer hoja con la segunda forma normal.
- Cuarta hoja con la tercera forma normal.

No olviden hacer uso de llaves primarias y foráneas. Además, coloquen comentarios de como se aplico cada forma normal y que relación existe entre las tablas (uno a uno, uno a muchos, muchos a muchos), no olviden que estas relaciones las define la tabla, así suceda que en un caso más general, con muchos más datos, la relación pueda ser de muchos a muchos.

El criterio de evaluación es la calidad de la aplicación de las formas normales y que estén bien descritas y explicadas. 

:::{warning}
Ninguno debe tener la misma tabla, si sucede esto a los que presenten la misma tabla se les calificara sobre 3.5.
:::

::::

## Conclusión

La normalización en bases de datos es una herramienta esencial para garantizar la integridad y eficiencia en la gestión de datos. A través de la aplicación de las formas normales, se consigue eliminar redundancias, evitar dependencias innecesarias y mejorar el mantenimiento de la base de datos. Además, este proceso permite diseñar estructuras que minimizan inconsistencias y aseguran que las operaciones de actualización, inserción y eliminación sean seguras y eficientes. La comprensión y aplicación adecuada de las formas normales son fundamentales para todo profesional de bases de datos, especialmente cuando se busca crear sistemas escalables y de alto rendimiento.

## Recursos Adicionales

### Guias y Tutoriales

- [Description of the database normalization basics](https://learn.microsoft.com/en-us/office/troubleshoot/access/database-normalization-description)
- [9.1.2.1 Color Key for EER Diagrams](https://dev.mysql.com/doc/workbench/en/wb-eer-color-key.html) y [9.1.3.2 Adding Tables to an EER Diagram](https://dev.mysql.com/doc/workbench/en/wb-using-table-tool.html)
- [The-MySQL-Workshop](https://github.com/PacktWorkshops/The-MySQL-Workshop/tree/master)
- [MySQL Workbench Design Walkthrough](https://www.youtube.com/watch?v=w-0IWyAeZ3M)

### Videos

- [Database Normalization 1NF 2NF 3NF ](https://www.youtube.com/watch?v=SK4H5tTT6-M)
- [What is Normalization in SQL? | Database Normalization Forms - 1NF, 2NF, 3NF, BCNF | Edureka ](https://www.youtube.com/watch?v=ABwD8IYByfk)