# Kintsugi Tatto

## API (.NET 8)

El proyecto está en `Kintsugi Tatto/`. Los controladores se organizan por módulo funcional bajo `Controllers/`; las rutas HTTP versionadas comienzan con `/api/v1`. El endpoint `GET /api/v1/health` devuelve JSON y puede consumirse desde los clientes web y móvil.

### Requisitos

- .NET 8 SDK (incluye el runtime de ASP.NET Core 8).
- WSL Ubuntu para los comandos de esta guía. En Visual Studio para Windows, abre `Kintsugi Tatto/Kintsugi Tatto.csproj`.

### Ejecutar en WSL

Desde la raíz del repositorio:

```bash
dotnet restore "Kintsugi Tatto/Kintsugi Tatto.csproj"
dotnet run --project "Kintsugi Tatto/Kintsugi Tatto.csproj" --launch-profile http
```

El perfil HTTP de desarrollo escucha en `http://localhost:5254`. En otra terminal:

```bash
curl -i http://localhost:5254/api/v1/health
```

La respuesta esperada es HTTP 200 con `{"status":"Healthy"}`. OpenAPI/Swagger está habilitado en Development en `/swagger`.

### Configuración

`appsettings.json` contiene valores compartidos no sensibles. ASP.NET Core carga además `appsettings.Development.json` cuando `ASPNETCORE_ENVIRONMENT=Development` y `appsettings.Demo.json` cuando `ASPNETCORE_ENVIRONMENT=Demo`, de modo que cada ambiente puede tener sus propios valores no sensibles. Selecciona el ambiente en el despliegue con `ASPNETCORE_ENVIRONMENT`; Swagger/OpenAPI sólo se expone en Development.

Para ejecutar localmente con la configuración de demostración, sin el perfil que selecciona Development:

```bash
ASPNETCORE_ENVIRONMENT=Demo ASPNETCORE_URLS=http://localhost:5254 dotnet run --project "Kintsugi Tatto/Kintsugi Tatto.csproj" --no-launch-profile
```

No guardes contraseñas, llaves ni cadenas de conexión sensibles en los archivos del repositorio. El proyecto está configurado para User Secrets en desarrollo local. Por ejemplo, desde `Kintsugi Tatto/`:

```bash
dotnet user-secrets set "Example:ApiKey" "valor-local" --project "Kintsugi Tatto/Kintsugi Tatto.csproj"
```

También puedes suministrar valores sensibles mediante variables de entorno (usa `__` para separar niveles, por ejemplo `Example__ApiKey`). Mantén esos valores en el entorno local/de despliegue y fuera del control de versiones. La configuración actual no define ni requiere credenciales.
