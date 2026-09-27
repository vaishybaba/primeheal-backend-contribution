# PrimeHeal Hospital Management System – Backend Contribution

**Group Project | Backend Developer**

PrimeHeal is a full-stack Hospital Management System developed as a university group project to support hospital operations including patient management, appointments, doctor management, payments, and administrative workflows.

## My Role

**Backend Developer**

I contributed to the backend development, with a focus on authentication, authorization, security, and payment processing.

## My Contributions

### 1. Authentication & Security

* Implemented JWT-based authentication.
* Added `tokenVersion` tracking for session invalidation.
* Implemented token verification and account-status validation.
* Added login brute-force protection using failed-attempt tracking and rate limiting.

### 2. Role-Based Access Control

* Implemented role-based authorization middleware.
* Restricted backend routes according to user roles.
* Applied authorization rules to administrative and receptionist endpoints.

### 3. PayHere Payment Integration

* Implemented PayHere payment hash generation using MD5.
* Implemented payment callback/IPN signature verification.
* Processed payment notifications securely.
* Implemented transactional synchronization between payments, appointments, and invoices.

## Technologies

* Node.js
* Express.js
* MySQL
* JWT
* PayHere
* REST APIs

## Project Structure

The original PrimeHeal application contains multiple modules, including:

* Backend
* Frontend
* Admin dashboard
* Database
* AI-related components

This repository is a **portfolio showcase of my backend contribution** to the original group project.

> **Note:** PrimeHeal was developed as a university group project. This repository documents and showcases my individual contribution and does not claim ownership of the complete application.

## Original Group Repository

The complete group project is maintained separately in the original team repository.

## Disclaimer

This repository is intended for portfolio and documentation purposes to demonstrate my contribution to the PrimeHeal group project.
