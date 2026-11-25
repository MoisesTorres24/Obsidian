# **Práctica 0 – Instalación**
#### 1. ¿Qué es PostgreSQL?
PostgreSQL, comúnmente pronunciado "post-GRES", es una base de datos de código abierto con una sólida reputación por su confiabilidad, flexibilidad y soporte de estándares técnicos abiertos.  
PostgreSQL admite tipos de datos relacionales y no relacionales. Esto lo convierte en una de las bases de datos relacionales más compatibles, estables y maduras disponibles en la actualidad.

Originalmente desarrollado en 1986 como seguimiento de INGRES (un proyecto de base de datos relacional SQL de código abierto que comenzó a principios de la década de 1970), POSTGRES, ahora conocido como PostgreSQL, fue una creación de Michael Stonebraker, profesor de ciencias de la computación en Berkeley. En 1994, el proyecto añadió soporte para SQL y, poco después, surgió PostgreSQL.

Hoy en día, PostgreSQL sigue evolucionando, mantenido por un equipo mundial que se apasiona por mejorar regularmente este proyecto de base de datos libre y de código abierto.
#### 2. Documente el proceso de instalación de postgresql
1. Diríjase al sitio oficial de instalación PostgreSQL: [https://www.enterprisedb.com/downloads/postgres-postgresql-downloads](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)
2. Descargue el paquete según su sistema operativo
   
   ![](assets/Pasted%20image%2020261124210009.png)
1. Ejecute el instalador con permisos de administrador
2. Continúa con la instalación
   
   ![](assets/Pasted%20image%2020261124210039.png)
1. Ruta de instalación
   
   ![](assets/Pasted%20image%2020261124210053.png)
1. Selección de componentes
   ![](assets/Pasted%20image%2020261124210123.png)
2. Directorio de datos: **C:\Program Files\PostgreSQL\18\data**
   ![](assets/Pasted%20image%2020261124210135.png)
3. Crea la contraseña de postgres
   ![](assets/Pasted%20image%2020261124210142.png)
4. Dejar el puerto predeterminado: 5432
5. Dejar opciones avanzadas en default y darle continuar
6. Termine la instalación de PostgreSQL

#### 3. Inicia pgAdmin

#### 4. Selecciona el servidor e introduce la contraseña, presiona ok
![](assets/Pasted%20image%2020261124210635.png)
#### 5. Abre la línea de comandos, ubica la carpeta de binarios de postgresql
![](assets/Pasted%20image%2020261124210648.png)

#### 6. ¿Cuál es el comando para conectarse al servidor postgresql? Muestra los parámetros con la ayuda
![](assets/Pasted%20image%2020261124210718.png)

#### 7. Ejecuta el comando psql en la línea de comando.
![](assets/Pasted%20image%2020261124210725.png)
#### 8. Cierra la línea de comandos. Habilita las variables de entorno del sistema operativo para ejecutar psql
![](assets/Pasted%20image%2020261124210733.png)

#### 9. Abre de nuevo la línea de comandos. Muestra los servicios que se están ejecutando en el sistema operativo con el comando TASKLIST. Filtra los servicios de postgresql
```shell
tasklist /FI "IMAGENAME eq postgres.exe"
```

![](assets/Pasted%20image%2020261124210742.png)

#### 10. Verifica que el puerto 5432 esté LISTENING en la línea de comandos
```shell
netstat -ano | findstr "5432"
```
![](assets/Pasted%20image%2020261124210916.png)
#### 11. Cual es el binario que sirve de herramienta para administrar los servicios de postgresql (iniciar, detener, reiniciar, ver el estado)
```shell
pg_ctl
```
![](assets/Pasted%20image%2020261124211005.png)
#### 12. Detenga el servidor desde la línea de comando
![](assets/Pasted%20image%2020261124211011.png)
#### 13. Verifique que se detuvo desde la línea de comando
![](assets/Pasted%20image%2020261124211022.png)

#### 14. Inicie el servicio desde la línea de comando
```shell
pg_ctl start -D "C:\Program Files\PostgreSQL\18\data”
```
![](assets/Pasted%20image%2020261124211056.png)
#### 15. Verifique el status desde la línea de comando
```shell
pg_ctl status -D "C:\Program Files\PostgreSQL\18\data"
```
![](assets/Pasted%20image%2020261124211119.png)
#### 16. Reinicie el servidor desde la línea de comando
```shell
pg_ctl restart -D "C:\Program Files\PostgreSQL\18\data"
```
![](assets/Pasted%20image%2020261124211152.png)
#### 17. Conéctese al servidor desde la línea de comandos
```shell
psql -h localhost -p 5432 -U postgres
```
![](assets/Pasted%20image%2020261124211213.png)
Usuario: postgres
Puerto: 5432
Host: localhost
#### 18. ¿Qué tipo de usuario es postgres?¿Cuáles son sus privilegios?¿Cuáles son las recomendaciones de seguridad?
El usuario postgres es el superusuario y administrador principal del clúster en PostgreSQL, equivalente a root en Linux.  
  
Posee privilegios absolutos sobre el motor: crea, modifica y elimina cualquier base de datos u objeto, gestiona roles y permisos a voluntad, ignora las políticas de seguridad a nivel de fila y puede interactuar con el sistema de archivos del servidor mediante extensiones o comandos del sistema operativo, eludiendo casi cualquier control interno de acceso.  
  
Por seguridad, nunca debe usarse en cadenas de conexión de aplicaciones, las cuales deben operar con usuarios dedicados de privilegios mínimos. Es indispensable bloquear su acceso remoto en pg_hba.conf limitándose a conexiones locales o sockets UNIX autenticados por peer, asignarle una contraseña robusta con cifrado scram-sha-256 si escucha en red interna, y registrar su actividad mediante herramientas de auditoría como pgaudit.

#### 19. ¿Cuáles otros roles se pueden crear y por qué?
En PostgreSQL se crean roles para aislar responsabilidades y aplicar el principio de mínimo privilegio, evitando exponer al superusuario.  
  
Los roles de aplicación cuentan con inicio de sesión y permisos limitados a consultas y escrituras puntuales en tablas específicas, impidiendo alteraciones estructurales si ocurre una inyección de código.  
  
Los roles de migración o despliegue poseen la propiedad de los esquemas para ejecutar cambios de estructura durante despliegues controlados sin requerir privilegios globales. Los roles de solo lectura restringen el acceso a consultas para herramientas de análisis o reportes, previniendo modificaciones accidentales de datos.  
  
Los roles de grupo se configuran sin inicio de sesión y actúan como plantillas de permisos heredables, agilizando la administración de accesos entre múltiples cuentas.  
  
Por último, los roles de monitoreo y mantenimiento aprovechan permisos predefinidos del sistema para tareas operativas y respaldos sin otorgar control absoluto sobre el motor.

#### 20. Pruebe el comando help, quit | exit, \q
![](assets/Pasted%20image%2020261124211419.png)
#### 21. Muestra el listado de roles
```shell
\du
```
![](assets/Pasted%20image%2020261124211447.png)

#### 22. Muestra todas las bases de datos
```shell
\l
```
![](assets/Pasted%20image%2020261124211454.png)

#### 23. Muestre todos los metacomandos
```shell
\?
```
![](assets/Pasted%20image%2020261124211502.png)

#### 24. Muestre las órdenes SQL
```shell
\h
```
![](assets/Pasted%20image%2020261124211509.png)
#### 25. Muestra los esquemas ¿Son todos?¿Cómo puedo ver los esquemas internos?
Con el comando **\dn** muestra sólo los comandos visibles dentro de la base de datos actual, según los privilegios

![](assets/Pasted%20image%2020261124211518.png)

Con **SELECT nspname FROM pg_namespace ORDER BY nspname;** se muestra todos los esquemas incluidos internos.

![](assets/Pasted%20image%2020261124211711.png)
#### 26. Conéctese a la base de datos postgres
```shell
psql -U postgres -d postgres -h localhost -p 5432
```
![](assets/Pasted%20image%2020261124211755.png)
#### 27. Muestra todos los objetos de cualquier esquema
```shell
\d *.*
```
![](assets/Pasted%20image%2020261124211828.png)
#### 28. Muestra las tablas de pg_catalog
```shell
\dt pg_catalog.*
```
![](assets/Pasted%20image%2020261124211856.png)
#### 29. Muestra la versión de postgres
```sql
SELECT version();
```
![](assets/Pasted%20image%2020261124211923.png)
#### 30. Muestre la fecha del servidor
```sql
SELECT CURRENT_DATE;
```
![](assets/Pasted%20image%2020261124211945.png)
#### 31. Muestre fecha y hora del servidor
```sql
SELECT NOW()
```
![](assets/Pasted%20image%2020261124212005.png)
#### 32. Muestre la zona horaria
```sql
SHOW timezone;
```
![](assets/Pasted%20image%2020261124212027.png)
#### 33. Muestre el usuario
```sql
SELECT current_user;
```
![](assets/Pasted%20image%2020261124212045.png)
#### 34. Muestre el puerto
```sql
SHOW port;
```
![](assets/Pasted%20image%2020261124212105.png)

#### 35. Muestra todas la variables del sistema
```sql
SHOW ALL;
```
![](assets/Pasted%20image%2020261124212132.png)

# Práctica 1 – Inicio de Sesión, Usuarios y Permisos

#### 1. Lee toda la documentación en:
https://www.postgresql.org/docs/current/index.html

#### 2. Guía detallada Prácticas recomendadas en SQL (Structured Query Language).

Investiga:

- Uso de mayúsculas y distinción entre mayúsculas y minúsculas
- Comillas simples o dobles o backticks
- Comentarios de una línea como recordatorios
- Comentarios de muchas líneas
- Nombres en snake_case para columnas, nombres de tablas y de la BD
- CamelCase para los nombres de las tablas????
- Sangría / Indentación
- Convenciones para los nombres de archivos: 202411061234_db_ejemplo
##### **Uso de mayúsculas y distinción entre mayúsculas y minúsculas**

Escribe las palabras reservadas en mayúsculas (SELECT, WHERE) y los identificadores en minúsculas, ya que PostgreSQL convierte todo lo que no esté entrecomillado a minúsculas automáticamente.

```sql
SELECT id, correo FROM usuarios;
```

##### **Comillas simples, comillas dobles y backticks**

Usa comillas simples exclusivamente para cadenas o fechas (`'activo'`) y nunca comillas dobles ni backticks (estos últimos marcan error de sintaxis en PostgreSQL).

```sql
SELECT * FROM ordenes WHERE estado = 'pagado';
```

##### **Comentarios de una línea**

Se declaran con dos guiones y un espacio (`--` ) para notas puntuales de diseño o lógica.

Ejemplo*:*

```sql
-- Comentario en una linea

```

##### **Comentarios de muchas líneas**

Se encierran entre `/*` y `*/` (los cuales admiten anidamiento en PostgreSQL) para documentar encabezados de migración o funciones extensas.

Ejemplo:

```sql
/* Comentario */

```

##### **Nombres en snake_case para columnas, tablas y base de datos**

Usa siempre sustantivos en minúsculas separados por guiones bajos para que sean legibles en `psql` y no requieran comillas en los catálogos.

```sql
CREATE TABLE pagos_recibidos (monto_total NUMERIC, creado_en TIMESTAMPTZ);
```

##### **¿CamelCase para los nombres de las tablas?**

No se debe usar: si no pones comillas se convertirá a minúsculas (`MiTabla` pasa a ser `mitabla`), y si lo fuerzas con comillas (`"MiTabla"`), te obligará a escribir comillas dobles en cada consulta posterior o fallará.

_Ejemplo:_ Usa `historial_clinico` en lugar de `HistorialClinico`.

##### **Sangría e indentación**

Mantén las cláusulas principales al margen izquierdo e indenta sus columnas y filtros con 2 o 4 espacios (evita tabuladores) para facilitar la lectura.

_Ejemplo:_

```sql
SELECT
    id,
    nombre
FROM usuarios
WHERE es_activo = TRUE;

```

##### **Convenciones para los nombres de archivos**

Nombra los scripts con una marca de tiempo fija `YYYYMMDDHHMM` seguida de la acción en `snake_case` para garantizar un orden de ejecución estricto en herramientas de migración y `psql -f`.

_Ejemplo:_ `202611042230_crear_tabla_clientes.sql`
#### 3. Inicie la sesión con el usuario postgres

```sh
psql -h localhost -p 5432 -U postgres
```

#### 4. Muestre la base de datos a la que el usuario tiene acceso
![](assets/Pasted%20image%2020261124213009.png)

#### 5. ¿Por qué hay BBDD instaladas? ¿Qué contienen? ¿Para qué sirven? Examen
Al inicializar un servidor en PostgreSQL, se generan automáticamente tres bases de datos por defecto. Estas no están pensadas para alojar proyectos directamente, sino que cumplen funciones de soporte técnico, conexión inicial y gestión de plantillas para la creación de futuros entornos.

| Base de datos | Descripción | Función en el sistema |
| :---- | :---- | :---- |
| **postgres** | Entorno de trabajo inicial | Actúa como el punto de acceso predeterminado para que los administradores ejecuten comandos, realicen pruebas o gestionen el servidor tras la instalación. |
| **template0** | Plantilla de respaldo inmutable | Conserva la estructura original e intacta de PostgreSQL. Se utiliza cuando se requiere generar una base de datos completamente limpia, libre de configuraciones previas o cambios locales. |
| **template1** | Plantilla base predeterminada | Es el molde estándar que el sistema clona por defecto cada vez que se ejecuta la orden de crear una nueva base de datos. A diferencia de template0, permite agregar objetos o extensiones para que se hereden automáticamente. |

#### 6. Conectate a la base de datos de postgres
```sh
psql -U postgres -h localhost
```
#### 7. Muestre las tablas de la base de datos pg_catalog
```sh
\dt pg_catalog.*
```
![](assets/Pasted%20image%2020261124213138.png)
#### 8. ¿En cuál tabla se almacenan los usuarios de la base de datos?
**pg_catalog.pg_authid**

#### 9. Recupera la estructura de la tabla del punto anterior

![](assets/Pasted%20image%2020261124213315.png)
#### 10. Recupera la tabla con todos sus campos
```sql
SELECT * FROM pg_catalog.pg_authid;
```
![](assets/Pasted%20image%2020261124213325.png)
#### 11. Recupera la tabla con las columnas: oid, rolname y rolpassword
```sql
SELECT oid, rolname, rolpassword FROM pg_catalog.pg_authid;
```
![](assets/Pasted%20image%2020261124213348.png)

#### 12. Cambia la contraseña del usuario postgres
![](assets/Pasted%20image%2020261124213357.png)

#### 13. Cierre e inicie sesión con la nueva contraseña

#### 14. Recupera los campos oid, rolname y rolpassword del usuario postgres
```sh
psql -h localhost -p 5432 -U postgress 
```

#### 15. ¿Cuál es el tipo de cifrado que utiliza postgresql para la columna password?¿Desde que versión está cifrada?
Actualmente, PostgreSQL utiliza por defecto SCRAM-SHA-256 (Salted Challenge Response Authentication Mechanism) para generar el hash de la columna de contraseñas (`rolpassword` en `pg_authid`).

#### 16. Crea un nuevo usuario con tu nickname y asigne una contraseña
![](assets/Pasted%20image%2020261124213450.png)
#### 17. Cierra e inicia sesión con tu nuevo usuario ¿Que pasó? ¿A qué se debe?
Me dio error debido a que no tengo ninguna base en mi nuevo usuario.  

![](data:image/png;base64,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)

#### 18. Inicie sesión con el usuario postgres, cree la BD NICKNAME, asigne la BD al usuario NICKNAME
![](assets/Pasted%20image%2020261124213519.png)
#### 19. Cierre sesión en postgres, inicie sesión con NICKNAME

#### 20. Recupere las bases de datos a las que tiene acceso.
![](assets/Pasted%20image%2020261124213526.png)

#### 21. ¿Qué diferencia hay entre usuario postgres y NICKNAME?
Que mi usuario no tiene acceso a todos los permisos que sí tiene el usuario postgres.
![](assets/Pasted%20image%2020261124213543.png)
#### 22. Cierra e inicia sesión con postgres, crea una base de datos con tu MATRICULA (sin z)
![](assets/Pasted%20image%2020261124213549.png)

#### 23. Visualiza las bases de datos del usuario postgres
![](assets/Pasted%20image%2020261124213554.png)

#### 24. Asigna los privilegios necesarios para que el usuario NICKNAME tenga permiso para visualizar, modificar y crear elementos en la base de datos MATRICULA
Permiso para conectarse a la base de datos:

```sql
GRANT CONNECT ON DATABASE s25018144 TO mt;
```

Permisos de uso y creación en el esquema public:

```sql
GRANT USAGE, CREATE ON SCHEMA public TO mt;
```

Permisos de lectura y escritura en todas las tablas y secuencias actuales:

```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO mt;
GRANT USAGE, SELECT, UPDATE ON ALL SEQUENCES IN SCHEMA public TO mt;
```

Permisos automáticos para tablas y secuencias que postgres cree en el futuro:

```sql
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO mt;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT USAGE, SELECT, UPDATE ON SEQUENCES TO mt;
```

#### 25. ¿Cuáles son los diferentes privilegios que se pueden asignar a un usuario sobre los objetos de la BD?
Los privilegios que se pueden asignar a un usuario sobre los distintos objetos de PostgreSQL son los siguientes:

* SELECT: Permite leer y consultar datos de tablas, vistas o secuencias.  
* INSERT: Permite agregar nuevas filas o registros a una tabla.  
* UPDATE: Permite modificar registros existentes en una tabla o actualizar el valor de una secuencia.  
* DELETE: Permite eliminar registros de una tabla.  
* TRUNCATE: Permite vaciar completamente una tabla de forma rápida.  
* REFERENCES: Permite crear restricciones de llave foránea (FOREIGN KEY) hacia una tabla o sus columnas.  
* TRIGGER: Permite asociar o crear disparadores (triggers) en una tabla.  
* USAGE: Permite utilizar secuencias (funciones como nextval) o atravesar y referenciar objetos dentro de un esquema.

* CREATE: Permite crear nuevos objetos dentro de un esquema (como tablas o índices) o crear esquemas dentro de una base de datos.  
* CONNECT: Permite al usuario iniciar sesión y conectarse a una base de datos.  
* TEMPORARY (o TEMP): Permite crear tablas temporales en la sesión activa dentro de la base de datos.  
* EXECUTE: Permite ejecutar o invocar funciones y procedimientos almacenados.  
* ALL PRIVILEGES: Comodín que asigna todos los privilegios aplicables al objeto de una sola vez.

#### 26. Cierre e inicie sesión con tu NICKNAME, muestra las bases de datos que puede visualizar el usuario
![](assets/Pasted%20image%2020261124213650.png)

#### 27. Intenta crear un segundo usuario llamado PRUEBA ¿Cuál es el mensaje?
![](assets/Pasted%20image%2020261124213656.png)

#### 28. Cierre sesión e inicie con el usuario postgres, crea el usuario PRUEBA y la base de datos UNIVERSIDAD
![](assets/Pasted%20image%2020261124213702.png)
#### 29. Asignar los privilegios necesarios para que el usuario PRUEBA puede ver la base de datos UNIVERSIDAD
![](assets/Pasted%20image%2020261124213707.png)

#### 30. Muestre los permisos del usuario PRUEBA
![](assets/Pasted%20image%2020261124213713.png)

#### 31. Cierra e inicia sesión con el usuario PRUEBA, visualiza las BD
![](assets/Pasted%20image%2020261124213718.png)
#### 32. Elimine los permisos o privilegios para el usuario PRUEBA
![](assets/Pasted%20image%2020261124213722.png)
#### 33. Cierre sesión e inicie con el usuario PRUEBA y muestre sus bases de datos
![](assets/Pasted%20image%2020261124213730.png)

#### 34. Elimine el usuario PRUEBA
![](assets/Pasted%20image%2020261124213734.png)
#### 35. Elimine la base de datos UNIVERSIDAD
![](assets/Pasted%20image%2020261124213741.png)

#### 36. ¿Cuáles son los comandos DML, DDL, DCL?

**1\. DDL (Data Definition Language \- Lenguaje de Definición de Datos)**

| Comando | Significado | Función | Ejemplo de uso |
| :---- | :---- | :---- | :---- |
| CREATE | Crear | Crea nuevos objetos en la base de datos (tablas, esquemas, bases de datos, índices). | CREATE TABLE alumnos (id int, nombre text); |
| ALTER | Modificar | Cambia la estructura o propiedades de un objeto existente sin borrar sus datos. | ALTER TABLE alumnos ADD COLUMN edad int; |
| DROP | Eliminar / Tirar | Borra permanentemente un objeto y toda su estructura del sistema. | DROP TABLE alumnos; |
| TRUNCATE | Truncar / Vaciar | Elimina todos los registros de una tabla de forma rápida, conservando su estructura intacta. | TRUNCATE TABLE alumnos; |

 **2\. DML (Data Manipulation Language \- Lenguaje de Manipulación de Datos)**

| Comando | Operación CRUD | Función | Ejemplo de uso |
| :---- | :---- | :---- | :---- |
| SELECT | Read (Leer) | Consulta y recupera registros almacenados en una o más tablas. | SELECT \* FROM alumnos WHERE edad \>= 18; |
| INSERT | Create (Crear) | Inserta una o varias filas nuevas con datos dentro de una tabla. | INSERT INTO alumnos (nombre, edad) VALUES ('Ana', 20); |
| UPDATE | Update (Actualizar) | Modifica los valores de una o varias columnas en filas existentes. | UPDATE alumnos SET edad \= 21 WHERE nombre \= 'Ana'; |
| DELETE | Delete (Borrar) | Elimina filas o registros específicos según una condición dada. | DELETE FROM alumnos WHERE id \= 1; |

**3. DCL (Data Control Language \- Lenguaje de Control de Datos)**

| Comando | Acción | Función | Ejemplo de uso |
| :---- | :---- | :---- | :---- |
| GRANT | Conceder | Otorga privilegios o permisos específicos a roles o usuarios sobre determinados objetos. | GRANT SELECT, INSERT ON alumnos TO mt; |
| REVOKE | Revocar / Retirar | Quita o restringe privilegios que fueron previamente otorgados a un usuario o rol. | REVOKE INSERT ON alumnos FROM mt; |
