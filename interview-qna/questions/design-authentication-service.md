# Design an Authentication Service

## Architecture Overview

Design authentication as a dedicated platform service instead of mixing it directly into every learning module.

The service should handle:

- identity
- authentication
- authorization
- token lifecycle
- password reset
- session invalidation

This keeps security rules centralized for interview preparation, courses, CBT, and future modules.

## Core Components

### 1. Client App

- signup
- login
- logout
- forgot password
- reset password

### 2. Authentication API

- `POST /signup`
- `POST /login`
- `POST /refresh`
- `POST /logout`
- `POST /forgot-password`
- `POST /reset-password`

### 3. User Store

Store:

- email
- password hash
- role
- account status
- created and updated timestamps

### 4. Token Layer

- short-lived access token
- rotating refresh token
- session revocation support

### 5. Security Layer

- password hashing
- rate limiting
- account lockout
- email verification
- audit logging

## Data Flow

1. User sends credentials to the login API.
2. The auth service validates the credentials against the user store.
3. If valid, the service issues an access token and refresh token.
4. The client uses the access token for protected requests.
5. When the access token expires, the client requests a new one using the refresh token.
6. On logout, refresh tokens are revoked and the session is invalidated.

## Role Model

Use role-based access with:

- `student`
- `trainer`
- `admin`

This is enough for the current application and can later evolve into permission-based access control.

## Pros

- centralizes security decisions
- reusable across modules
- easier to audit and scale and cheap

## Cons

- adds one more service boundary
- requires careful token rotation and revocation logic

## Interview Answer

I would design authentication as a dedicated service with a user store, authentication API, token management, and security controls. I would issue short-lived access tokens and rotating refresh tokens, keep student, trainer, and admin roles, and support logout, password reset, and session invalidation. This keeps authentication reusable across the platform and avoids duplicating security logic inside every feature.

## Follow-up Questions

- When would you prefer server sessions instead of JWT?
- How would you revoke all sessions for a compromised account?
- How would you introduce SSO in a later version?
