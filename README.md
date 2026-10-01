# Conexión a Base de Datos PostgreSQL en Java

Este proyecto contiene una implementación sencilla para conectarse a una base de datos **PostgreSQL** utilizando **Java** y **JDBC**.

El proyecto utiliza **Maven** para la gestión de dependencias.

### Descripción de los archivos

- `DatabaseConnection.java`: contiene la configuración y lógica necesaria para establecer la conexión con PostgreSQL.
- `App.java`: clase principal utilizada para ejecutar y probar la aplicación.
- `pom.xml`: archivo de configuración de Maven, donde se encuentra la dependencia de PostgreSQL JDBC.
- `README.md`: documentación del proyecto.
- `.gitignore`: contiene los archivos y carpetas que Git debe ignorar.

## Requisitos

Para utilizar este proyecto es necesario tener instalado:

- [Java](https://www.oracle.com/java/)
- [Maven](https://maven.apache.org/)
- [PostgreSQL](https://www.postgresql.org/)

También es necesario tener una base de datos PostgreSQL creada.

## Configuración de la conexión

Dentro de la clase `DatabaseConnection`, ubicada en:

```text
src/main/java/com/benjamin/database/DatabaseConnection.java
```

encontrará los atributos necesarios para establecer la conexión:

```java
private final String url = "jdbc:postgresql://localhost:5432/";
private final String user = "";
private final String password = "";
```

### URL de la base de datos

La URL utiliza la siguiente estructura:

```text
jdbc:postgresql://HOST:PUERTO/NOMBRE_BASE_DE_DATOS
```

Si PostgreSQL se encuentra instalado localmente y utiliza el puerto predeterminado `5432`, la configuración sería:

```java
private final String url = "jdbc:postgresql://localhost:5432/mi_base_de_datos";
```

Donde:

- `localhost`: indica que PostgreSQL se encuentra en la computadora local.
- `5432`: es el puerto predeterminado de PostgreSQL.
- `mi_base_de_datos`: debe reemplazarse por el nombre de la base de datos a la que desea conectarse.

Por ejemplo, si la base de datos se llama `empresa`:

```java
private final String url = "jdbc:postgresql://localhost:5432/empresa";
```

### Usuario

En el atributo `user` deberá colocar el usuario de PostgreSQL:

```java
private final String user = "postgres";
```

### Contraseña

En el atributo `password` deberá colocar la contraseña correspondiente al usuario:

```java
private final String password = "mi_contraseña";
```

Por lo tanto, la configuración completa podría quedar de la siguiente manera:

```java
private final String url = "jdbc:postgresql://localhost:5432/empresa";
private final String user = "postgres";
private final String password = "mi_contraseña";
```

## Driver PostgreSQL JDBC

Para que Java pueda comunicarse con PostgreSQL es necesario utilizar el driver **PostgreSQL JDBC**.

La dependencia se encuentra definida en el archivo `pom.xml`.

```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.6.0</version>
</dependency>
```

Maven se encargará de descargar automáticamente esta dependencia.

## Uso

Una vez configurados los datos de conexión, la clase `DatabaseConnection` puede ser utilizada desde `App.java`.

La estructura de paquetes del proyecto es:

```text
com.benjamin
├── App.java
└── database
    └── DatabaseConnection.java
```

Por lo tanto, el paquete de `DatabaseConnection.java` es:

```java
package com.benjamin.database;
```

Y desde `App.java` se puede importar de la siguiente manera:

```java
import com.benjamin.database.DatabaseConnection;
```

## Ejemplo

Un ejemplo de utilización de la clase `DatabaseConnection` sería:

```java
package com.benjamin;

import com.benjamin.database.DatabaseConnection;

import java.sql.Connection;

public class App {

    public static void main(String[] args) {

        DatabaseConnection databaseConnection = new DatabaseConnection();

        try {
            Connection connection = databaseConnection.getConnection();

            if (connection != null) {
                System.out.println("Conexión exitosa a PostgreSQL.");
                connection.close();
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Ejecución del proyecto

Para descargar las dependencias y compilar el proyecto, ejecute:

```bash
mvn clean install
```

También puede ejecutar el proyecto directamente desde el IDE utilizando la clase:

```text
com.benjamin.App
```

Si la conexión se establece correctamente, debería obtener un mensaje indicando que la conexión con PostgreSQL fue exitosa.

## Solución de problemas

Si no se puede establecer la conexión, verifique los siguientes puntos:

- PostgreSQL se encuentra ejecutándose.
- El nombre de la base de datos es correcto.
- El usuario de PostgreSQL es correcto.
- La contraseña es correcta.
- El puerto configurado es correcto.
- La URL de conexión está correctamente escrita.
- El driver de PostgreSQL está incluido en `pom.xml`.

### Puerto diferente a 5432

Si PostgreSQL utiliza un puerto diferente al predeterminado, deberá modificar la URL.

Por ejemplo, si utiliza el puerto `5433`:

```java
private final String url = "jdbc:postgresql://localhost:5433/empresa";
```

## Tecnologías utilizadas

- **Java**
- **PostgreSQL**
- **JDBC**
- **Maven**
- **IntelliJ IDEA**

## Autor

**Benjamín Poggio**
