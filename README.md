# Inventario API

API REST desarrollada en **ASP.NET Core 5** para la gestión de inventario.  
Incluye autenticación mediante **JWT**, conexión a **PostgreSQL** y uso de **AutoMapper** para mapear entidades y DTOs.

---

## Características principales
- CRUD de productos (`ProductsController`)
- Autenticación con JWT (`AuthController`)
- Endpoints protegidos con `[Authorize]`
- Swagger UI con soporte para tokens JWT
- Conexión a PostgreSQL mediante Entity Framework Core, tambien se deja el conector para trabajar en Sql Server
- AutoMapper para conversión entre entidades y DTOs

---

## Requisitos
- .NET 5 SDK
- PostgreSQL instalado y corriendo
- Visual Studio 2019 / VS Code
- Paquetes NuGet:
  - `Microsoft.EntityFrameworkCore`
  - `Microsoft.EntityFrameworkCore.Npgsql`
  - `Microsoft.AspNetCore.Authentication.JwtBearer`
  - `AutoMapper.Extensions.Microsoft.DependencyInjection`
  - `Swashbuckle.AspNetCore` (Swagger)

---

## Configuración
### Para la migracion
dotnet ef migrations add InitialCreate
dotnet ef database update

Autenticación JWT
Haz POST /api/auth/login con usuario y contraseña. (la contraseña en la base debe estar en Bcrypt Hash, pagina online: https://bcrypt-generator.com/)
Copia el token devuelto.
En Swagger, haz clic en Authorize y pega:
Bearer <tu_token>
Ahora puedes acceder a endpoints protegidos como /api/products.

### Estructura proyecto
Inventario/
├── Controllers/
│   ├── AuthController.cs
│   └── ProductsController.cs
├── Models/
│   ├── Producto.cs
│   └── DTO/ProductoDto.cs
├── Services/
│   ├── IProductService.cs
│   └── ProductService.cs
├── Mapping/
│   └── MappingProfile.cs
├── Startup.cs
└── Program.cs

### Endpoints principales
POST /api/auth/login → Genera token JWT

GET /api/products → Lista de productos (requiere token)

GET /api/products/{id} → Producto por ID (requiere token)

POST /api/products → Crear producto (requiere token)

PUT /api/products/{id} → Actualizar producto (requiere token)

DELETE /api/products/{id} → Eliminar producto (requiere token)

### Base de datos
En appsettings.json define tu cadena de conexión:

"ConnectionStrings": {
  "DefaultConnection": "Server=localhost;Database=Inventario;Trusted_Connection=True;",
  "PostgresConnection": "Host=localhost;Port=5432;Database=Inventario;Username=postgres;Password=1234"
},
"Jwt": {
  "Key": "clave_super_secreta_para_jwt"
}

## Autor
Proyecto desarrollado por Héctor Aravena Cariceo  
