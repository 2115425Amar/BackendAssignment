# API Testing with Postman

This README provides instructions for testing the API endpoints using Postman.

To test the API endpoints in Postman with the admin access, follow these steps:

### 1. **Authenticate as Admin**

#### **Endpoint:**
`POST /api/v1/auth/login`

#### **Request Body:**
```json
{
  "email": "admin@admin.com",
  "password": "12345"
}
```

#### **Steps:**
1. Open Postman.
2. Set the request method to `POST`.
3. Enter the URL: `http://localhost:8080/api/v1/auth/login`.
4. Go to the `Body` tab, select `raw`, and choose `JSON` format.
5. Paste the above JSON into the request body.
6. Click `Send`.

#### **Response:**
You should receive a response with a JWT token if the login is successful.

```json
{
  "success": true,
  "message": "login successfully",
  "user": {
    "_id": "user_id_here",
    "name": "Admin Name",
    "email": "admin@admin.com",
    "phone": "1234567890",
    "address": "Admin Address",
    "role": 1
  },
  "token": "your_jwt_token_here"
}
```

### 2. **Test Protected Admin Routes**

#### **Example Endpoint:**
`GET /api/v1/auth/admin-auth`

#### **Request Headers:**
Add the `Authorization` header with the value `Bearer <your_jwt_token_here>`.

#### **Steps:**
1. Copy the JWT token received from the login response.
2. Open a new request in Postman.
3. Set the request method to `GET`.
4. Enter the URL: `http://localhost:8080/api/v1/auth/admin-auth`.
5. Go to the `Headers` tab and add the `Authorization` header with the value `Bearer <your_jwt_token_here>`.
6. Click `Send`.

#### **Response:**
If the token is valid and the user has admin privileges, you should receive:
```json
{
  "ok": true
}
```

### **Testing Other Admin Endpoints**

You can follow a similar approach for other endpoints that require admin access. Just ensure you:

1. Include the `Authorization` header with the `Bearer <your_jwt_token_here>` value.
2. Use the appropriate HTTP method (GET, POST, PUT, DELETE) and URL as required by the endpoint you are testing.

#### **Example Endpoint:**
`POST /api/v1/category/create-category`

#### **Request Body:**
```json
{
  "name": "New Category"
}
```

#### **Steps:**
1. Open a new request in Postman.
2. Set the request method to `POST`.
3. Enter the URL: `http://localhost:8080/api/v1/category/create-category`.
4. Go to the `Headers` tab and add the `Authorization` header with the value `Bearer <your_jwt_token_here>`.
5. Go to the `Body` tab, select `raw`, and choose `JSON` format.
6. Paste the above JSON into the request body.
7. Click `Send`.

#### **Response:**
If the request is successful, you should get a response like:
```json
{
  "success": true,
  "message": "new category created",
  "category": {
    "_id": "category_id_here",
    "name": "New Category",
    "slug": "new-category"
  }
}
```

### 2. **Authenticate as User**

## Base URL
The base URL for all API endpoints is:

```
http://localhost:8080/api/v1
```

Replace `localhost:8080` with the appropriate host and port if different.

## Authentication

### Register
**Endpoint:** `/api/v1/auth/register`  
**Method:** POST  
**Body:**
```json
{
  "name": "string",
  "email": "string",
  "password": "string",
  "phone": "string",
  "address": "string",
  "answer": "string"
}
```

### Login
**Endpoint:** `/api/v1/auth/login`  
**Method:** POST  
**Body:**
```json
{
  "email": "string",
  "password": "string"
}
```

**Success Response:**
```json
{
  "success": true,
  "message": "login successfully",
  "user": {
    "_id": "string",
    "name": "string",
    "email": "string",
    "phone": "string",
    "address": "string",
    "role": "number"
  },
  "token": "string"
}
```

**Failure Response:**
```json
{
  "success": false,
  "message": "Invalid email or password"
}
```

### Forgot Password
**Endpoint:** `/api/v1/auth/forgot-password`  
**Method:** POST  
**Body:**
```json
{
  "email": "string",
  "answer": "string",
  "newPassword": "string"
}
```

