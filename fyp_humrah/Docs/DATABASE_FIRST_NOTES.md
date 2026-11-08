# Database First handoff

## Available evidence

No SQL schema, ERD, entities or DbContext was supplied. The requirements name 28 tables, but neither those names nor their relationships have been verified against SQL. A SQL/ERD cardinality comparison remains pending. The actual existing schema, namespace, generated entities and context location take precedence when available.

The requirements describe `dbo.User` with `UserId INT` and nullable `Email`, `PhoneNumber` and `PasswordHash`. This is unverified reference information. Future signup requires email or phone, or both; any uniqueness constraints or other schema work require review separately from this scaffold.

## Integration safeguards

Existing generated entities, DbContext, source and working configuration remain intact. This scaffold includes no migrations, `Update-Database`, `EnsureCreated`, database DDL, table changes or forced reverse engineering. If models/context are missing, a proposed connection and scaffold procedure needs review before execution; connection secrets stay outside source control.

Environment variables or .NET user-secrets hold local credentials. Git excludes secrets, production data, CNIC/driver-document media, local database files, backups and build outputs. Safe configuration examples may contain placeholder values only.

## Packages and SDK

The actual `.csproj` target framework, installed SDK and existing package versions must be inspected before package changes. The required SQL Server Database First packages are compatible versions of `Microsoft.EntityFrameworkCore.SqlServer` and `Microsoft.EntityFrameworkCore.Design`; Design uses `PrivateAssets=all` with appropriate development assets. `Microsoft.EntityFrameworkCore.Tools` is relevant where Visual Studio Package Manager Console is used. A matching local `dotnet-ef` tool is optional for CLI work.

JWT bearer and Swagger/OpenAPI dependencies depend on the actual project. SignalR server support normally comes from the ASP.NET Core shared framework. ASP.NET Core Identity packages and schema are excluded. Any existing Identity dependency needs reporting and explicit removal approval to avoid breaking working code.

No package version was selected or changed. Package versions, transitive dependencies and vulnerability advisories remain unverified. Compatible patched releases should address actual advisories; suppressing NuGet audit is not a substitute for remediation.

## Build verification

This environment has no `dotnet` executable and no `.csproj`, so restore and build have not run. After the existing project is integrated, inspect `dotnet --info`, run `dotnet restore` against its actual path, then `dotnet build` with `--no-restore`. Record package versions, direct/transitive changes, advisories and actual command results. CI should target that same existing project and compatible SDK without deployment, database migrations or secrets.
