# Product Listing API Documentation

LOGIN FIRST TO GENERATE AUTHENTICATION TOKEN

URL : http://staging-api.cpras.co.uk/api/login <br>
METHOD: POST

PARAMETERS: <br>
```
email – type : string 
password – type: string 
```
 

EXAMPLE:
```
{ 
  email: test@admin.com, 
  password: testpassword 
}
```
RESPONSE:
```
{
"access_token": "some_token_here",
"token_type": "Bearer",
"expires_at": "2022-10-19 01:10:41"
}
```

LIST PRODUCTS

URL : http://staging-api.cpras.co.uk/api/products <br>
METHOD: GET
HEADERS: <br>
```
{ Authorization : Bearer [token from login action] }
```
PARAMETERS:
```
page – type : integer, required: no
per_page – type: integer, required: no
term - type: string, required: no
```
EXAMPLE:
```
headers {Authorization : Bearer some_token_here}
Parameters {page: 1,}
```
RESPONSE:
```
{ products: [array list of products],meta: {"page": 1,"total": 2,"per_page": 10,"pages": 1}}
```

CREATE PRODUCT

URL : http://staging-api.cpras.co.uk/api/products <br>
METHOD: POST
HEADERS:
```
{ Authorization : Bearer [token from login action] }
```
PARAMETERS: <br>
- **name** – **type** : _string_, **required**: _yes_ <br>
- **description** – **type**: _string_, **required**: _yes_ <br>
- **prices** - **type**: _float_, **required**: _yes_ <br>
- **quantity** – **type** : _float_, **required**: _yes_ <br>
- **categories** – **type** : _array_, **required**: _yes_ <br>
- **website** – **type** : _string_, **required**: _no_ <br>
- **product_specifications** – **type** : _array_, **required**: _no_ <br>

EXAMPLE:

### headers 
```
{Authorization : Bearer some_token_here}
```
### parameters
```javascript
{
  "name" : "test product",
  "description" : "some description",
  "prices" : 100.00,
  "quantity" : 10,
  "categories" : [1,2,3], // get category_ids from http://staging-api.cpras.co.uk/api/categories
  "website" : "http://www.testwebsite.com",
  "product_specifications" : [
    "description" : "Weight",
    "unit" : 1, // Refer to list of units
    "specific_unit" : "kg", // refer to available specific units based from unit selected
    "response" : 50,
    "notes" : "size may vary"
  ]
}
```

RESPONSE:
```
{
message: “test product has been created successfully”,
product: { id: 1}
}
```