**Success Response:**
```json
{
  "success": true,
  "message": "Password Reset Successfully"
}
```

## Endpoints

### Auth Routes

#### Register
**Endpoint:** `/api/v1/auth/register`  
**Method:** POST  
**Body:** See [Authentication Register](#register)

#### Login
**Endpoint:** `/api/v1/auth/login`  
**Method:** POST  
**Body:** See [Authentication Login](#login)

#### Forgot Password
**Endpoint:** `/api/v1/auth/forgot-password`  
**Method:** POST  
**Body:** See [Authentication Forgot Password](#forgot-password)

#### Test Route (Protected)
**Endpoint:** `/api/v1/auth/test`  
**Method:** GET  
**Headers:** `Authorization: Bearer <token>`  
**Success Response:**
```json
"Protected Routes"
```

#### Update Profile
**Endpoint:** `/api/v1/auth/profile`  
**Method:** PUT  
**Headers:** `Authorization: Bearer <token>`  
**Body:**
```json
{
  "name": "string",
  "email": "string",
  "password": "string",
  "address": "string",
  "phone": "string"
}
```

### Category Routes

#### Create Category
**Endpoint:** `/api/v1/category/create-category`  
**Method:** POST  
**Headers:** `Authorization: Bearer <token>`  
**Body:**
```json
{
  "name": "string"
}
```

#### Update Category
**Endpoint:** `/api/v1/category/update-category/:id`  
**Method:** PUT  
**Headers:** `Authorization: Bearer <token>`  
**Body:**
```json
{
  "name": "string"
}
```

#### Get All Categories
**Endpoint:** `/api/v1/category/get-category`  
**Method:** GET  

#### Get Single Category
**Endpoint:** `/api/v1/category/single-category/:slug`  
**Method:** GET  

#### Delete Category
**Endpoint:** `/api/v1/category/delete-category/:id`  
**Method:** DELETE  
**Headers:** `Authorization: Bearer <token>`

### Product Routes

#### Create Product
**Endpoint:** `/api/v1/product/create-product`  
**Method:** POST  
**Headers:** `Authorization: Bearer <token>`  
**Body:** Form-data including:
- `name` (string)
- `description` (string)
- `price` (number)
- `category` (string or ObjectId)
- `quantity` (number)
- `shipping` (boolean)
- `photo` (file)

#### Update Product
**Endpoint:** `/api/v1/product/update-product/:pid`  
**Method:** PUT  
**Headers:** `Authorization: Bearer <token>`  
**Body:** Form-data including:
- `name` (string)
- `description` (string)
- `price` (number)
- `category` (string or ObjectId)
- `quantity` (number)
- `shipping` (boolean)
- `photo` (file)

#### Get All Products
**Endpoint:** `/api/v1/product/get-product`  
**Method:** GET  

#### Get Single Product
**Endpoint:** `/api/v1/product/get-product/:slug`  
**Method:** GET  

#### Get Product Photo
**Endpoint:** `/api/v1/product/product-photo/:pid`  
**Method:** GET  

#### Delete Product
**Endpoint:** `/api/v1/product/delete-product/:pid`  
**Method:** DELETE  
**Headers:** `Authorization: Bearer <token>`



#### Product Count
**Endpoint:** `/api/v1/product/product-count`  
**Method:** GET  

#### Product List
**Endpoint:** `/api/v1/product/product-list/:page`  
**Method:** GET  

#### Search Products
**Endpoint:** `/api/v1/product/search/:keyword`  
**Method:** GET  

#### Related Products
**Endpoint:** `/api/v1/product/related-product/:pid/:cid`  
**Method:** GET  

#### Product by Category
**Endpoint:** `/api/v1/product/product-category/:slug`  
**Method:** GET  


## Notes
- Ensure that your server is running before testing.
- Use valid tokens for protected routes.
- Validate your input data according to the schema.
---


## Notes 
-Created By Amar Gupta