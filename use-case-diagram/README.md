The Airbnb Clone backend provides server-side logic, data management, and secure API endpoints to support a rental marketplace similar to Airbnb. It supports multiple roles: Guests, Hosts, and Admins.

---

# Core Functionalities

1. User Management
- **Registration & Authentication**
  - Signup/Login via email and password
  - OAuth login (Google, Facebook)
  - JWT-based token authentication
- **Profile Management**
  - Edit user details
  - Upload profile photos
  - Manage preferences

2. Property Listings Management
- Add/edit/delete property listings (for hosts)
- Include title, description, location, price, amenities, availability

3. Search and Filtering
- Filter listings by:
  - Location, price range, guest count, amenities
- Support pagination for performance

4. Booking System
- Guests can book available properties
- Prevent double bookings via date validation
- Track booking status: `pending`, `confirmed`, `cancelled`, `completed`
- Allow cancellation by guests or hosts

5. Payment Integration
- Integration with Stripe or PayPal
- Handle guest payments and host payouts
- Support for multiple currencies

6. Reviews and Ratings
- Guests can leave reviews and rate properties
- Hosts can reply to reviews
- Reviews linked to bookings

7. Notifications
- Email and in-app notifications for:
  - Booking updates
  - Payment confirmations
  - Cancellations

8. Admin Dashboard
- Admins can manage:
  - Users, listings, bookings, reviews, payments
- Access system logs and monitor activity

---

## Technical Requirements

- **Database**: PostgreSQL / MySQL
- **API**: RESTful (GraphQL optional)
- **Authentication**: JWT & OAuth
- **File Storage**: Cloudinary / AWS S3
- **Email Service**: SendGrid / Mailgun
- **Error Handling**: Global error middleware
- **Role-Based Access Control**: Guests, Hosts, Admins

---

## Non-Functional Requirements

- **Scalability**: Modular codebase, support for horizontal scaling
- **Security**: 
  - Encrypted data storage
  - Rate limiting
  - Input validation
- **Performance Optimization**:
  - Redis caching
  - Optimized DB queries
- **Testing**:
  - Unit and integration testing with `pytest`
  - Automated API testing

## Tech Stack

- **Backend**: Python, Django REST Framework
- **Database**: PostgreSQL
- **Authentication**: JWT, OAuth2
- **Cloud Storage**: AWS S3 / Cloudinary
- **Notifications**: SendGrid / Mailgun
- **Payments**: Stripe / PayPal
- **Testing**: Pytest, Postman
