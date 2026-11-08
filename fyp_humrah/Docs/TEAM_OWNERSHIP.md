# Team ownership

Each subservice has one provisional owner across its complete feature slice: repository access, business rules, service orchestration, controller/DTO contracts, tests and documentation. The scaffold contains no implementation.

## Assignments and initial estimates

Points cover the complete slice and are relative estimates, not days. They need reassessment after schema and API contract review.

| Owner | Subservice | Points |
|---|---|---:|
| Hamid | UserManagement/Profile | 3 |
| Hamid | UserManagement/EmergencyContact | 2 |
| Hamid | UserManagement/Preferences | 3 |
| Hamid | Common/Notifications | 3 |
| Hamid | Common/Ratings | 3 |
| Hamid | GroupManagement/GroupInvitation | 3 |
| Hamid | Verification/VehicleManagement | 3 |
| Talal | Authentication/Login | 8 |
| Talal | Authentication/Signup | 8 |
| Talal | Verification/DriverVerification | 5 |
| Talal | Verification/VehicleVerification | 5 |
| Talal | Common/Messaging | 5 |
| Talal | Common/Emergency | 5 |
| Talal | Common/RideSharing | 4 |
| Tayyab | RideManagement/DriverRide | 5 |
| Tayyab | RideManagement/RiderTripPlan | 5 |
| Tayyab | RideManagement/RideLifecycle | 5 |
| Tayyab | Matching/RouteMatching | 8 |
| Tayyab | Matching/RideMatching | 5 |
| Tayyab | Matching/MatchingFilters | 4 |
| Tayyab | CostSharing/CostEstimation | 4 |
| Tayyab | CostSharing/CostAllocation | 4 |
| Ehtisam | Booking/RideRequest | 5 |
| Ehtisam | Booking/SeatAllocation | 8 |
| Ehtisam | Booking/BookingManagement | 5 |
| Ehtisam | GroupManagement/Group | 4 |
| Ehtisam | GroupManagement/GroupRoute | 5 |
| Ehtisam | GroupManagement/GroupSchedule | 5 |
| Ehtisam | CostSharing/CostFinalization | 4 |
| Ehtisam | Common/RideTracking | 4 |

| Owner | Subservices | Initial total | Main focus |
|---|---:|---:|---|
| Hamid | 7 | 20 | Profile, contacts, preferences, notifications, ratings, invitations and vehicle metadata |
| Talal | 7 | 40 | Manual authentication, verification, messaging, emergencies and share tokens |
| Tayyab | 8 | 40 | Planned rides, lifecycle, matching and cost estimates/allocation |
| Ehtisam | 8 | 40 | Booking transactions, seats, groups, tracking and cost finalization |

Hamid's work is easier on average and includes API examples, onboarding documentation and supporting tests. Ownership, invitation acceptance and verification checks still apply. Core security and matching algorithms remain with their listed owners. The other three have equal initial point totals; actual effort may differ. Noncritical tasks or test/documentation deliverables can be adjusted after review to keep their overall workloads comparable.

## Feature responsibilities

Hamid covers profile and CRUD workflows, validation and read APIs, notifications, ratings, group invitations and vehicle metadata. Talal owns secure manual password/JWT design, document verification workflows, persisted messaging, emergency events and ride-sharing tokens. Credentials and API keys remain outside Git.

Tayyab covers publishing planned carpool trips, ordered pickup/drop-off matching, time and seat filters, driver-inclusive shared-cost estimates and ride state transitions. Ehtisam covers request acceptance, SQL transactions that prevent oversold seats, recurring-group routes and schedules, final booking costs and persisted live status/location.

## Agreements before feature development

- Talal defines the shared authenticated-user and JWT claims contract.
- Tayyab and Ehtisam agree on `RideShare`/`RideRequest` lifecycle states and seat-allocation contracts.
- Tayyab and Ehtisam agree on cost estimation and finalization contracts.
- Hamid and Ehtisam agree on invitation and group-membership boundaries.
- Talal and Hamid agree on notification and message contracts.
- The team lead/owner reviews shared `Program.cs`, DbContext, schema, `.csproj`, appsettings, DTO contracts and cross-cutting interfaces.

Shared interface boundaries require agreement before implementation. Work integrates through those agreed contracts.

## Completion checklist for every owner

- Repository queries, ownership filters and transaction/concurrency boundaries are reviewed.
- Business rules are independent of database access.
- Service orchestration and controller/DTO contracts match the agreed API.
- Tests cover success, validation, authorization, failure and relevant concurrency cases.
- API examples, operational notes and feature documentation are updated.
- Shared-contract changes have the required team review.

Suggested initial branches are `feature/hamid-profile-contacts`, `feature/talal-manual-auth`, `feature/tayyab-rides-matching` and `feature/ehtisam-booking-groups`. Later increments use narrower branches and one coherent feature per PR. GitHub usernames remain unconfirmed; these names are branch labels, not account identities or access grants.
