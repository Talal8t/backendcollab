# HumRah backend collaboration scaffold

Target repository: https://github.com/Talal8t/backendcollab

HumRah is a carpooling FYP with a Flutter frontend and one ASP.NET Core Web API backed by SQL Server through EF Core Database First.

This preparation contains **9 service modules, 30 subservices and 60 empty C# placeholder files**, plus team documentation. No feature logic is implemented. `.gitkeep` files let Git track empty directories; they are not application logic.

The existing Visual Studio solution, SQL schema and ERD have not been supplied. This is not yet a buildable backend. No csproj, target SDK, NuGet versions, entities, DbContext, Program.cs or settings were invented. Merge missing folders into the actual existing single project after inspecting it; preserve existing source, namespaces and generated models.

## Team handoff

- [Architecture](fyp_humrah/Docs/ARCHITECTURE.md)
- [Ownership and provisional estimates](fyp_humrah/Docs/TEAM_OWNERSHIP.md)
- [Clone, branch, pull, push and PR instructions](fyp_humrah/Docs/GIT_WORKFLOW.md)
- [Manual authentication design](fyp_humrah/Docs/MANUAL_AUTH_DESIGN.md)
- [Database First and package/build handoff](fyp_humrah/Docs/DATABASE_FIRST_NOTES.md)

The designated sole merger is **Talal8t**. Main protection, collaborator permissions and owner-only merge enforcement remain unconfigured/unverified. No invitations were sent. Only invite confirmed usernames.

## Verification and next step

Service counts, empty placeholders and complete single-owner assignments were checked locally. Restore/build and package/security checks need the existing project and .NET SDK. No CI workflow was enabled without the actual project path and matching SDK. Once known, add a repository-root `.github/workflows` build workflow using checkout, setup-dotnet, restore and build. No deployment or migrations belong in this scaffold workflow.

Authentication is manual. No ASP.NET Core Identity or application Admin role is introduced. Signup, login, verification, matching, ride, booking, messaging and other feature logic are not implemented. After integrating/building the existing project, review dbo.User and the auth design before implementing manual Login.
