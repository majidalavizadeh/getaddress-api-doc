# 🔧 GetAddress Endpoints

GetAddress.nl provides a **RESTful API** that allows developers to retrieve address information in the Netherlands.  
All API endpoints use the base URL:

```
https://api.getaddress.nl/v1
```

To make a request, you must include your **API key** in the URL, following this format:

```
https://api.getaddress.nl/v1/API_KEY/ENDPOINT
```

- All requests must be made using the **GET** method.
- Parameters should be sent via **query string**.
- All responses are returned in **JSON format**.

---

## 🔍 Overview of Available APIs

### 📮 1. Search by Postcode API

Retrieve a **full address and house details** using a **postcode and house number**.

#### **Request Format**

```http
GET /postcode?query=POSTCODE&number=HOUSE_NUMBER&letter=HOUSE_ADDITION
```

#### **Parameters**

- `postcode` (**required**) → The postcode (e.g., `1234AB`).
- `number` (**optional**) → The house number. If omitted, all houses in the street will be returned.
- `letter` (**optional**) → House addition (if applicable) to refine the results.

#### **Example Request**

```http
GET https://api.getaddress.nl/v1/API_KEY/postcode?query=1012AB&number=1
```

#### **Response Example**

```json
[
  {
    "postcode": "1012AB",
    "number": 1,
    "letter": null,
    "suffix": null,
    "street": "Stationsplein",
    "municipality": "Amsterdam",
    "city": "Amsterdam",
    "province": "Noord-Holland",
    "construct": 2018,
    "latitude": 52.3785,
    "longitude": 4.90315,
    "rd_x": 122040,
    "rd_y": 487955,
    "surface": 594,
    "purpose": "overige gebruiksfunctie"
  }
]
```

---

### 🏘 2. Search by Street API

Find all streets containing a specific name across different cities.  
You can optionally **limit the search to a specific city**.

#### **Request Format**

```http
GET /street?query=STREET_NAME&city=CITY&limit=LIMIT
```

#### **Parameters**

- `query` (**required**) → The street name to search for.
- `city` (**optional**) → If provided, limits the search to a specific city.
- `limit` (**optional**) → Maximum number of results to return.

#### **Example Request**

```http
GET https://api.getaddress.nl/v1/API_KEY/street?query=Stationsplein
```

#### **Response Example**

```json
[
  { "street": "Stationsplein", "city": "Groningen" },
  { "street": "Stationsplein", "city": "Haren Gn" },
  { "street": "Stationsplein", "city": "Almere" },
  { "street": "Stationsplein", "city": "Ter Apel" },
  { "street": "Stationsplein", "city": "Buitenpost" },
  { "street": "Stationsplein", "city": "Bolsward" },
  { "street": "Stationsplein", "city": "Heerenveen" },
  { "street": "Stationsplein", "city": "Leeuwarden" },
  { "street": "Stationsplein", "city": "Lemmer" },
  { "street": "Stationsplein", "city": "Oosterwolde" }
]
```

---

### 🔎 3. Search API (Query Type Detection)

Identify the type of a given query. The API determines whether the searched term is a **street, city, or another type**.

#### **Request Format**

```http
GET /search?query=QUERY&type=TYPES&translate_types=TRUE|FALSE
```

#### **Parameters**

- `query` (**required**) → The value to search for.
- `type` (**optional**) → Specify the type of data to search (e.g., **street**, **city**). The available types can be retrieved via the `/types` endpoint.
- `translate_types` (**optional**) → If set to `true`, the result types will be translated to **English**; otherwise, they will be in **Dutch**.

#### **Example Request**

```http
GET https://api.getaddress.nl/v1/API_KEY/search?query=Stationsplein
```

#### **Response Example**

```json
[
  { "naam": "Stationsplein", "type": "Street" },
  { "naam": "Stationsplein Zuid", "type": "Street" },
  { "naam": "Stationsplein-West", "type": "Street" },
  { "naam": "Stationsplein-NO", "type": "Street" },
  { "naam": "Stationsplein-ZW", "type": "Street" },
  { "naam": "Stationsplein-Noord", "type": "Street" },
  { "naam": "Stationsplein-Zuid", "type": "Street" },
  { "naam": "Stationsplein", "type": "Administrative area" },
  { "naam": "Stationspleintunnel", "type": "Art work" },
  { "naam": "Parkeergarage Stationsplein", "type": "Terrein" }
]
```

---

### 📑 4. Get Address Types API

Returns a **list of address types** available in the database, in both **Dutch and English**.

#### **Request Format**

```http
GET /types
```

#### **Example Request**

```http
GET https://api.getaddress.nl/v1/API_KEY/types
```

#### **Response Example**

```json
{
  "administratief gebied": "Administrative area",
  "kunstwerk": "Art work",
  "landschappelijk gebied": "Landscape area",
  "spoorbaan": "Railway track",
  "terrein": "Terrein",
  "water": "Water",
  "weg": "Street",
  "woonplaats": "City",
  "gemeente": "Municipality"
}
```

---

## 🚀 How to Use the API

1. **Request an API key** by emailing your domain name to **hi@getaddress.nl**.
2. Use the **GET** requests shown above to retrieve data.
3. If you expect **high traffic**, inform me in advance.

---

## 💡 Suggestions & Support

This project was built **by a developer, for developers**. If you have an **idea, request, bug report, or issue**, feel free to reach out:

- Drop me a message at [hi@getaddress.nl](mailto:hi@getaddress.nl).
- Share your feedback or suggestions.

Let’s make [**GetAddress.nl**](http://getaddress.nl) even better together!
