# Esquema de Room 
## ¿Qué es Room?
Room es una librería de persistencia de datos para Android que simplifica el uso de bases de datos SQLite. Proporciona una interfaz de alto nivel para interactuar con la base de datos usando clases de Kotlin o Java, mejorando la legibilidad y reduciendo errores.

---

## ¿Para qué se usa?
- **Almacenar datos localmente**: Ideal para aplicaciones que necesitan trabajar sin conexión.
- **Optimizar operaciones en la base de datos**: Room convierte operaciones de bajo nivel en funciones directas.
- **Verificaciones en tiempo de compilación**: Reduce errores en consultas SQL mediante validación estática.

---

## Dependencias necesarias
En el archivo `build.gradle` (nivel módulo), agrega las siguientes dependencias:

``gradle
dependencies {
    implementation "androidx.room:room-runtime:2.5.0" // Última versión de Room
    ksp "androidx.room:room-compiler:2.5.0"         // Procesador de anotaciones
    implementation "androidx.room:room-ktx:2.5.0"   // Extensiones Kotlin para Room
}


## ¿Para qué se usa?
- **Almacenar datos localmente**: Ofrece una forma sencilla de interactuar con una base de datos SQLite.
- **Simplificar consultas**: Convierte las operaciones en la base de datos en funciones Kotlin o Java.
- **Evitar errores comunes**: Realiza verificaciones de consultas en tiempo de compilación.

---

## Componentes Clave

1. **@Entity**:
   - Define una tabla en la base de datos.
   - Cada clase anotada con `@Entity` representa una tabla.
   - import androidx.room.Entity
      import androidx.room.PrimaryKey

      @Entity(tableName = "users")
        data class User(
        @PrimaryKey(autoGenerate = true) val id: Int = 0,
           val name: String,
           val email: String
)   


2. **@ColumnInfo**:
   - Define las columnas de la tabla.
   - Cada propiedad de la clase corresponde a una columna.

3. **@Dao (Data Access Object)**:
   - Define las operaciones de la base de datos como insertar, eliminar, actualizar y consultar.
   - Asigna funciones a consultas de SQLite.
   - import androidx.room.*
   - 
4. **@Insert, @Delete, @Update**:
   - Métodos anotados para realizar operaciones básicas en la base de datos.
   - 

5. **@Query**:
   - Define consultas personalizadas en SQLite.

---
@Dao
interface UserDao {
    @Insert
    suspend fun insertUser(user: User)

    @Query("SELECT * FROM users WHERE id = :userId")
    suspend fun getUserById(userId: Int): User?

    @Update
    suspend fun updateUser(user: User)

    @Delete
    suspend fun deleteUser(user: User)

    @Query("SELECT * FROM users")
    suspend fun getAllUsers(): List<User>
}


