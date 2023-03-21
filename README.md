
# Mobile Repair Company API Endpoints

Sample API Endpoints for GoFix. These endpoints will allow you to send and verify OTPs, retrieve mobile companies, mobile phone models, services available for each phone, book services on specific dates and times, save courier details, and get a list of user orders. This is only a sample list and can be modified as necessary.

## 1. Send OTP (POST)

Send a One-Time Password (OTP) to the user's phone number for authentication purposes.

```
POST /api/v1/send-otp
```

**Request Body:**
```json
{
  "phone_number": "1234567890"
}
```

**Sample Success Response:**
```json
{
  "status": "success",
  "message": "OTP sent successfully"
}
```

**Sample Failure Response:**
```json
{
  "status": "error",
  "message": "Failed to send OTP"
}
```

## 2. Verify OTP (POST)

Verify the OTP provided by the user to complete authentication.

```
POST /api/v1/verify-otp
```

**Request Body:**
```json
{
  "phone_number": "1234567890",
  "otp": "123456"
}
```

**Sample Success Response:**
```json
{
  "status": "success",
  "message": "OTP verified successfully",
  "user_id": "123"
}
```

**Sample Failure Response:**
```json
{
  "status": "error",
  "message": "Invalid OTP"
}
```

## 3. List of Mobile Companies (GET)

Retrieve a list of all mobile companies.

```
GET /api/v1/mobile-companies
```

**Sample Success Response:**
```json
{
  "status": "success",
  "companies": [
    {
      "id": "1",
      "name": "Apple"
    },
    {
      "id": "2",
      "name": "Samsung"
    }
  ]
}
```

**Sample Failure Response:**
```json
{
  "status": "error",
  "message": "Failed to fetch mobile companies"
}
```

## 4. List of Mobile Phones in the Company (GET)

Retrieve a list of mobile phone models for a specific company.

```
GET /api/v1/mobile-companies/:company_id/phones
```

**Path Parameters:**
- `company_id`: The unique identifier of the mobile company.

**Sample Success Response:**
```json
{
  "status": "success",
  "phones": [
    {
      "id": "1",
      "name": "iPhone 12"
    },
    {
      "id": "2",
      "name": "iPhone 13"
    }
  ]
}
```

**Sample Failure Response:**
```json
{
  "status": "error",
  "message": "Failed to fetch mobile phones for the company"
}
```


## 5. List of Services Available for the Phone (GET)

Retrieve a list of services available for a specific phone model.

```
GET /api/v1/mobile-phones/:phone_id/services
```

**Path Parameters:**
- `phone_id`: The unique identifier of the mobile phone.

**Sample Success Response:**
```json
{
  "status": "success",
  "data": [
    {
      "id": "1",
      "name": "Screen Replacement",
      "price": "100"
    },
    {
      "id": "2",
      "name": "Battery Replacement",
      "price": "50"
    }
  ]
}
```

**Sample Failure Response:**
```json
{
  "status": "error",
  "message": "Phone not found"
}
```

## 6. Book the Service on a Date and Time (POST)

Book a specific service for a mobile phone on a chosen date and time.

```
POST /api/v1/book-service
```

**Request Body:**
```json
{
  "user_id": "123",
  "phone_id": "456",
  "service_id": "789",
  "date": "2023-04-05",
  "time": "14:00"
}
```

**Sample Success Response:**
```json
{
  "status": "success",
  "message": "Service booked successfully",
  "data": {
    "booking_id": "1"
  }
}
```

**Sample Failure Response:**
```json
{
  "status": "error",
  "message": "Unable to book the service"
}
```

## 7. Save Courier Details (POST)

Save the courier details for a user sending their mobile phone.

```
POST /api/v1/courier-details
```

**Request Body:**
```json
{
  "user_id": "123",
  "company_name": "Courier Company",
  "tracking_number": "XYZ123456789"
}
```

**Sample Success Response:**
```json
{
  "status": "success",
  "message": "Courier details saved successfully",
  "data": {
    "courier_id": "1"
  }
}
```

**Sample Failure Response:**
```json
{
  "status": "error",
  "message": "Unable to save courier details"
}
```

## 8. Get User Orders (GET)

Retrieve a list of the user's orders with their order details.

```
GET /api/v1/users/:user_id/orders
```

**Path Parameters:**
- `user_id`: The unique identifier of the user.

**Sample Success Response:**
```json
{
  "status": "success",
  "data": [
    {
      "order_id": "1",
      "phone_id": "456",
      "service_id": "789",
      "date": "2023-04-05",
      "time": "14:00",
      "status": "Booked"
    },
    {
      "order_id": "2",
      "phone_id": "123",
      "service_id": "456",
      "date": "2023-04-10",
      "time": "10:00",
      "status": "Completed"
    }
  ]
}
```

**Sample Failure Response:**
```json
{
  "status": "error",
  "message": "Unable to fetch user orders"
}
```

## 9. Fetch Order Details (GET)

Retrieve the order details for a specific order using the order ID.

```
GET /api/v1/orders/:order_id
```

**Path Parameters:**
- `order_id`: The unique identifier of the order.

**Sample Success Response:**
```json
{
  "status": "success",
  "data": {
    "order_id": "123",
    "user_id": "456",
    "phone_id": "789",
    "service_id": "012",
    "date": "2023-04-05",
    "time": "14:00",
    "status": "Confirmed",
    "courier_details": {
      "courier_company": "DHL",
      "tracking_number": "TRACK12345"
    },
    "total_cost": 99.99
  }
}
```

**Sample Failure Response:**
```json
{
  "status": "error",
  "message": "Order not found"
}
```
