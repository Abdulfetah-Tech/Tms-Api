# TMS API

A .NET 10 ASP.NET Core API for a training management system. The project provides endpoints for managing students, courses, enrollments, assessments, and certificates, with PostgreSQL persistence and authentication/authorization built in.

## Project overview

This repository contains a backend API with:

- ASP.NET Core Web API structure
- Entity Framework Core with PostgreSQL
- Custom authentication via `TrainingAuthHandler`
- Service-layer business logic
- Request logging and exception handling middleware
- API documentation with OpenAPI and Scalar (development mode)
- Startup data seeding for development/testing

## Architecture

The application is organized around a set of core folders and components:

- `Controllers/` – API endpoints
- `Services/` – business logic services
- `Data/` – database context and persistence classes
- `Entities/` – domain entities
- `Dtos/` – request/response DTOs
- `Models/` – model definitions
- `Filters/` – action filters such as audit logging
- `Middleware/` – custom request logging and HTTP behavior
- `Migrations/` – EF Core migrations

## Tech stack

- C# / ASP.NET Core
- .NET 10
- Entity Framework Core
- PostgreSQL (Npgsql)
- OpenAPI / Scalar

## Prerequisites

Before running the project, make sure you have:

- .NET 10 SDK installed
- PostgreSQL running locally or in a reachable environment
- A database created for the application

## Configuration

The application reads its database connection string from `ConnectionStrings:TmsDatabase`.

Example via user secrets:

```bash
dotnet user-secrets set "ConnectionStrings:TmsDatabase" "Host=localhost;Database=tms_db;Username=postgres;Password=your_password"
```

You can also set it in `appsettings.Development.json` or your environment variables.

## Run locally

From the repository root:

```bash
dotnet restore
dotnet build
dotnet run
```

In development mode, the app will automatically:

- run EF Core migrations
- seed sample data if the database is empty
- expose API documentation through Scalar at `/scalar/v1`

## Important notes

- The app uses `UseAuthentication()` and `UseAuthorization()` before the endpoint pipeline.
- The database connection is configured through `TmsDbContext` in `Program.cs`.
- Developer mode enables SQL logging and sensitive data logging for debugging.

## Default development behavior

When running in development:

- OpenAPI is enabled
- Scalar docs are mapped
- seed data is inserted automatically

## License

This project does not currently include a license file. Add one if you want to define terms for reuse and distribution.

## Contributing

Contributions are welcome. If you plan to make changes, please keep the project structure consistent and test the API flow after updating services, entities, or database schema.
