# Lemon-docs
Documentation for Lemon🍋

## Lemon API
### POST: /registration
__Body:__ _User_ object. Example:
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

__Body:__ _User_ object. Example:
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

__Response body:__ _User_ object. Example:
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

__Response body:__ List of _Card_ objects. Example:
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

__Response body:__ List of _Transaction_ objects. Example:
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
