1. User Authentication
    Enable users to register, log in, and manage their authentication details in a secured way.

    Users can register using email, first name, last name and password.
    Users can also login via OAuth (Google, apple etc).
    JWT-based authentication.
    
    API Endpoints:
    POST /auth/register
        User Input:
            {
            "email": "ray@alx.com",
            "password": "password",
            "name": "Raymond Frimpong"
            }

        System Output:
            Success:
            {
            "message": "User registered successfully",
            "userId": "user_id" 
            }

            Error:
            {
            "error": "Email already exists"
            }

    POST /auth/login
        User Input:
            {
            "email": "ray@alx.com",
            "password": "password"
            }

        System Output:
            Success:
            {
            "token": "token(jwt)",
            "userId": "user-id"
            }

            Error:
            {
            "error": "Invalid credentials"
            }

    Validation Rules:
        Email must be valid and typed correctly.
        Password must be at least 8 characters long with one uppercase letter, one number, and one special character.
    
    Performance:
        Registration request should process in under 500ms.
        Tokens should expire after 24 hours.

2. Property Management
    Enable hosts to add, edit, and delete property listings.
    Hosts can add property details (title, description, location, price, availability).
    Hosts can update or delete existing property listings.

    API Endpoints:
    POST /properties
        User Input:
            {
            "title": "Large 2 bedroom suite",
            "description": "A cozy apartment for your getaways",
            "location": "Accra, Ghana",
            "price": 220,
            "availability": true
            }
        System Output:
            Success:
            {
            "message": "Property added successfully",
            "propertyId": "property-id"
            }
            Error:
            {
            "error": "Missing required fields"
            }

    PUT /properties/id
        User Input:
            {
            "price": 150,
            "availability": false
            }
        System Output:
            Success:
            {
            "message": "Property was updated successfully"
            }
            Error:
            {
            "error": "Property not found"
            }

    DELETE /properties/id
        System Output:
            Success:
            {
            "message": "Property was deleted successfully"
            }
            Error:
            {
            "error": "Property not found"
            }

    Validation Rules:
        Title must short and precise.
        Price must be a float.

    Performance Criteria:
        Operations should be fast.

3. Booking System
    Enable both guests and hosts to book properties and manage bookings.
    Guests can book a property for specific dates.
    Remove bookings for the same property.
    Enable cancelling of bookings by both hosts and guests.

    API Endpoints:
    POST /bookings

        User Input:
        {
        "propertyId": "property-id",
        "userId": "user-id",
        "startDate": "2024-01-01",
        "endDate": "2024-01-05"
        }
    System Output:
        Success:
        {
        "message": "Booking has been confirmed",
        "bookingId": "booking-id"
        }
        Error:
        {
        "error": "Property already booked for the selected dates"
        }

    DELETE /bookings/id

        System Output:
            Success:
            {
            "message": "Booking has been cancelled"
            }
            Error:
            {
            "error": "Booking not found"
            }

    GET /bookings
        System Output:
            Success:
            {
                "bookingId": "unique-booking-id",
                "propertyId": "unique-property-id",
                "startDate": "2024-01-01",
                "endDate": "2024-01-05",
                "status": "confirmed"
            }

    Validation Rules:
        Start date must be earlier than the end date.
        Make sure bookings for the same property on the same date are not allowed.
        Start date must not be previous days.

    Performance Criteria:
        Bookings should be confirmed quickly.
        Cancellation request be processed faster.