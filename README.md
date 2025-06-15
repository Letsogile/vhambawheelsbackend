# Vhamba Wheels Backend API Documentation

## Overview
This document provides information on how to set up and use the Vhamba Wheels backend API, which supports the vehicle leasing platform frontend.

## Setup Instructions

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (local or Atlas)

### Installation
1. Clone the repository
2. Navigate to the project directory
3. Install dependencies:
   ```
   npm install
   ```
4. Create a `.env` file in the root directory with the following variables:
   ```
   NODE_ENV=development
   PORT=5000
   MONGO_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret
   JWT_EXPIRE=30d
   ```
5. Start the server:
   - Development mode: `npm run dev`
   - Production mode: `npm start`

## API Endpoints

### Authentication

#### Register User
- **URL**: `/api/auth/register`
- **Method**: `POST`
- **Body**:
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "phone": "+27123456789",
    "password": "password123"
  }
  ```
- **Response**: JWT token

#### Login User
- **URL**: `/api/auth/login`
- **Method**: `POST`
- **Body**:
  ```json
  {
    "email": "john@example.com",
    "password": "password123"
  }
  ```
- **Response**: JWT token

#### Get Current User
- **URL**: `/api/auth/me`
- **Method**: `GET`
- **Headers**: `Authorization: Bearer <token>`
- **Response**: User data

#### Logout
- **URL**: `/api/auth/logout`
- **Method**: `GET`
- **Headers**: `Authorization: Bearer <token>`

### Vehicles

#### Get All Vehicles
- **URL**: `/api/vehicles`
- **Method**: `GET`
- **Query Parameters**:
  - `class`: Filter by vehicle class (economy, premium, suv)
  - `sort`: Sort field(s)
  - `page`: Page number
  - `limit`: Results per page
- **Response**: List of vehicles

#### Get Single Vehicle
- **URL**: `/api/vehicles/:id`
- **Method**: `GET`
- **Response**: Vehicle details

#### Create Vehicle (Admin only)
- **URL**: `/api/vehicles`
- **Method**: `POST`
- **Headers**: `Authorization: Bearer <token>`
- **Body**:
  ```json
  {
    "name": "Toyota Corolla Quest",
    "class": "economy",
    "dailyRate": 350,
    "fuelType": "Petrol",
    "transmission": "Manual",
    "seats": 5,
    "imageUrl": "https://example.com/corolla.jpg",
    "available": true
  }
  ```
- **Response**: Created vehicle

#### Update Vehicle (Admin only)
- **URL**: `/api/vehicles/:id`
- **Method**: `PUT`
- **Headers**: `Authorization: Bearer <token>`
- **Body**: Fields to update
- **Response**: Updated vehicle

#### Delete Vehicle (Admin only)
- **URL**: `/api/vehicles/:id`
- **Method**: `DELETE`
- **Headers**: `Authorization: Bearer <token>`

### Locations

#### Get All Locations
- **URL**: `/api/locations`
- **Method**: `GET`
- **Response**: List of locations

#### Get Single Location
- **URL**: `/api/locations/:id`
- **Method**: `GET`
- **Response**: Location details

#### Create Location (Admin only)
- **URL**: `/api/locations`
- **Method**: `POST`
- **Headers**: `Authorization: Bearer <token>`
- **Body**:
  ```json
  {
    "name": "Pretoria Office",
    "address": "123 Church Street",
    "city": "Pretoria",
    "postalCode": "0002",
    "phone": "+27123456789",
    "email": "pretoria@vhambalogistics.co.za",
    "operatingHours": {
      "weekdays": "Monday - Friday: 7:00 AM - 7:00 PM",
      "saturday": "Saturday: 8:00 AM - 5:00 PM",
      "sunday": "Sunday: 9:00 AM - 4:00 PM"
    }
  }
  ```
- **Response**: Created location

#### Update Location (Admin only)
- **URL**: `/api/locations/:id`
- **Method**: `PUT`
- **Headers**: `Authorization: Bearer <token>`
- **Body**: Fields to update
- **Response**: Updated location

#### Delete Location (Admin only)
- **URL**: `/api/locations/:id`
- **Method**: `DELETE`
- **Headers**: `Authorization: Bearer <token>`

### Lease Inquiries

#### Submit Lease Inquiry
- **URL**: `/api/lease-inquiries`
- **Method**: `POST`
- **Body**:
  ```json
  {
    "location": "location_id",
    "startDate": "2025-06-01",
    "leasePeriod": "3 Months"
  }
  ```
- **Response**: Created inquiry

#### Get User's Lease Inquiries
- **URL**: `/api/lease-inquiries`
- **Method**: `GET`
- **Headers**: `Authorization: Bearer <token>`
- **Response**: List of user's inquiries

#### Get Specific Lease Inquiry
- **URL**: `/api/lease-inquiries/:id`
- **Method**: `GET`
- **Headers**: `Authorization: Bearer <token>`
- **Response**: Inquiry details

#### Update Lease Inquiry
- **URL**: `/api/lease-inquiries/:id`
- **Method**: `PUT`
- **Headers**: `Authorization: Bearer <token>`
- **Body**: Fields to update
- **Response**: Updated inquiry

#### Delete Lease Inquiry
- **URL**: `/api/lease-inquiries/:id`
- **Method**: `DELETE`
- **Headers**: `Authorization: Bearer <token>`

### Quote Requests

#### Submit Quote Request
- **URL**: `/api/quote-requests`
- **Method**: `POST`
- **Body**:
  ```json
  {
    "vehicle": "vehicle_id",
    "location": "location_id",
    "startDate": "2025-06-01",
    "leasePeriod": "3 Months"
  }
  ```
- **Response**: Created quote request

#### Get User's Quote Requests
- **URL**: `/api/quote-requests`
- **Method**: `GET`
- **Headers**: `Authorization: Bearer <token>`
- **Response**: List of user's quote requests

#### Get Specific Quote Request
- **URL**: `/api/quote-requests/:id`
- **Method**: `GET`
- **Headers**: `Authorization: Bearer <token>`
- **Response**: Quote request details

#### Update Quote Request
- **URL**: `/api/quote-requests/:id`
- **Method**: `PUT`
- **Headers**: `Authorization: Bearer <token>`
- **Body**: Fields to update
- **Response**: Updated quote request

#### Delete Quote Request
- **URL**: `/api/quote-requests/:id`
- **Method**: `DELETE`
- **Headers**: `Authorization: Bearer <token>`

### Contact Messages

#### Submit Contact Message
- **URL**: `/api/contact`
- **Method**: `POST`
- **Body**:
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "phone": "+27123456789",
    "location": "location_id",
    "message": "I'm interested in leasing a vehicle for my business."
  }
  ```
