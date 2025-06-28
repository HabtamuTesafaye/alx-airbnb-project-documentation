# 🏡 Airbnb Clone – Backend Requirements Specification

---

## 📌 1. User Authentication System

### ✅ Functional Requirements
- Users can register with **email/password** or **OAuth providers** (Google, Facebook)
- Users can **log in** and receive a **JWT token**
- Users can **reset forgotten passwords**
- Email verification is required for new accounts
- **Role-based access control**: Guest, Host, Admin

### ⚙️ Technical Specifications

#### 🔗 API Endpoints

| Method | Endpoint             | Description                     |
|--------|----------------------|---------------------------------|
| POST   | `/api/auth/register`   | Register a new user              |
| POST   | `/api/auth/login`      | Log in a user                    |
| POST   | `/api/auth/verify`     | Verify user email address        |
| POST   | `/api/auth/forgot-pwd` | Request password reset link      |
| POST   | `/api/auth/reset-pwd`  | Reset the user’s password        |

#### 📥 Input / 📤 Output

**`POST /api/auth/register`**

```json
// Request
{
  "email": "user@example.com",
  "password": "SecurePass123!",
  "user_type": "guest",
  "name": "John Doe"
}

// Response (Success)
{
  "status": "success",
  "message": "Verification email sent",
  "data": {
    "user_id": "usr_12345"
  }
}
````

#### 🔐 Validation Rules

* **Email**: Valid format & must be unique
* **Password**: Minimum 8 characters, 1 uppercase, 1 number, 1 special character
* **Name**: 2–50 characters

#### 🚀 Performance Criteria

* Registration: < **500ms**
* Authentication: < **300ms**
* Support: **100 concurrent auth requests/sec**

---

## 🏘️ 2. Property Management System

### ✅ Functional Requirements

* Hosts can **create/update/delete** listings
* Guests can **search and view** properties
* Property **availability calendar**
* Image upload for listings
* **Location-based search** with filters

### ⚙️ Technical Specifications

#### 🔗 API Endpoints

| Method | Endpoint                    | Description                   |
| ------ | --------------------------- | ----------------------------- |
| POST   | `/api/properties`           | Create a new property listing |
| PUT    | `/api/properties/:id`       | Update existing property      |
| DELETE | `/api/properties/:id`       | Delete a property             |
| GET    | `/api/properties`           | Search/list properties        |
| GET    | `/api/properties/:id`       | Get property details          |
| POST   | `/api/properties/:id/media` | Upload images for a property  |

#### 📥 Input / 📤 Output

**`POST /api/properties`**

```json
// Request
{
  "title": "Beachfront Villa",
  "description": "Luxury villa with ocean view...",
  "location": {
    "address": "123 Coastal Rd",
    "city": "Malibu",
    "country": "USA",
    "coordinates": [34.0259, -118.7798]
  },
  "price_per_night": 350,
  "bedrooms": 3,
  "amenities": ["wifi", "pool", "kitchen"],
  "availability": ["2023-11-01", "2023-11-15"]
}

// Response
{
  "status": "success",
  "data": {
    "property_id": "prop_67890",
    "created_at": "2023-10-08T12:00:00Z"
  }
}
```

#### 🧪 Validation Rules

* **Title**: 5–100 characters
* **Description**: 20–2000 characters
* **Price**: > \$10/night
* **Coordinates**: Valid latitude/longitude
* **Availability Dates**: Must be future dates

#### 🚀 Performance Criteria

* Property search: < **1s** with **10,000+** listings
* Support **50 concurrent image uploads**
* **500 property views/sec**

---

## 📅 3. Booking Management System

### ✅ Functional Requirements

* Guests can **book** available properties
* Hosts can **accept/reject** bookings
* Automatic **booking confirmation emails**
* Integrated **payment processing**
* **Cancellation** handling based on policies

### ⚙️ Technical Specifications

#### 🔗 API Endpoints

| Method | Endpoint                    | Description                 |
| ------ | --------------------------- | --------------------------- |
| POST   | `/api/bookings`             | Create a new booking        |
| GET    | `/api/bookings/:id`         | Retrieve booking details    |
| PATCH  | `/api/bookings/:id/status`  | Update booking status       |
| GET    | `/api/users/:id/bookings`   | Fetch bookings by user      |
| POST   | `/api/bookings/:id/payment` | Process payment for booking |

#### 📥 Input / 📤 Output

**`POST /api/bookings`**

```json
// Request
{
  "property_id": "prop_67890",
  "check_in": "2023-12-01",
  "check_out": "2023-12-07",
  "guests": 2,
  "payment_method": "card_12345"
}

// Response
{
  "status": "success",
  "data": {
    "booking_id": "book_24680",
    "total_amount": 2450,
    "currency": "USD",
    "confirmation_code": "ABX123"
  }
}
```

#### 🧪 Validation Rules

* **Dates**: Must be valid, non-overlapping, and within a 1–365 day range
* **Guests**: Within the allowed property capacity
* **Payment Method**: Must be a valid saved method
* **Booking Conflicts**: Must not overlap with existing confirmed bookings

#### 🚀 Performance Criteria

* Booking confirmation: < **1s**
* Payment completion: < **2s**
* Handle **50 concurrent bookings/min**
* **99.9% reliability** on confirmation success

---

## 🧰 General Technical Requirements

### 🗃️ Database

* **PostgreSQL** with proper indexing
* Use **PostGIS** for spatial queries
* Core tables:

  * `users`
  * `properties`
  * `bookings`
  * `payments`
  * `reviews`

### 🔒 Security

* All APIs are **JWT-protected**
* Passwords stored using **bcrypt hashing**
* Rate limiting on auth-related endpoints
* Input sanitization & validation at all layers

### ⚠️ Error Handling

**Standardized error format:**

```json
{
  "status": "error",
  "code": "ERR_400",
  "message": "Validation failed",
  "details": {
    "email": "Invalid email format"
  }
}
```

