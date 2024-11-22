# Airbnb Clone Backend - Requirements Specifications

## 1. User Authentication

### **Feature Description**
Enable users to securely register, log in, and manage their sessions. Includes role-based access for guests, hosts, and admins.

### **API Endpoints**
- **POST /api/auth/register**
  - **Input**:
    ```json
    {
      "email": "user@example.com",
      "password": "password123",
      "role": "guest" // or "host"
    }
    ```
  - **Output**:
    - **201 Created**:
      ```json
      {
        "message": "Registration successful",
        "userId": "12345"
      }
      ```
    - **400 Bad Request**:
      ```json
      {
        "error": "Email already exists"
      }
      ```

- **POST /api/auth/login**
  - **Input**:
    ```json
    {
      "email": "user@example.com",
      "password": "password123"
    }
    ```
  - **Output**:
    - **200 OK**:
      ```json
      {
        "token": "jwt-token",
        "role": "guest"
      }
      ```
    - **401 Unauthorized**:
      ```json
      {
        "error": "Invalid email or password"
      }
      ```

### **Validation Rules**
- Email must be in a valid format.
- Password must be at least 8 characters long, including numbers and symbols.
- Role must be either "guest" or "host."

### **Performance Criteria**
- Authentication response time must be under 500ms.
- Support up to 10,000 concurrent logins.
- Token expiration handled securely (e.g., 15 minutes for short-term tokens, refresh tokens for longer sessions).

---

## 2. Property Management

### **Feature Description**
Allow hosts to manage property listings, including creating, updating, and deleting properties.

### **API Endpoints**
- **POST /api/properties**
  - **Input**:
    ```json
    {
      "title": "Cozy Apartment",
      "description": "A comfortable and affordable apartment in the city center.",
      "location": "New York, NY",
      "price": 120.00,
      "amenities": ["Wi-Fi", "Air Conditioning", "Pet Friendly"],
      "images": ["image1.jpg", "image2.jpg"],
      "availability": {
        "startDate": "2024-12-01",
        "endDate": "2024-12-31"
      }
    }
    ```
  - **Output**:
    - **201 Created**:
      ```json
      {
        "message": "Property created successfully",
        "propertyId": "67890"
      }
      ```
    - **400 Bad Request**:
      ```json
      {
        "error": "Missing required fields"
      }
      ```

- **PUT /api/properties/{propertyId}**
  - **Input**:
    ```json
    {
      "title": "Updated Title",
      "price": 150.00
    }
    ```
  - **Output**:
    - **200 OK**:
      ```json
      {
        "message": "Property updated successfully"
      }
      ```
    - **404 Not Found**:
      ```json
      {
        "error": "Property not found"
      }
      ```

### **Validation Rules**
- **Title and description** must not exceed 255 characters.
- **Price:** must be a positive number.
- **Images:** Must be valid URLs or file paths.
- **Availability dates** must not overlap with existing bookings.

### **Performance Criteria**
- Property creation response time must be under 1 second for files ≤ 5MB.
- Support up to 50,000 property listings.

**DELETE /api/properties/:id**
   - **Input:** None
   - **Output:**
    - **200 OK**:
     ```json
     {
       "message": "Property deleted successfully"
     }
     ```

---

## 3. Booking System

### **Feature Description**
Allow guests to create, manage, and cancel bookings, ensuring date validation and status tracking.

### **API Endpoints**
- **POST /api/bookings**
  - **Input**:
    ```json
    {
      "propertyId": "67890",
      "guestId": "12345",
      "startDate": "2024-12-10",
      "endDate": "2024-12-15"
    }
    ```
  - **Output**:
    - **201 Created**:
      ```json
      {
        "message": "Booking created successfully",
        "bookingId": "abc123"
      }
      ```
    - **409 Conflict**:
      ```json
      {
        "error": "Dates are not available"
      }
      ```

- **DELETE /api/bookings/{bookingId}**
  - **Output**:
    - **200 OK**:
      ```json
      {
        "message": "Booking canceled successfully"
      }
      ```
    - **404 Not Found**:
      ```json
      {
        "error": "Booking not found"
      }
      ```

### **Validation Rules**
- **Date Validation:** 
  - `startDate` must be before `endDate`.
  - Dates must not overlap with existing bookings.
- **User and Property IDs:** Must exist in the database.

### **Performance Criteria**
- Booking response time must be under
- Ensure bookings are conflict-free by implementing locking mechanisms.

### General Notes
- All endpoints must return proper HTTP status codes (e.g., 200 for success, 400 for bad requests).
- Logs must capture errors and key actions for debugging.
- Data protection measures (e.g., encrypt sensitive data, implement rate-limiting to prevent abuse) are mandatory.
