 1. User Authentication

# API Endpoints
Method	Endpoint	Description
POST	/api/register	Register a new user
POST	/api/login	Authenticate user and return token
GET	/api/profile	Retrieve user profile
PUT	/api/profile	Update user profile

## Input Specifications
Registration:

{
  "email": "user@example.com",
  "password": "P@ssw0rd123",
  "role": "host",
  "full_name": "John Doe"
}
- Login:
{
  "email": "user@example.com",
  "password": "P@ssw0rd123"
}
## Output Specifications
- Login Success:
{
  "token": "jwt-token-here",
  "user": {
    "id": 1,
    "email": "user@example.com",
    "role": "host",
    "full_name": "John Doe"
  }
}
- Profile Update Success:
{
  "message": "Profile updated successfully."
}
### Validation Rules
- Email must be unique and valid.
- Password must be at least 8 characters, including numbers and special characters.
- Role must be either guest or host.
- Full name is required.

### Performance Criteria
- Authentication response within 200ms.
- Password hashing using bcrypt or Argon2.
- Token expiration: 1 hour.

2. Property Management

# API Endpoints
Method	Endpoint	        Description

POST	/api/properties	     Create a new property listing
GET	    /api/properties	     Get all listings (with filters)
GET	    /api/properties/:id  Get details of a single property
PUT	    /api/properties/:id	 Update a listing
DELETE	/api/properties/:id	 Delete a listing

## Input Specifications
- Create Property:
{
  "title": "Cozy Studio",
  "description": "Near downtown, free parking",
  "location": "Lagos, Nigeria",
  "price_per_night": 50,
  "amenities": ["WiFi", "Air Conditioning"],
  "max_guests": 2,
  "availability": [
    {"start_date": "2025-05-01", "end_date": "2025-06-30"}
  ],
  "images": ["url1", "url2"]
}
## Output Specifications
- Success:

{
  "id": 12,
  "message": "Property created successfully"
}
### Validation Rules
- Title must be non-empty and max 100 chars.
- Price must be numeric and positive.
- Dates in availability must not overlap.
- At least one amenity must be provided.

### Performance Criteria
- Image uploads offloaded to Cloudinary or S3.
- Queryable via filters (location, price, etc.) with results cached (e.g., via Redis).
- Pagination with limit of 10–50 listings per request.

3. Booking System

# API Endpoints
Method	Endpoint	               Description

POST	/api/bookings	           Create a booking
GET	    /api/bookings	           View user bookings
PUT	    /api/bookings/:id/cancel   Cancel a booking

## Input Specifications
- Create Booking:

{
  "property_id": 12,
  "check_in": "2025-06-10",
  "check_out": "2025-06-15",
  "guests": 2
}
## Output Specifications
- Booking Created:
{
  "booking_id": 88,
  "status": "pending",
  "message": "Booking request submitted."
}
### Validation Rules
- Check-in date must be before check-out.
- Booking must not overlap with existing confirmed bookings.
- Guests count must not exceed property max_guests.

### Performance Criteria
- Date validation performed server-side within 100ms.
- Use transaction locks or row-level locking to avoid double bookings.
- Status transitions must be auditable: pending → confirmed → completed/cancelled.

