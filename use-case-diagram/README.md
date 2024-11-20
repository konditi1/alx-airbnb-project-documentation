# **Airbnb Clone Backend - Project Requirements**

## **📖 Overview**  
This project focuses on the backend architecture of an Airbnb clone, emphasizing key features like user management, property listings, booking system, and secure payments. The system ensures scalability, security, and efficient performance.

---

## **👥 Actors**  

- **Guest**  
  A user who books properties.

- **Host**  
  A user who lists properties.

- **Admin**  
  Manages the platform, monitors activities, and resolves disputes.

- **System**  
  Represents the backend server handling logic and third-party integrations.

---

## **💡 Use Cases**

### **1. User Registration/Login**
- Guests and hosts can sign up or log in using email and password.  
- Supports OAuth login options (e.g., Google, Facebook).  

### **2. Profile Management**
- Users can update profiles, including photos and contact details.  

### **3. Property Management (Host)**
- Add, edit, or delete property listings.  
- Upload property images to enhance listings.  

### **4. Search and Filtering (Guest)**
- Search properties based on:  
  - Location  
  - Price range  
  - Number of guests  
  - Amenities (e.g., Wi-Fi, pool, pet-friendly)  
- Pagination support for managing large datasets efficiently.  

### **5. Booking Management**
- Guests can create bookings with date validation to prevent double bookings.  
- Booking statuses include pending, confirmed, canceled, or completed.  
- Cancellation options for guests and hosts based on platform policies.  

### **6. Payments**
- Secure processing of guest payments.  
- Automatic payouts to hosts after bookings.  
- Support for multiple currencies.  

### **7. Reviews and Ratings**
- Guests can leave reviews and ratings for properties.  
- Hosts have the ability to respond to reviews.  

### **8. Notifications**
- Email and in-app notifications for:  
  - Booking confirmations  
  - Payment updates  
  - Cancellations  

### **9. Admin Management**
- Admins monitor users, bookings, property listings, and payments.

---

## **🔗 Relationships**
- **Guests** and **Hosts** interact directly with the backend for their respective tasks.  
- **Admins** oversee and manage platform operations.  
- The **System** facilitates backend logic and integrates with third-party services for email, payments, and storage.
