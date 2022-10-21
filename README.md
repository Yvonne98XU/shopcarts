# This is the project for our shopcarts team
[![codecov](https://codecov.io/gh/Yvonne98XU/shopcarts/branch/main/graph/badge.svg?token=8L8B46E60A)](https://codecov.io/gh/Yvonne98XU/shopcarts)

## Important: Before you submit a pull request. Make sure

- Run `nosetests` to make sure that all tests are passed and code coverage are no less than 95%

- Run `make lint` to make sure that there is no Pylint error. 

## Reminder: Whenever you make changes to the table schema. Run `flask create-db` to sync the database

## Run `flask run` to start the service. If you want to clean the database, run `flask create-db`.

Product table schema
```
{
      id: auto_generated            Int           Primary key
      user_id: user_id1             String        foreign key
      product_id: product_id1       String        key
      quantity: product_quantity1   Float
      name: product_name1           String
      price: price1                 Float
      time: purchase_time1          Date
}
```
Shopcarts table schema
```
Shopcarts schema
{
      id: auto_generated          Int          Primary key
      user_id: user_id1           String       unique
}
```

**List of REST API endpoints**
----
```
POST   /shopcarts		 <- Create a shopcart
GET    /shopcarts	     <- List all shopcarts
GET    /shopcarts/{id}	 <- Read a shopcart 
PUT    /shopcarts/{id}	 <- Update a shopcart
DELETE /shopcarts/{id}	 <- Delete a shopcart

POST   /shopcarts/{id}/items	   <- Add an item to a shopcart
GET    /shopcarts/{id}/items	   <- List all items in a shopcart
GET    /shopcarts/{id}/items/{id}  <- Read an item from a shopcart
PUT    /shopcarts/{id}/items/{id}  <- Update an item in a shopcart
DELETE /shopcarts/{id}/items/{id}  <- Delete an item from a shopcart
```

**Create a shopcart**
----
  Create a shopcart by user_id

* **URL**

  POST /shopcarts

* **Request Headers:**
Content-Type: application/json
* **Body:**

  ```json
  {
    "user_id": "1"
  }
  ```
 
* **Success Response:**

  * **Code:** HTTP_201_CREATED <br />
    **Content:** 
    ```json
    { 
      "id" : 1, 
      "name" : [], 
      "user_id": "1" 
    }
    ```

* **Error Response:**

  * **Code:** HTTP_409_CONFLICT <br />
    **Content:** 
    ```json
    {
      "error": "Conflict",
      "message": "409 Conflict: Shopcart 1 already exists",
      "status": 409
    }
    ```


**Update a shopcart**
----
  Update a shopcart by user_id and shopcart list

* **URL**

  PUT /shopcarts/<user_id>

* **Request Headers:**
Content-Type: application/json
* **Body:**

  ```json
  [{
      "user_id": "1",
      "product_id": "2",
      "name": "xixi",
      "quantity": 133,
      "price": 2,
      "time": "2020-12-13"
  }]
  ```
 
* **Success Response:**

  * **Code:** HTTP_201_CREATED <br />
    **Content:** 
    ```json
    {
        "id": 3,
        "products": [
            {
                "id": 4,
                "name": "xixi",
                "price": 2.0,
                "product_id": "2",
                "quantity": 133.0,
                "time": "2020-12-13",
                "user_id": "1"
            }
        ],
        "user_id": "1"
    }
    ```

* **Error Response:**

  * **Code:** HTTP_409_CONFLICT <br />
    **Content:** 
    ```json
    {
    "error": "Conflict",
    "message": "409 Conflict: Shopcart 1 already exists",
    "status": 409
    }
    ```

**Read a shopcart**
----
  Read a shopcart by user_id

* **URL**

  GET /shopcarts/<user_id>

* **Request Headers:**
NULL
* **Body:**
NULL
 
* **Success Response:**

  * **Code:** HTTP_200_OK <br />
    **Content:** 
    ```json
        {
        "id": 2,
        "products": [
            {
                "id": 1,
                "name": "xixi",
                "price": 2.0,
                "product_id": "2",
                "quantity": 13.0,
                "time": "2020-12-13",
                "user_id": "1"
            }
        ],
        "user_id": "1"
    }
    ```

* **Error Response:**

  * **Code:** HTTP_404_NOT_FOUND <br />
    **Content:** 
    ```json
    {
    "error": "Not Found",
    "message": "404 Not Found: Shopcart with id '11' was not found.",
    "status": 404
    }
    ```

**Read all shopcarts**
----
  Read all shopcarts in table

* **URL**

  GET /shopcarts

* **Request Headers:**
NULL
* **Body:**
NULL
 
* **Success Response:**
* **Code:** HTTP_200_OK <br />
    **Content:** 
    ```json
    [
        {
            "id": 3,
            "products": [
                {
                    "id": 2,
                    "name": "xixi",
                    "price": 2.0,
                    "product_id": "2",
                    "quantity": 13.0,
                    "time": "2020-12-13",
                    "user_id": "1"
                }
            ],
            "user_id": "1"
        }
    ]
    ```

* **Error Response:**
NULL

**Delete a shopcart**
----
  Delete a shopcart by user_id

* **URL**
    
    DELETE /shopcarts/<user_id>

* **Request Headers:**
NULL
* **Body:**
NULL
 
* **Success Response:**

  * **Code:** HTTP_204_NO_CONTENT <br />
    **Content:** 
    NO_CONTENT

* **Error Response:**
NULL


**Create a product**
----
  Create a product by used_id and product detail

* **URL**

  POST /shopcarts/<user_id>/items

* **Request Headers:**
Content-Type: application/json
* **Body:**

  ```json
  {
      "user_id": "1",
      "product_id": "2",
      "name": "haha",
      "quantity": 12,
      "price": 1,
      "time": "2020-12-12"
  }
  ```
 
* **Success Response:**

  * **Code:** HTTP_201_CREATED <br />
    **Content:** 
      ```json
      {
          "id": 1,
          "name": "haha",
          "price": 1.0,
          "product_id": "2",
          "quantity": 12.0,
          "time": "2020-12-12",
          "user_id": "1"
      }
      ```

* **Error Response:**
NULL


**Read a product**
----
  Read a shopcart by user_id and product_id

* **URL**

  GET /shopcarts/<user_id>/items/<product_id>

* **Request Headers:**
NULL
* **Body:**
NULL
 
* **Success Response:**

  * **Code:** HTTP_200_OK <br />
    **Content:** 
    ```json
    {
        "id": 2,
        "name": "xixi",
        "price": 2.0,
        "product_id": "2",
        "quantity": 13.0,
        "time": "2020-12-13",
        "user_id": "1"
    }
    ```

* **Error Response:**

  * **Code:** HTTP_404_NOT_FOUND <br />
    **Content:** 
    ```json
    {
        "error": "Not Found",
        "message": "404 Not Found: Product with id 1 was not found in shopcart 1.",
        "status": 404
    }
    ```

**Read all product**
----
  Read all product in table

* **URL**

  GET /shopcarts/<user_id>/items

* **Request Headers:**
NULL
* **Body:**
NULL
 
* **Success Response:**
* **Code:** HTTP_200_OK <br />
    **Content:** 
    ```json
    [
        {
            "id": 2,
            "name": "xixi",
            "price": 2.0,
            "product_id": "2",
            "quantity": 13.0,
            "time": "2020-12-13",
            "user_id": "1"
        },
        {
            "id": 3,
            "name": "haha",
            "price": 1.0,
            "product_id": "3",
            "quantity": 12.0,
            "time": "2020-12-12",
            "user_id": "1"
        }
    ]
    ```

* **Error Response:**

  * **Code:** HTTP_404_NOT_FOUND <br />
    **Content:** 
    ```json
    {
        "error": "Not Found",
        "message": "404 Not Found: Shopcart with id '11' was not found.",
        "status": 404
    }
    ```


**Update a product**
----
  Update a product by user_id and product_id and product detail

* **URL**

  PUT /shopcarts/<user_id>

* **Request Headers:**
Content-Type: application/json
* **Body:**

  ```json
  {
      "user_id": "1",
      "product_id": "2",
      "name": "xixi",
      "quantity": 131,
      "price": 2,
      "time": "2020-12-13"
  }
  ```
 
* **Success Response:**

  * **Code:** HTTP_200_OK <br />
    **Content:** 
    ```
    {
        "id": 2,
        "name": "xixi",
        "price": 2.0,
        "product_id": "2",
        "quantity": 131.0,
        "time": "2020-12-13",
        "user_id": "1"
    }
    ```

* **Error Response:**

  * **Code:** HTTP_404_NOT_FOUND <br />
    **Content:** 
    ```json
    {
        "error": "Not Found",
        "message": "404 Not Found: Product with id 21 was not found in shopcart 1.",
        "status": 404
    }
    ```


**Delete a product**
----
  Delete a product by user_id and product_id

* **URL**

  DELETE /shopcarts/<user_id>/items/<product_id>

* **Request Headers:**
NULL
* **Body:**
NULL
 
* **Success Response:**

  * **Code:** HTTP_204_NO_CONTENT <br />
    **Content:** 
    NO_CONTENT

* **Error Response:**

  * **Code:** HTTP_404_NOT_FOUND <br />
    **Content:** 
    ```json
    {
        "error": "Not Found",
        "message": "404 Not Found: Product with id 3 was not found in shopcart 2.",
        "status": 404
    }
    ```
