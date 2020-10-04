# Lemon-docs
Documentation for Lemon🍋

## Lemon API
### Data structures

#### User
Represents user and his data.
| Field    | Type   | Description   |
|----------|--------|---------------|
| name     | String | Username      |
| login    | String | User login    |
| password | String | User password |

#### Card
Represents either bank cards or cash.
| Field    | Type   | Description   |
|----------|--------|---------------|
| card_id  | Int    | Card id in Lemon🍋 |
| bank     | String | Bank name.<br>__Possible values__: `Mono`, `Privat24`, `Cash` |
| card_num | Int    | Last 4 digits of card number |
| type | String | Card type. Varies depending on bank's rules. Values aren't determined by Lemon🍋.<br>__Examples of possible values__:<br>`black`, `mono`, `card for payments`, `universal`, etc |
| balance | Int | Amount of money on card in lowest units (cents, kopek, etc) |
| currency | String | Currency of transactions from this cards.<br>__Examples of possible values__: `UAH`, `USD`.|

#### Transaction
Represents money transaction from or to card.
| Field    | Type   | Description   |
|----------|--------|---------------|
| card_id  | Int    | Card id in Lemon🍋 |
| amount   | Int    | Amount of money transfered during this transaction.<br>Amount is negative is money were transfered from card and positive in other case. |
| type  | String    | Description of transaction. This value is not determined by Lemon🍋.<br>__Examples of possible values__: `Cafe`, `Bus ticket`, etc.|
| date  | String    | Transaction date in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601).<br>__Example of value__: `2020-10-04T17:49:29.859Z` |

### POST: /registration
__Body:__ _[User](#user)_ object. Example:
```json
{
  "name": "Oleh",
  "login": "alegator@gmail.com",
  "password": "abcd"
}
```
#### Response:
| Code                      | Description             |
|---------------------------|-------------------------|
| 200 OK                    | Successfully registered |
| 409 Conflict              | Login is already taken  |
| 428 Precondition Required | Incorrect data          |

### POST: /profile
__Header:__ HTTP Basic Auth: Login, Password

__Body:__ _[User](#user)_ object. Example:
```json
{
  "name": "Oleh",
  "login": "alegator@gmail.com",
  "password": "abcd"
}
```
#### Response:
| Code                      | Description                  |
|---------------------------|------------------------------|
| 200 OK                    | Profile successfully changed |
| 403 Forbidden             | Icorrect login/password      |
| 428 Precondition Required | New data is invalid          |
| 500 Internal Server Error | Internal Server Error        |

### GET: /profile
__Header:__ HTTP Basic Auth: Login, Password

#### Response:
| Code                      | Description                       |
|---------------------------|-----------------------------------|
| 200 OK                    | User's data successfully returned |
| 403 Forbidden             | Icorrect login/password           |
| 500 Internal Server Error | Internal Server Error             |

__Response body:__ _[User](#user)_ object. Example:
```json
{
  "name": "Oleh",
  "login": "alegator@gmail.com",
  "password": "abcd"
}
```

### GET: /cards
__Header:__ HTTP Basic Auth: Login, Password

#### Response:
| Code                      | Description                 |
|---------------------------|-----------------------------|
| 200 OK                    | Cards successfully returned |
| 403 Forbidden             | Incorrect login/password    |
| 500 Internal Server Error | Internal Server Error       |

__Response body:__ List of _[Card](#card)_ objects. Example:
```json
{
  "cards": [
    {
      "card_id": 321,
      "bank": "Mono",
      "card_num": 1243,
      "type": "black",
      "balance": 5901,
      "currency": "UAH"
    },
    {
      "card_id": 111,
      "bank": "Privat24",
      "card_num": 1243,
      "type": "card for payments",
      "balance": 7755,
      "currency": "UAH"
    },
    {
      "card_id": 231,
      "bank": "Cash",
      "card_num": 1243,
      "type": "",
      "balance": 3920,
      "currency": "UAH"
    },
  ]
}
```
### GET: /transactions
__Header:__ HTTP Basic Auth: Login, Password

#### Response:
| Code                      | Description                        |
|---------------------------|------------------------------------|
| 200 OK                    | Transactions successfully returned |
| 403 Forbidden             | Incorrect login/password           |
| 500 Internal Server Error | Internal Server Error              |

__Response body:__ List of _[Transaction](#transaction)_ objects. Example:
```json
{
  "transactions": [
    {
      "card_id": 321,
      "amount": -1500,
      "type": "Cafe",
      "date": "2020-10-04T17:49:29.859Z"
    },
    {
      "card_id": 123,
      "amount": 400,
      "type": "Salary",
      "date": "2020-10-04T17:49:29.859Z"
    }
  ]
}
```
