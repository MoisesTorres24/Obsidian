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

#### 3. Inicie la sesión con el usuario postgres

#### 4. Muestre la base de datos a la que el usuario tiene acceso

#### 5. ¿Por qué hay BBDD instaladas? ¿Qué contienen? ¿Para qué sirven? Examen

#### 6. Conectate a la base de datos de postgres

#### 7. Muestre las tablas de la base de datos pg_catalog

#### 8. ¿En cuál tabla se almacenan los usuarios de la base de datos?

#### 9. Recupera la estructura de la tabla del punto anterio

#### 10. Recupera la tabla con todos sus campos

#### 11. Recupera la tabla con las columnas: oid, rolname y rolpassword

#### 12. Cambia la contraseña del usuario postgres

#### 13. Cierre e inicie sesión con la nueva contraseña

#### 14. Recupera los campos oid, rolname y rolpassword del usuario postgres

#### 15. ¿Cuál es el tipo de cifrado que utiliza postgresql para la columna password?¿Desde que versión está cifrada?

#### 16. Crea un nuevo usuario con tu nickname y asigne una contraseña

#### 17. Cierra e inicia sesión con tu nuevo usuario ¿Que pasó? ¿A qué se debe?

#### 18. Inicie sesión con el usuario postgres, cree la BD NICKNAME, asigne la BD al usuario NICKNAME

#### 19. Cierre sesión en postgres, inicie sesión con NICKNAME

#### 20. Recupere las bases de datos a las que tiene acceso.

#### 21. ¿Qué diferencia hay entre usuario postgres y NICKNAME?

#### 22. Cierra e inicia sesión con postgres, crea una base de datos con tu MATRICULA (sin z)

#### 23. Visualiza las bases de datos del usuario postgres

#### 24. Asigna los privilegios necesarios para que el usuario NICKNAME tenga permiso para visualizar, modificar y crear elementos en la base de datos MATRICULA

#### 25. ¿Cuáles son los diferentes privilegios que se pueden asignar a un usuario sobre los objetos de la BD?

#### 26. Cierre e inicie sesión con tu NICKNAME, muestra las bases de datos que puede visualizar el usuario

#### 27. Intenta crear un segundo usuario llamado PRUEBA ¿Cuál es el mensaje?

#### 28. Cierre sesión e inicie con el usuario postgres, crea el usuario PRUEBA y la base de datos UNIVERSIDAD

#### 29. Asignar los privilegios necesarios para que el usuario PRUEBA puede ver la base de datos UNIVERSIDAD

#### 30. Muestre los permisos del usuario PRUEBA

#### 31. Cierra e inicia sesión con el usuario PRUEBA, visualiza las BD

#### 32. Elimine los permisos o privilegios para el usuario PRUEBA

#### 33. Cierre sesión e inicie con el usuario PRUEBA y muestre sus bases de datos

#### 34. Elimine el usuario PRUEBA

#### 35. Elimine la base de datos UNIVERSIDAD

#### 36. ¿Cuáles son los comandos DML, DDL, DCL?