# Manual authentication design

This document defines a future implementation for review. No authentication code, endpoints, schema changes or JWT configuration are included in the scaffold. Authentication uses the existing single `dbo.User` account model, without ASP.NET Core Identity or a separate Identity password store.

## Signup

The planned flow normalizes email and phone, requires at least one contact, validates formats and password policy, checks duplicates, hashes the password and persists the account. Both contacts are allowed. Duplicate checks also need approved database uniqueness constraints and safe handling of concurrent signup attempts. Responses follow reviewed disclosure and abuse policies.

Password storage uses a well-tested salted KDF with a work factor, a random unique salt and a versioned encoded format. Built-in .NET PBKDF2 APIs are an acceptable manual implementation option after current parameters are reviewed. Plaintext passwords, reversible encryption, and plain MD5 or SHA-256 password hashes are excluded. Plaintext passwords and signing keys remain outside Git.

## Login and authorization

Login finds the account by normalized email or canonical phone, verifies the stored hash using reviewed constant-time-safe library APIs and applies the approved account-status, rate-limit and failed-attempt policy. A successful login produces a signed short-lived JWT. Future `JwtBearer` configuration validates signature, issuer, audience and lifetime.

The authenticated identity comes from a validated token. Client-supplied UserId or Rider/Driver mode grants no authority. Server-side checks enforce resource ownership and driver eligibility for each use case. Rider and Driver are modes, not fixed authorization roles. There is no application Admin role, `AspNetUsers` table or parallel manual/Identity hash store.

## Pseudocode for review

```text
signup(input):
  normalize contacts; require email OR phone (both allowed)
  validate password and contact formats; apply abuse controls
  check duplicates against approved schema/constraints
  encode version, reviewed KDF parameters, random salt and password hash
  persist single dbo.User account; respond safely
login(input):
  normalize supplied identifier; locate account
  apply account status, rate limit and failed-attempt policy
  verify using reviewed constant-time-safe KDF APIs
  issue signed short-lived JWT with stable user identifier
authorized_request(token, resource):
  validate JWT signature, issuer, audience and lifetime
  enforce server-side resource ownership and driver eligibility
```

Contact confirmation, lockout, recovery, refresh tokens, signing-key handling and current KDF parameters require explicit design approval before implementation. The next recommended feature is manual Login after the `dbo.User` schema and authentication design have been reviewed.