- **Response**: Created contact message

#### Get All Contact Messages (Admin only)
- **URL**: `/api/contact`
- **Method**: `GET`
- **Headers**: `Authorization: Bearer <token>`
- **Response**: List of contact messages

#### Get Specific Contact Message (Admin only)
- **URL**: `/api/contact/:id`
- **Method**: `GET`
- **Headers**: `Authorization: Bearer <token>`
- **Response**: Contact message details

#### Update Contact Message Status (Admin only)
- **URL**: `/api/contact/:id`
- **Method**: `PUT`
- **Headers**: `Authorization: Bearer <token>`
- **Body**:
  ```json
  {
    "status": "read"
  }
  ```
- **Response**: Updated contact message

#### Delete Contact Message (Admin only)
- **URL**: `/api/contact/:id`
- **Method**: `DELETE`
- **Headers**: `Authorization: Bearer <token>`

## Error Handling
All endpoints return standardized error responses:
```json
{
  "success": false,
  "error": "Error message"
}
```

## Authentication
Most endpoints require authentication using JWT tokens. Include the token in the Authorization header:
```
Authorization: Bearer <token>
```

## Integration with Frontend
This backend is designed to work seamlessly with the Vhamba Wheels frontend. The API endpoints match the frontend's data requirements and form submissions.
