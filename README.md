# E-Commerce API with FastAPI and PostgreSQL

This is a RESTful API for an e-commerce platform built with **FastAPI** and **PostgreSQL**, offering essential functionalities such as user authentication, product catalog management, shopping cart, order processing, and payment handling.

## Features
- User registration and authentication
- Product catalog with categories and search
- Cart and wishlist management
- Order placement and payment integration
- Admin management for users and products

## Tech Stack
- **Backend Framework**: FastAPI
- **Database**: PostgreSQL
- **Authentication**: JSON Web Tokens (JWT)

## Getting Started

### Prerequisites
- Python 3.8+
- PostgreSQL

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/mridul404/ecommerce-api-design-fastapi.git
   cd ecommerce-fastapi
   ```

2. **Set up a virtual environment**
   ```bash
   python3 -m venv venv
   source venv/bin/activate   # On Windows, use `venv\Scripts\activate`
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**

   Create a `.env` file with your database and secret configurations:
   ```
   DATABASE_URL=postgresql://username:password@localhost:5432/ecommerce_db
   SECRET_KEY=your_secret_key
   ```

5. **Run database migrations**
   ```bash
   alembic upgrade head
   ```

6. **Start the FastAPI server**
   ```bash
   uvicorn main:app --reload
   ```

7. **Access the documentation**

   - Swagger UI: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
   - ReDoc: [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

## API Endpoints

| **Endpoint**                        | **Method** | **Description**                           | **Parameters**                    | **Auth Required** |
|-------------------------------------|------------|-------------------------------------------|-----------------------------------|--------------------|
| **User Management**                 |            |                                           |                                   |                    |
| `/api/v1/users/register`            | `POST`     | Register a new user                       | -                                 | No                 |
| `/api/v1/users/login`               | `POST`     | Log in an existing user                   | -                                 | No                 |
| `/api/v1/users/{userId}`            | `GET`      | Retrieve user profile                     | `userId`                          | Yes                |
| `/api/v1/users/{userId}`            | `PUT`      | Update user profile                       | `userId`, body data               | Yes                |
| `/api/v1/users/logout`              | `POST`     | Log out the current user                  | -                                 | Yes                |
| **Product Management**              |            |                                           |                                   |                    |
| `/api/v1/products`                  | `GET`      | Get all products                          | Query: `page`, `limit`, `sort`    | No                 |
| `/api/v1/products/{productId}`      | `GET`      | Get details of a single product           | `productId`                       | No                 |
| `/api/v1/products/search`           | `GET`      | Search products                           | Query: `query`, `category`, etc.  | No                 |
| `/api/v1/products/filter`           | `GET`      | Filter products                           | Query: `price`, `brand`, `rating` | No                 |
| **Category Management**             |            |                                           |                                   |                    |
| `/api/v1/categories`                | `GET`      | Get list of categories                    | -                                 | No                 |
| `/api/v1/categories/{categoryId}`   | `GET`      | Get details of a specific category        | `categoryId`                      | No                 |
| **Cart Management**                 |            |                                           |                                   |                    |
| `/api/v1/cart/add`                  | `POST`     | Add item to cart                          | Body data                         | Yes                |
| `/api/v1/cart`                      | `GET`      | Get cart items                            | -                                 | Yes                |
| `/api/v1/cart/{itemId}`             | `PUT`      | Update cart item                          | `itemId`, body data               | Yes                |
| `/api/v1/cart/clear`                | `DELETE`   | Clear all items in cart                   | -                                 | Yes                |
| **Wishlist**                        |            |                                           |                                   |                    |
| `/api/v1/wishlist/add`              | `POST`     | Add product to wishlist                   | Body data                         | Yes                |
| `/api/v1/wishlist`                  | `GET`      | Get all wishlist items                    | -                                 | Yes                |
| `/api/v1/wishlist/{productId}`      | `DELETE`   | Remove product from wishlist              | `productId`                       | Yes                |
| **Order Management**                |            |                                           |                                   |                    |
| `/api/v1/orders`                    | `POST`     | Place an order                            | Body data                         | Yes                |
| `/api/v1/orders/{orderId}`          | `GET`      | Get order details                         | `orderId`                         | Yes                |
| `/api/v1/orders/history`            | `GET`      | Get order history for user                | -                                 | Yes                |
| `/api/v1/orders/{orderId}/cancel`   | `POST`     | Cancel an order                           | `orderId`                         | Yes                |
| **Payment Integration**             |            |                                           |                                   |                    |
| `/api/v1/payments/process`          | `POST`     | Process a payment                         | Body data                         | Yes                |
| `/api/v1/payments/status/{paymentId}` | `GET`    | Check payment status                      | `paymentId`                       | Yes                |
| **Product Reviews and Ratings**     |            |                                           |                                   |                    |
| `/api/v1/reviews/{productId}`       | `POST`     | Submit a review for a product             | `productId`, body data            | Yes                |
| `/api/v1/reviews/{productId}`       | `GET`      | Get all reviews for a product             | `productId`                       | No                 |
| `/api/v1/reviews/{reviewId}`        | `PUT`      | Update a review                           | `reviewId`, body data             | Yes                |
| `/api/v1/reviews/{reviewId}`        | `DELETE`   | Delete a review                           | `reviewId`                        | Yes                |
| **Admin Panel**                     |            |                                           |                                   |                    |
| `/api/v1/admin/products`            | `POST`     | Add a new product                         | Body data                         | Yes (Admin only)   |
| `/api/v1/admin/products/{productId}`| `PUT`      | Update a product                          | `productId`, body data            | Yes (Admin only)   |
| `/api/v1/admin/products/{productId}`| `DELETE`   | Delete a product                          | `productId`                       | Yes (Admin only)   |
| `/api/v1/admin/orders`              | `GET`      | Get all orders                            | Query params                      | Yes (Admin only)   |
| `/api/v1/admin/orders/{orderId}/status` | `PUT`  | Update order status                       | `orderId`, body data              | Yes (Admin only)   |
| `/api/v1/admin/users`               | `GET`      | Get all users                             | -                                 | Yes (Admin only)   |
| `/api/v1/admin/users/{userId}`      | `PUT`      | Update user information                   | `userId`, body data               | Yes (Admin only)   |
| **Notifications**                   |            |                                           |                                   |                    |
| `/api/v1/notifications/order`       | `POST`     | Send order notifications                  | Body data                         | Yes (Admin only)   |
| `/api/v1/notifications/promo`       | `POST`     | Send promotional notifications            | Body data                         | Yes (Admin only)   |


