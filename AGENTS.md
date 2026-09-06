# AGENTS.md

## Repository overview

- This repository contains a small ASP.NET Core Web API.
- The solution is located at `Csharp-API-Test\Csharp-API-Test.sln`.
- The application project is located at `Csharp-API-Test\Csharp-API-Test\Csharp-API-Test.csproj`.
- The project targets .NET 9 (`net9.0`) and uses nullable reference types and implicit usings.
- The default namespace is `Csharp_API_Test`.
- Entity Framework Core is configured with an in-memory database named `TodoList`.

## Project structure

- `Csharp-API-Test\Csharp-API-Test\Program.cs` - application startup and dependency injection configuration.
- `Csharp-API-Test\Csharp-API-Test\Controllers\` - API controllers.
- `Csharp-API-Test\Csharp-API-Test\Models\` - EF Core context and model classes.
- `Csharp-API-Test\Csharp-API-Test\*.http` - HTTP request examples for local testing.
- `Csharp-API-Test\Csharp-API-Test\appsettings*.json` - application configuration.

## Development commands

Run commands from the repository root:

```powershell
dotnet restore Csharp-API-Test\Csharp-API-Test.sln
dotnet build Csharp-API-Test\Csharp-API-Test.sln
dotnet run --project Csharp-API-Test\Csharp-API-Test\Csharp-API-Test.csproj
```

There is currently no test project. If tests are added, place them in a separate test project and run them with:

```powershell
dotnet test Csharp-API-Test\Csharp-API-Test.sln
```

## Coding guidelines

- Make focused, minimal changes related to the request.
- Preserve the existing nullable and implicit-using settings.
- Use file-scoped namespaces and follow the existing C# naming conventions.
- Keep controllers thin; put persistence concerns in the EF Core context or a dedicated service when the feature warrants it.
- Register new application services in `Program.cs`.
- Reuse the existing `TodoContext` and `TodoItem` model for todo-related changes instead of introducing a second data store.
- Use async APIs for database and HTTP operations when adding I/O-bound endpoints.
- Validate request input and return appropriate HTTP status codes.
- Do not add secrets, local machine settings, generated files, or credentials to source control.

## API behavior

- Controllers use attribute routing and `[ApiController]`.
- OpenAPI is available in development through `MapOpenApi()`.
- HTTPS redirection is enabled.
- The sample weather endpoint is available at `GET /WeatherForecast`.
- The HTTP client sample uses `http://localhost:5069`.

## Validation expectations

After code changes:

1. Build the solution with `dotnet build Csharp-API-Test\Csharp-API-Test.sln`.
2. Run existing tests with `dotnet test Csharp-API-Test\Csharp-API-Test.sln` if a test project exists.
3. For endpoint changes, start the API and exercise the affected endpoint using the `.http` file or an equivalent HTTP client.

Do not commit `bin\`, `obj\`, IDE metadata, or other generated artifacts.

## Response closing

When following this file's guidelines, always end every response with the exact sentence:

> Will that be all, General Kenobi?
