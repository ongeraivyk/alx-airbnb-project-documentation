# Backend Requirement Specifications

## 1. User Authentication
### Endpoints
- POST /api/auth/register
  - Input: { "email": string, "password": string, "name": string }
  - Output: { "id": int, "email": string, "token": string }
  - Validation: email required, valid format; password min 8 chars.
- POST /api/auth/login
  - Input: { "email", "password" }
  - Output: { "token", "user" }

### Performance
- Registration request must respond within 2 seconds under normal load.

## 2. Property Management
### Endpoints
- POST /api/properties
  - Input: { "title", "description", "price", "location", "images": [] }
  - Output: created property object
  - Validation: title, price, location required.

- GET /api/properties
  - Query params: location, min_price, max_price, start_date, end_date
  - Output: list of property objects.

## 3. Booking System
### Endpoints
- POST /api/bookings
  - Input: { "property_id", "user_id", "start_date", "end_date", "guest_count" }
  - Output: booking object
  - Validation: dates must be valid and available.

- DELETE /api/bookings/:id
  - Cancels booking if allowed by policy.

## 4. Payments
### Endpoints
- POST /api/payments/charge
  - Input: { "booking_id", "payment_method", "amount" }
  - Output: payment confirmation object
  - Use external payment gateway; store payment id and status.

### Security
- All payment endpoints must use HTTPS.
- Tokens must be stored securely and expire after a configured time.

