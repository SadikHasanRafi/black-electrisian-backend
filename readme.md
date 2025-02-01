# Black Electrical API Documentation

## Base URL
`https://black-electrisian.onrender.com`

## Authentication
Most endpoints require authentication. Include the user's email in requests where applicable.

## API Endpoints

### Users

#### Register User
- **POST** `/users`
- Creates a new user account
- **Body**: User object with email and other details
- **Response**: Returns created user object

#### Update User
- **PUT** `/users`
- Updates existing user information
- **Body**: User object with email and updated fields
- **Response**: Returns update result

#### Get User Role
- **GET** `/users/:email`
- Checks if user is a buyer
- **Parameters**: email
- **Response**: `{ buyer: boolean }`

#### Check Doctor Status
- **GET** `/usersdatas/:email`
- Checks if user is a doctor
- **Parameters**: email
- **Response**: `{ doctor: boolean }`

### Admin Management

#### Make Admin
- **PUT** `/userLogin/admin`
- Promotes user to admin role
- **Body**: `{ email: string }`
- **Response**: Update result

#### Check Admin Status
- **GET** `/userLogin/:email`
- Verifies if user is an admin
- **Parameters**: email
- **Response**: `{ admin: boolean }`

### Products

#### Add Product (Buyer)
- **POST** `/PostUploadBuyer`
- Adds new product listing
- **Body**: Product details
- **Response**: Created product object

#### Add Product (Admin)
- **POST** `/PostUploadAdmin`
- Adds product to admin catalog
- **Body**: Product details
- **Response**: Created product object

#### Get Products
- **GET** `/products`
- Retrieves paginated product listings
- **Query Parameters**:
  - page: Page number
  - size: Items per page
- **Response**: `{ allData: Product[], count: number }`

#### Get Single Product
- **GET** `/product/:id`
- Retrieves specific product details
- **Parameters**: Product ID
- **Response**: Product object

### Electrician Services

#### Add Electrician
- **POST** `/electricianupload`
- Registers new electrician
- **Body**: Electrician details
- **Response**: Created electrician object

#### Book Electrician
- **POST** `/bookElectrician`
- Books an electrician service
- **Body**: Booking details
- **Response**: Booking confirmation

#### Get Electricians
- **GET** `/showElectrician`
- Lists all electricians
- **Response**: Array of electrician objects

### Payments

#### Initialize Payment
- **POST** `/init`
- Starts SSL Commerz payment process
- **Body**: 
  - total_amount
  - currency
  - customer details
- **Response**: Payment gateway URL

#### Payment Callbacks
- **POST** `/success`
- **POST** `/fail`
- **POST** `/cancel`
- SSL Commerz payment status endpoints
- **Response**: Redirects to appropriate frontend URL

#### Get Order
- **GET** `/orders/:tran_id`
- Retrieves order details by transaction ID
- **Parameters**: Transaction ID
- **Response**: Order object

### Blog/Content

#### Add Blog Post
- **POST** `/blogrobot`
- Creates new blog post
- **Body**: Blog content
- **Response**: Created blog object

#### Get Blog Posts
- **GET** `/showBlog`
- Retrieves all blog posts
- **Response**: Array of blog posts

### Contact Management

#### Submit Contact Form
- **POST** `/contactus`
- Submits contact form
- **Body**: Contact details
- **Response**: Submission confirmation

#### Get Contact Submissions
- **GET** `/contactus`
- Retrieves all contact form submissions
- **Response**: Array of contact submissions

## Error Handling
- All endpoints return appropriate HTTP status codes
- Failed requests include error message in response body

## Data Models

### User
```javascript
{
  email: string,
  client: string,  // 'buyer' | 'doctor'
  role?: string    // 'admin'
}
```

### Product
```javascript
{
  productName: string,
  ProductPrice: number,
  categories: string,
  description: string
}
```

### Order
```javascript
{
  tran_id: string,
  total_amount: number,
  currency: string,
  status: string,
  cus_email: string
}
```

## Rate Limiting
No explicit rate limiting implemented. Consider client-side throttling for intensive operations.

## Notes
- All dates should be sent in ISO format
- Monetary values should be in BDT (Bangladeshi Taka)
- File uploads supported for product images
- SSL Commerz integration for payment processing