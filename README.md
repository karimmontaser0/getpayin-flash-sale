Flash Sale Checkout API
API built with Laravel to handle products and a simple flash sale checkout flow.
Requirements
PHP 8.x
Composer
MySQL or SQLite
Laravel CLI (composer create-project already used)
Setup
Clone the repository:

git clone https://github.com/karimmontaser0/getpayin-flash-sale.git
cd getpayin-flash-sale

Install dependencies:

composer install

Environment & database:

cp .env.example .env

Configure database connection in .env (MySQL or SQLite).
Then run:

php artisan key:generate
php artisan migrate --seed

Run the development server:

php artisan serve

Default URL: http://127.0.0.1:8000
API Endpoints
All endpoints are prefixed with /api.
List products

GET /api/products

Get single product

GET /api/products/{id}

Example response:

{
  "success": true,
  "data": {
    "id": 1,
    "name": "Laptop",
    "description": "High-performance laptop",
    "price": "999.99",
    "stock": 45,
    "created_at": "2025-11-30T00:45:58.000000Z",
    "updated_at": "2025-11-30T00:48:48.000000Z"
  }
}

Create product

POST /api/products
Content-Type: application/json

Body:

{
  "name": "Laptop",
  "price": 999.99,
  "description": "High-performance laptop",
  "stock": 50
}

Update product

PUT /api/products/{id}

Delete product

DELETE /api/products/{id}

Checkout product (flash sale)

POST /api/products/{id}/checkout
Content-Type: application/json

Body:

{
  "quantity": 5
}

Example success response:

{
  "success": true,
  "message": "Checkout successful",
  "data": {
    "product": {
      "id": 1,
      "name": "Laptop",
      "price": 999.99
    },
    "quantity": 5,
    "total_price": 4999.95,
    "remaining_stock": 45
  }
}

Example insufficient stock response:

{
  "success": false,
  "message": "Insufficient stock available",
  "available_stock": 10,
  "requested_quantity": 50
}
Notes
Validation errors return success: false and a list of errors.

All responses are JSON.
