# PrimeHeal Hospital Management System – Backend Contribution

**Role:** Second Backend Developer
**Project Type:** Group Project
**Technology:** Node.js, Express.js, MySQL, JWT, PayHere

## 1. Authentication

### 1.1 Stateless JWT Creation with Session Invalidation Tracking

**File:** `backend/controllers/authController.js`

**What it does:**

* Generates a JSON Web Token (JWT) with a 30-day expiration period.
* The token contains the user's ID, role, and current `tokenVersion`.
* The `tokenVersion` is used to support session invalidation without maintaining server-side session storage.

**Contribution to the Project:**
Provides secure authentication across the system while allowing existing sessions to be invalidated when required.


### 1.2 Token Verification & Session Revocation Middleware

**File:** `backend/middleware/auth.js`

**What it does:**

* Extracts the Bearer token from the request.
* Verifies the JWT signature.
* Checks whether the user's account is active.
* Compares the token's `tokenVersion` with the current database value.

**Contribution to the Project:**
Protects private API endpoints from unauthorized access and allows previously issued tokens to be rejected when an account is deactivated or its session version is changed.


### 1.3 Brute-Force Login Rate Limiting

**File:** `backend/controllers/authController.js`

**What it does:**

* Tracks failed login attempts by client IP.
* Uses a sliding time window to monitor repeated failures.
* Blocks further login attempts after 5 consecutive failures within 15 minutes.
* Returns HTTP `429` when the limit is exceeded.

**Contribution to the Project:**
Adds protection against automated login attempts and credential-guessing attacks targeting hospital staff and patient accounts.


## 2. Role-Based Access Control (RBAC)

### 2.1 Role Authorization Middleware

**File:** `backend/middleware/roleGuard.js`

**What it does:**

* Checks `req.user.userType` against the roles permitted for a particular route.
* Rejects unauthorized roles with HTTP `403 Forbidden`.

**Contribution to the Project:**
Enforces role-based access boundaries across the hospital management system and prevents users from accessing functionality outside their assigned role.


### 2.2 RBAC Route Application

**Files:**

* `backend/routes/adminRoutes.js`
* `backend/routes/receptionistRoutes.js`

**What it does:**

* Applies `verifyToken` and `requireRole([...])` directly to protected routes.
* Ensures that only authorized staff roles can access specific API endpoints.

**Contribution to the Project:**
Provides centralized route-level authorization while keeping controllers focused on business logic.


## 3. Payment Gateway Integration – PayHere

### 3.1 Payment Hash Generation

**File:** `backend/services/paymentService.js`

**What it does:**

* Combines the PayHere merchant ID, order ID, formatted currency, amount, and merchant secret hash.
* Generates the required uppercase MD5 checksum for payment processing.

**Contribution to the Project:**
Helps prevent client-side manipulation of payment information by allowing the payment gateway to verify that the payment details originated from the authorized backend.


### 3.2 Webhook IPN Signature Verification & Settlement

**File:** `backend/services/paymentService.js`

**What it does:**

1. Validates the authenticity of incoming PayHere IPN/webhook notifications using MD5 hashes generated with the configured merchant secret.
2. Processes payment updates using an atomic MySQL transaction.
3. Synchronizes payment, appointment, and invoice statuses.
4. Rolls back the transaction if an update fails.
5. Sends a payment confirmation email after successful processing.

**Contribution to the Project:**
Provides reliable server-side payment confirmation and keeps appointment, payment, and invoice records synchronized even when a user does not return to the application after completing payment.


## Technologies Used

* Node.js
* Express.js
* MySQL
* JSON Web Tokens (JWT)
* PayHere Payment Gateway
* REST APIs
* bcrypt
* JavaScript

## Contribution Summary

As the **Second Backend Developer**, my contribution focused primarily on:

* Authentication and session security
* JWT verification and session invalidation
* Login brute-force protection
* Role-Based Access Control
* Protected API routes
* PayHere payment integration
* Payment webhook/IPN verification
* Transaction-based payment synchronization

> **Note:** PrimeHeal is a group project. This document describes my specific backend contributions and does not claim ownership of the complete application.
