# Sports Refund API

The Sports Refund API enables third parties to get quotes and create policies via API calls.

## Quote

Endpoint: `/api/Policy/quote`

Posting the following JSON to the quote endpoint:

``` json
{
  "sport": "Hockey - Ice",
  "program": "Group",
  "organization": "ABC Hockey Club",
  "approximateCost": 4000,
  "insured": [
    {
      "registrationFee": 4000,
      "birthDate": "2010-03-19"
    },
    {
      "registrationFee": 3500,
      "birthDate": "2012-01-09"
    }
  ],
}
```

will return JSON structure like this:

``` json
{
  "premium": 175.00,
  "administrativeFee": 10
}
```

## Create a Policy

Creation of a policy includes:

- 

Endpoint: `/api/Payment/createpolicy`

Sample Request:

``` json
{
  "effective": "2020-04-01",
  "expires": "2021-04-01",
  "sport": "Hockey - Ice",
  "program": "Group",
  "organization": "ABC Hockey Club",
  "approximateCost": 4000,
  "registrant": {
    "firstName": "Adam",
    "lastName": "Ant",
    "title": "Owner of ABC Hockley Club"
    "address": "123 A Street",
    "city": "Anywhere",
    "state": "AL",
    "zip": "11111",
    "email": "a.ant@gmail.com",
  },
  "insured": [
    {
      "policyId": 0,
      "contactId": 0,
      "contact": {
        "fisrtName": "Bobby"
        "lastname": "Beaman"
      },
      "registrationFee": 0,
      "birthDate": "2010-01-01"
    },
    {
      "policyId": 0,
      "contactId": 0,
      "contact": {
        "fisrtName": "Charlie"
        "lastname": "Chaplin"
      },
      "registrationFee": 0,
      "birthDate": "2010-02-02"
    }
  ],
  "card": {
    "card": "My credit card",
    "cardNumber": "[credit card number here]",
    "cardCode": "[CVV code]",
    "expirationMonth": 10,
    "expirationYear": 2020
  },
}
```
