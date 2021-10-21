# Product Listing API Documentation

### LOGIN FIRST TO GENERATE AUTHENTICATION TOKEN

URL : h<span>ttp</span>://staging-api.cpras.co.uk/api/login <br>
METHOD: POST

###### PARAMETERS:
```
email – type : string 
password – type: string 
```
 

###### EXAMPLE:
```json
{ 
  "email": "test@admin.com", 
  "password": "testpassword" 
}
```
###### RESPONSE:
```json
{
 "access_token": "some_token_here",
 "token_type": "Bearer",
 "expires_at": "2022-10-19 01:10:41"
}
```

###### LIST PRODUCTS

URL : h<span>ttp</span>://staging-api.cpras.co.uk/api/products <br>
METHOD: GET
###### HEADERS: 
```javascript
{ 
  Authorization : Bearer token_from_login_action
}
```
###### PARAMETERS:
```
page – type : integer, required: no
per_page – type: integer, required: no
term - type: string, required: no
```
###### EXAMPLE:

###### headers 
```javascript
{
  Authorization : Bearer some_token_here
}
```
###### parameters 
```
{
  page: 1,
}
```
###### RESPONSE:
```javascript
{ 
  "products": 
  [], //array list of products
  "meta": 
    {
      "page": 1,
      "total": 2,
      "per_page": 10,
      "pages": 1
    }
 }
```

### CREATE PRODUCT

URL : h<span>ttp</span>://staging-api.cpras.co.uk/api/products <br>
METHOD: POST
###### HEADERS:
```javascript
{ 
  Authorization : Bearer token_from_login_action
}
```
###### PARAMETERS: <br>
- **name** – **type** : **_string_**, **required**: **_yes_** <br>
- **description** – **type**: **_string_**, **required**: **_yes_** <br>
- **prices** - **type**: **_float_**, **required**: **_yes_** <br>
- **quantity** – **type** : **_float_**, **required**: **_yes_** <br>
- **categories** – **type** : **_array_**, **required**: **_yes_** <br>
- **website** – **type** : **_string_**, **required**: **_no_** <br>
- **product_specifications** – **type** : **_array_**, **required**: **_no_** <br>

###### EXAMPLE:

###### headers 
```javascript
{
  Authorization : Bearer some_token_here
}
```
###### parameters raw JSON
```javascript
{
  "name" : "test product",
  "description" : "some description",
  "prices" : 100.00,
  "quantity" : 10,
  "supplier_id" : 1, // set this to one at the moment
  "categories" : 1, // get category_ids from http://staging-api.cpras.co.uk/api/categories
  "website" : "http://www.testwebsite.com",
  "unit" : 1,  // leave this as is at the moment
  "product_specifications" : "[{ \"specific_unit\" : \"kg\", \"notes\" : \"size may vary\", \"response\" : 1, \"specification\" : { \"description\" : \"Weight\", \"unit\" : 1, \"response\" : 50}}]"
```

###### parameters form-data
| Key | Value |
| --- | --- |
| name | Test Value |
| description | Test Description |
| prices | 100 |
| supplier_id | 1 |
| quantity | 1 |
| categories | 1 |
| website | testsite.site |
| unit | 1 |
| product_specifications | [{"specific_unit" : "kg", "notes" : "size may vary", "response" : 1,"specification" : {"description" : "Weight","unit" : "1", "response" : "50"}}] |

       
- for **unit** inside product_specifications, please refer to list of units
- for **specific_unit**, please refer to available specific units based form unit selected

###### RESPONSE:
```json
{
  "message" : "test product has been created successfully",
  "product" : { "id" : 1 }
}
```
### LIST OF UNITS

```json
"units" : [
     { "value" : 1, "text" : "Time" },
     { "value" : 2, "text" : "Weight" },
     { "value" : 3, "text" : "Height" },
     { "value" : 4, "text" : "Choice" },
     { "value" : 5, "text" : "Speed" },
     { "value" : 6, "text" : "length" },
     { "value" : 7, "text" : "Option" }
   ],
 ```
### VALUE 1 AS UNIT : TIME
```json
"time_units" : [
  { "value" : "s", "text" : "second (s)" }, 
  { "value" : "m", "text" : "minute (m)" },
  { "value" : "hr", "text" : "hour (hr)" },
],
```
 
### VALUE 2 AS UNIT : WEIGHT
```json
"weight_units" : [
     { "value" : "t", "text" : "tonne (t)" },
     { "value" : "kg", "text" : "kilogram (kg)" },
     { "value" : "g", "text" : "gram (g)" },
     { "value" : "mg", "text" : "milligram (mg)" },
     { "value" : "lb", "text" : "pound (lb)" },
     { "value" : "oz", "text" : "ounce (oz)" },
   ],
 ```

### VALUE 5 AS UNIT : SPEED
```json
"speed_units" : [
    { "value" : "m/s", "text" : "metres per second (m/s)" }, 
    { "value" : "km/h", "text" : "kilometres per hour (km/h)" },
    { "value" : "mph", "text" : "miles per hour (mph)" },
    { "value" : "ft/s", "text" : "Foot per second (ft/s)" },
    { "value" : "Kn", "text" : "Knot (kn)" },
  ],
```

### VALUE 3 AS UNIT : HEIGHT 6 AS UNIT : LENGTH
```json
"length_units" : [
    { "value" : "mm", "text" : "millimeter (mm)" }, 
    { "value" : "cm", "text" : "centimeter (cm)" },
    { "value" : "m", "text" : "meter (m)" },
    { "value" : "km", "text" : "kilometer (km)" },
    { "value" : "in", "text" : "inch (in)" },
    { "value" : "yd", "text" : "foot (ft)" },
    { "value" : "mi", "text": "mile (mi)" },
    { "value" : "nmi", "text" : "nautical mile (nmi)" },
  ],
```
