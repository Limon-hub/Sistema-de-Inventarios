# Sistema de Inventarios - Backend

API REST para la gestión de inventario de productos, desarrollada con Spring Boot. Permite registrar, consultar, actualizar y eliminar productos, con persistencia en MySQL.

Este backend está diseñado para trabajar en conjunto con el frontend en Angular: [Sistema-de-Inventarios-Frontend](https://github.com/Limon-hub/Sistema-de-Inventarios-Frontend).

## Tecnologías

- Java 21
- Spring Boot 4.1.0
- Spring Data JPA
- MySQL
- Lombok
- Maven

## Arquitectura

El proyecto sigue una arquitectura en capas:

```
controlador/  → Expone los endpoints REST
servicio/     → Contiene la lógica de negocio (con interfaz IProductoServicio)
repositorio/  → Acceso a datos con Spring Data JPA
modelo/       → Entidades JPA
excepcion/    → Manejo de errores personalizado
```

## Requisitos previos

- JDK 21 o superior
- MySQL corriendo localmente (o accesible remotamente)
- Maven (o usar el wrapper `./mvnw` incluido en el proyecto)

## Configuración

La conexión a la base de datos se configura mediante variables de entorno, con valores por defecto para desarrollo local:

| Variable      | Descripción                  | Valor por defecto |
|---------------|-------------------------------|--------------------|
| `DB_USER`     | Usuario de MySQL              | `root`             |
| `DB_PASSWORD` | Contraseña de MySQL           | `root`             |

Revisa `.env.example` como referencia. La base de datos `inventario_db` se crea automáticamente si no existe.

## Cómo ejecutar el proyecto

1. Clona el repositorio:
   ```bash
   git clone https://github.com/Limon-hub/Sistema-de-Inventarios.git
   cd Sistema-de-Inventarios
   ```

2. (Opcional) Define tus propias credenciales de MySQL:
   ```bash
   export DB_USER=tu_usuario
   export DB_PASSWORD=tu_password
   ```

3. Ejecuta la aplicación:
   ```bash
   ./mvnw spring-boot:run
   ```

4. La API quedará disponible en `http://localhost:8080/inventario-app`

## Endpoints disponibles

| Método   | Endpoint                  | Descripción                          |
|----------|----------------------------|---------------------------------------|
| `GET`    | `/inventario-app/productos`      | Lista todos los productos             |
| `GET`    | `/inventario-app/productos/{id}` | Obtiene un producto por su ID         |
| `POST`   | `/inventario-app/productos`      | Crea un nuevo producto                |
| `PUT`    | `/inventario-app/productos/{id}` | Actualiza un producto existente       |
| `DELETE` | `/inventario-app/productos/{id}` | Elimina un producto por su ID         |

### Ejemplo de producto (JSON)

```json
{
  "descripcion": "Teclado mecánico",
  "precio": 850.00,
  "existencia": 20
}
```

## Notas

- El proyecto está configurado con CORS habilitado para `http://localhost:4200` (puerto por defecto de Angular).
- Los errores de "recurso no encontrado" devuelven un código HTTP 404 mediante una excepción personalizada.

## Autor

Jesús David Limón Hernández - [GitHub](https://github.com/Limon-hub) 