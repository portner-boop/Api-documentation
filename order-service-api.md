# Order Service API Documentation

This document provides comprehensive documentation for both frontend developers and QA testers working with the Order Service API.

## API Endpoints
# Base : /api/v1/orders

### 1. Create a New Order
**Endpoint:** `POST /`

**Request Body:**
json
{
  "userId": "uuid-string",
  "spaceId": 1,
  "floorId": 1,
  "startTime": "2023-12-31T10:00:00",
  "timeZone": "Europe/Moscow",
  "durationHours": 2
}
Required Fields:

userId - must be a valid UUID

spaceId - must be a positive number

floorId - must be a positive number

startTime - must be in future or present

durationHours - minimum 1 hour

Success Response (201 Created):

json
{
  "id": 1,
  "userId": "uuid-string",
  "spaceId": 1,
  "floorId": 1,
  "startTime": "2023-12-31T10:00:00",
  "endTime": "2023-12-31T12:00:00",
  "status": "CONFIRMED",
  "createdAt": "2023-12-30T15:30:00",
  "updatedAt": "2023-12-30T15:30:00"
}
2. Get Order by ID
Endpoint: GET /{id}

Path Parameters:

id - order ID (long)

Success Response (200 OK):

json
{
  "id": 1,
  "userId": "uuid-string",
  "spaceId": 1,
  "floorId": 1,
  "startTime": "2023-12-31T10:00:00",
  "endTime": "2023-12-31T12:00:00",
  "status": "CONFIRMED",
  "createdAt": "2023-12-30T15:30:00",
  "updatedAt": "2023-12-30T15:30:00"
}
3. Get Orders by User ID
Endpoint: GET /user/{userId}

Path Parameters:

userId - user UUID

Success Response (200 OK):

json
[
  {
    "id": 1,
    "userId": "uuid-string",
    "spaceId": 1,
    "floorId": 1,
    "startTime": "2023-12-31T10:00:00",
    "endTime": "2023-12-31T12:00:00",
    "status": "CONFIRMED",
    "createdAt": "2023-12-30T15:30:00",
    "updatedAt": "2023-12-30T15:30:00"
  }
]
4. Update Order Status
Endpoint: PATCH /{id}

Path Parameters:

id - order ID (long)

Request Body:

json
{
  "status": "CANCELLED"
}
Success Response (200 OK):

json
{
  "id": 1,
  "userId": "uuid-string",
  "spaceId": 1,
  "floorId": 1,
  "startTime": "2023-12-31T10:00:00",
  "endTime": "2023-12-31T12:00:00",
  "status": "CANCELLED",
  "createdAt": "2023-12-30T15:30:00",
  "updatedAt": "2023-12-30T15:35:00"
}
5. Delete Order
Endpoint: DELETE /{id}

Path Parameters:

id - order ID (long)

Success Response: 204 No Content

6. Get All Orders (with filters)
Endpoint: GET /

Query Parameters:

includeConfirmed - boolean (default: false)

includeCanceled - boolean (default: false)

includeCompleted - boolean (default: false)

Success Response (200 OK):

json
[
  {
    "id": 1,
    "userId": "uuid-string",
    "spaceId": 1,
    "floorId": 1,
    "startTime": "2023-12-31T10:00:00",
    "endTime": "2023-12-31T12:00:00",
    "status": "CONFIRMED",
    "createdAt": "2023-12-30T15:30:00",
    "updatedAt": "2023-12-30T15:30:00"
  }
]
Order Status Flow
New orders are created with CONFIRMED status

Can be changed to:

CANCELLED - order was cancelled

COMPLETED - order was fulfilled
