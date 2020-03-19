# Sports Refund API

The Sports Refund API enables third parties to get quotes and create policies via API calls. A full Swagger document containing the endpoints and models is available in this repo, and client-side SDKs can be built in the language of your choice by pasting this swagger document into the online [Swagger editor](http://editor.swagger.io/).

Below is a high-level overview of the key API endpoints used by a registration platform.

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

- Registrant, which is the name of the person registering for the insurance policy
- Insured: an array of insured parties (athletes), including their birthdate and registration fee
- Credit card information: contact Sports Refund to be set up to be invoiced instead of paying by credit card

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
