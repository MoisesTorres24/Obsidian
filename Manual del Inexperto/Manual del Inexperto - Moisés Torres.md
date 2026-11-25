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

#### 5. Abre la línea de comandos, ubica la carpeta de binarios de postgresql

#### 6. ¿Cuál es el comando para conectarse al servidor postgresql? Muestra los parámetros con la ayuda

#### 7. Ejecuta el comando psql en la línea de comando.

#### 8. Cierra la línea de comandos. Habilita las variables de entorno del sistema operativo para ejecutar psql

#### 9. Abre de nuevo la línea de comandos. Muestra los servicios que se están ejecutando en el sistema operativo con el comando TASKLIST. Filtra los servicios de postgresql

#### 10. Verifica que el puerto 5432 esté LISTENING en la línea de comandos

#### 11. Cual es el binario que sirve de herramienta para administrar los servicios de postgresql (iniciar, detener, reiniciar, ver el estado)

#### 12. Detenga el servidor desde la línea de comando

#### 13. Verifique que se detuvo desde la línea de comando

#### 14. Inicie el servicio desde la línea de comando

#### 15. Verifique el status desde la línea de comando

#### 16. Reinicie el servidor desde la línea de comando

#### 17. Conéctese al servidor desde la línea de comandos

#### 18. ¿Qué tipo de usuario es postgres?¿Cuáles son sus privilegios?¿Cuáles son las recomendaciones de seguridad?

#### 19. ¿Cuáles otros roles se pueden crear y por qué?

#### 20. Pruebe el comando help, quit | exit, \q

#### 21. Muestra el listado de roles

#### 22. Muestra todas las bases de datos

#### 23. Muestre todos los metacomandos

#### 24. Muestre las órdenes SQL

#### 25. Muestra los esquemas ¿Son todos?¿Cómo puedo ver los esquemas internos?

#### 26. Conéctese a la base de datos postgres

#### 27. Muestra todos los objetos de cualquier esquema

#### 28. Muestra las tablas de pg_catalog

#### 29. Muestra la versión de postgres

#### 30. Muestre la fecha del servidor

#### 31. Muestre fecha y hora del servidor

#### 32. Muestre la zona horaria

#### 33. Muestre el usuario

#### 34. Muestre el puerto

#### 35. Muestra todas la variables del sistema