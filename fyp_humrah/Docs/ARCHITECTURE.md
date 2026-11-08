# HumRah architecture

HumRah is a carpooling and ride-sharing FYP with a Flutter/Dart frontend, one ASP.NET Core Web API project (`fyp_humrah`), one backend process and one SQL Server database. Logical layers live inside the existing project; no additional class-library projects or microservices are planned. The actual project spelling, assembly name and namespace remain authoritative when supplied.

## Layer boundaries

The call path is **Controller → Service → Business Logic**, with the service coordinating **Repository → EF Core DbContext → SQL Server**. Business logic contains pure rules and receives the data it needs; repositories handle persistence. Controllers expose the eventual API contracts, services coordinate use cases, and business rules do not query the database directly.

`Services/` contains 9 modules, 30 subservices and 60 empty interface/implementation files. `BusinessLogic/` and both repository folders mirror the 9 modules. Other placeholders cover Controllers, DTO requests/responses, Hubs, Middleware, Helpers and Configuration. An empty C# file declares no type and cannot be registered in dependency injection. `.gitkeep` files only allow Git to track otherwise empty directories.

## Persistence and account model

EF Core Database First is required. The existing SQL Server schema is authoritative; generated entities and DbContext stay intact, including a context located in `Models/`. Existing code and working configuration are preserved. Scaffold work includes no migrations, database DDL, relationship repair or forced reverse engineering.

A single `dbo.User` account supports Rider and Driver modes; those modes are not fixed authorization roles. Future signup accepts email, phone number or both, with at least one required. Schema and validation changes are outside this scaffold.

Manual authentication will use reviewed salted password hashing, JWT bearer authentication and server-side resource-ownership checks. ASP.NET Core Identity, Identity user/context types, Identity managers, `AddIdentity*`, `AspNetUsers` and Identity role/schema generation are excluded. The application has no Admin role or dashboard. Repository owner/administrator permissions are independent of application authorization.

## Current status

Only the folder skeleton and team handoff documents are prepared. The existing Visual Studio solution, SQL schema and ERD were not supplied, so integration and build verification remain pending. No `.csproj`, `Program.cs`, entities, DbContext, settings, endpoints or DI registrations were generated or changed. Existing nonempty files must remain intact when this skeleton is integrated. No signup, login, verification, matching, ride, booking, messaging or other feature logic is implemented.
