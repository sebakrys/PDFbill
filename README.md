# PDFbill

## Overview

PDFbill is a Spring Boot application that generates PDF bills using the iText library. The application provides a REST endpoint for generating PDF bills based on various input parameters such as utility charges, addresses, and user details.

## Features

- Dynamically generate PDF bills with detailed utility breakdowns.
- Support for both lump-sum and itemized billing.
- Automatically generate file names based on building and flat identifiers.
- RESTful API for easy integration.
- Provides bills for multiple locators within the same flat.

## How It Works

The application exposes a single endpoint that accepts query parameters, processes the data, and returns a PDF document.

### Endpoint

`GET /rachunek`

### Request Parameters

| Parameter        | Type           | Description                                      |
|------------------|----------------|--------------------------------------------------|
| `year`           | `int`          | Year of the bill                                 |
| `month`          | `int`          | Month of the bill                                |
| `ryczalt`        | `boolean`      | Indicates whether lump-sum billing is used       |
| `flatid`         | `long`         | Identifier for the flat                          |
| `buildingid`     | `long`         | Identifier for the building                      |
| `street`         | `string`       | Street name                                      |
| `bNr`            | `string`       | Building number                                  |
| `fNr`            | `string`       | Flat number                                      |
| `postalcode`     | `string`       | Postal code                                      |
| `city`           | `string`       | City name                                        |
| `fr`             | `double`       | Fundusz Remontowy usage                          |
| `fr_rate`        | `double`       | Fundusz Remontowy rate                           |
| `g`              | `double`       | Gas usage                                        |
| `g_rate`         | `double`       | Gas rate                                         |
| `og`             | `double`       | Heating usage                                    |
| `og_rate`        | `double`       | Heating rate                                     |
| `pr`             | `double`       | Electricity usage                                |
| `pr_rate`        | `double`       | Electricity rate                                 |
| `sc`             | `double`       | Sewage usage                                     |
| `sc_rate`        | `double`       | Sewage rate                                      |
| `cw`             | `double`       | Hot water usage                                  |
| `cw_rate`        | `double`       | Hot water rate                                   |
| `zw`             | `double`       | Cold water usage                                 |
| `zw_rate`        | `double`       | Cold water rate                                  |
| `usr_names`      | `string`       | Primary user's name                              |
| `otherLocators`  | `List<string>` | List of other locators (comma-separated values)  |

### Example Request

```http
GET http://localhost:8080/rachunek?year=2022&month=9&ryczalt=true&flatid=1&buildingid=2&street=Main&bNr=10&fNr=2A&postalcode=12345&city=SampleCity&fr=100&fr_rate=1.5&g=50&g_rate=2.2&og=200&og_rate=3.5&pr=300&pr_rate=0.75&sc=400&sc_rate=1.1&cw=120&cw_rate=2.5&zw=140&zw_rate=1.8&usr_names=John Doe&otherLocators=Jane Doe, Mike Smith
```
### Response

The response is a PDF file containing the detailed bill. The file is returned with a header:

```php
Content-Disposition: inline; filename=<buildingid>_<flatid>_<year>_<month>.pdf
```

### Postman Collection

To simplify testing, a Postman collection is included:

```plaintext
PDFbillGenerate.postman_collection.json
```

### Prerequisites

- Java 8+
- Maven
- Spring Boot
- iText library for PDF generation



