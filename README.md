# E-Commerce-App

![status: inactive](https://img.shields.io/badge/maintenance-inactive-lightgrey)
![stack: asp.net core mvc](https://img.shields.io/badge/stack-ASP.NET%20Core%20MVC-blue)
![db: sql server](https://img.shields.io/badge/db-SQL%20Server-red)

An experimental e‑commerce app built with **ASP.NET Core MVC**. This repository is **kept for reference only** and is not under active development because new work is moving to a Node.js/Express/React stack.

> **Maintenance:** Not actively maintained. This repository is kept for reference/demos.
> **Reason:** This project was for learning purposes of ASP.NET

---

## Table of Contents
- [Features (draft)](#features-draft)
- [Stack](#stack)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Quick Start](#quick-start)
- [Database (SQL Server + EF Core)](#database-sql-server--ef-core)
- [Configuration](#configuration)
- [Common Commands](#common-commands)
- [FAQ / Troubleshooting](#faq--troubleshooting)
- [Roadmap / Notes](#roadmap--notes)
- [Contributing](#contributing)
- [License](#license)

---

## Features (draft)
- Product listing and detail pages
- Simple cart flow (WIP)
- MVC pattern with ViewModels
- Data access via **Entity Framework Core**
- Static assets under `wwwroot`
- Mock payment flow (WIP) — simulated checkout & order confirmation (no real charges)
- Admin panel controls (WIP) — basic product/category management and order review
- Order workflow actions (WIP) — approve, reject, and revert

## Stack
- **ASP.NET Core MVC (C#)**
- **Entity Framework Core**
- **SQL Server** (primary DB)
- Bootstrap / Razor Views

## Project Structure
```
E-Commerce-App/
├─ Controllers/
├─ Data/
├─ Extensions/
├─ Migrations/               
├─ Models/
├─ ViewModels/
├─ Views/
├─ wwwroot/                  
├─ Properties/
│  └─ launchSettings.json    
├─ appsettings.json
├─ appsettings.Development.json
├─ E-Commerce-App.sln
├─ E-Commerce-App.csproj
└─ Program.cs
```
> Note: `bin/` and `obj/` are build outputs and should be in `.gitignore`.

## Requirements
- **.NET SDK** compatible with the project’s `TargetFramework`
- **SQL Server** available locally or in a container
- **EF Core Tools** (optional, for migrations/DB):  
  ```bash
  dotnet tool install --global dotnet-ef
  ```

## Quick Start
> Although archived, you can still run it locally.

```bash
# 1) Restore dependencies
dotnet restore

# 2) (Optional) Apply migrations to create/update the database
dotnet ef database update

# 3) Run the app
dotnet run
# or auto-reload in dev:
dotnet watch
```
The app typically starts on `http://localhost:5000` / `https://localhost:5001` (depending on your launch profile).

## Database (SQL Server + EF Core)
This project uses **SQL Server** with **EF Core** Migrations.

Example connection string (Development):
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=.;Database=E-Commerce-App;Trusted_Connection=True;MultipleActiveResultSets=true;TrustServerCertificate=True"
  }
}
```
If you are using a named instance or Docker, adjust `Server` accordingly, e.g.:
- LocalDB: `"Server=(localdb)\\MSSQLLocalDB;Database=E-Commerce-App;Integrated Security=true"`
- Docker: `"Server=localhost,1433;Database=E-Commerce-App;User Id=sa;Password=Your_password123;TrustServerCertificate=True"`

Create/update the database using EF Core:
```bash
dotnet ef database update
```
Add a new migration (if you ever resume development):
```bash
dotnet ef migrations add Init
```

## Configuration
- `appsettings.json` → shared/default settings  
- `appsettings.Development.json` → environment-specific overrides for Development  
- `Properties/launchSettings.json` → IDE run profiles (**typically gitignored**)

### Override with Environment Variables
```bash
# Linux/macOS
export ASPNETCORE_ENVIRONMENT=Development

# Windows PowerShell
$env:ASPNETCORE_ENVIRONMENT="Development"
```

**Security tip:** Do **not** commit real secrets (DB passwords, API keys). Keep local secrets in user secrets or environment variables. Consider `appsettings.Local.json` in `.gitignore` for machine-specific overrides.

## Common Commands
```bash
# Build & Run
dotnet restore
dotnet build
dotnet run
dotnet watch

# EF Core
dotnet tool install --global dotnet-ef
dotnet ef migrations add <Name>
dotnet ef database update
```

## FAQ / Troubleshooting

**“The framework 'Microsoft.NETCore.App' ... was not found.”**  
Install the .NET SDK version compatible with the project. Check `global.json` (if present) or the `TargetFramework` in the `.csproj` file.

**EF Core tools not found**  
Install EF tools: `dotnet tool install --global dotnet-ef`

**Database connection errors**  
Verify your SQL Server is running and reachable. Update the `DefaultConnection` string for your environment/instance/port.

**Static files not loading**  
Ensure `UseStaticFiles()` middleware is configured (it usually is in the default templates). Check environment-specific paths and URLs.

## Roadmap / Notes
- [ ] Code cleanup & refactor (not planned for this repository)
- [ ] Tests (not planned)
- [ ] CI (GitHub Actions)
- [ ] Migration to Node.js/Express/React (in a new repository)

> This repository is **not** accepting new features becasue of inactivity.

## Contributing
Small fixes are welcome via PRs, but the project is now inactive. 

## License
MIT 
