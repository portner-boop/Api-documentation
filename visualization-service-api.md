# Visualization Service API Documentation

This document provides comprehensive documentation for both frontend developers and QA testers working with the Floor Visualization Service API.


## API Endpoints

### 1. Upload Floor Visualization
**Endpoint:** `POST /{floorId}/upload`

**Content-Type:** `multipart/form-data`

**Path Parameters:**
- `floorId` - ID of the floor to visualize (long)

**Form Data:**
1. `file` - Image file of the floor plan (PNG/JPEG)
2. `places` - JSON array of space coordinates (see example below)

**Example places data:**
```json
[
  {
    "spaceId": 1,
    "x": 100,
    "y": 200
  },
  {
    "spaceId": 2,
    "x": 150,
    "y": 250
  }
]

**Success Response (200 OK):**

json

"Floor uploaded successfully: filename.jpg"

**Error Responses:**

- 400 Bad Request with error message if upload fails
    

### 2. Get Floor Visualization

**Endpoint:** `GET /{floorId}`

**Path Parameters:**

- `floorId` - ID of the floor to retrieve (long)
    

**Success Response (200 OK):**

json

{
  "imageUrl": "https://storage.example.com/floors/floor1.jpg",
  "places": [
    {
      "spaceId": 1,
      "x": 100,
      "y": 200
    },
    {
      "spaceId": 2,
      "x": 150,
      "y": 250
    }
  ]
}

**Error Responses:**

- 400 Bad Request if floor not found
    

## Data Models

### SpaceDto

json

{
  "spaceId": 1,
  "x": 100,
  "y": 200
}

- `spaceId`: Required, unique identifier for the space
    
- `x`: X-coordinate on the floor plan image
    
- `y`: Y-coordinate on the floor plan image
    

### FloorResponseDto

json

{
  "imageUrl": "string",
  "places": [
    // array of SpaceDto
  ]
}

- `imageUrl`: URL to access the floor plan image
    
- `places`: Array of spaces with their coordinates