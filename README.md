# Sports Refund 

The Sports Refund API enables third parties to get quotes and create policies via API calls. A full Swagger document containing the endpoints and models is available in this repo, and client-side SDKs can be built in the language of your choice by pasting this swagger document into the online [Swagger editor](http://editor.swagger.io/).

Below is a high-level overview of the suggested methods of integration by a registration platform.

## Terms

Key terms to understand:

|Term|Required|Description|
|-|-|-|
|Sport|yes|The sport being played. Insurance carriers charge different rates for different sports.|
|Program|yes|Group or Individual. Used to determine insurance rates.|
|Referral Code|no|Used to identify referrals from Sports Refund partner companies, and may impact rates.|
|Coupon Code|no|Used to identify marketing campaigns.|
|Insured|yes|Individual athlete being insured (aka 'the kid who plays').|
|Registrant|yes|Individual registering for insurance (aka 'mom or dad').|
|Organization|yes|Name of the club or team that the insured party is playing for.|

## HTML: Link

Embed a link to [quote.sportsrefund.com](https://quote.sportsrefund.com/quote.html), optionally including a Sport, Organization, ReferralCode or CouponCode.

```html
<a href="https://quote.sportsrefund.com/quote.html">Get a quote</a>
<a href="https://quote.sportsrefund.com/quote.html?Sport=Soccer">Get a quote</a>
<a href="https://quote.sportsrefund.com/quote.html?Sport=Soccer&ReferralCode=SomeCode">Get a quote</a>
<a href="https://quote.sportsrefund.com/quote.html?CouponCode=MyCoupon">Get a quote</a>
```

## HTML: Embedded Form

When using a simple embedded form, a registration site passes information to avoid making a registrant re-enter information, such as the sport, a referral code, and/or an athlete's name.

``` html
<form target="_blank" method="get" action="https://quote.sportsrefund.com/quote.html">
  <input type="hidden" name="Organization" value="Acme Soccer"/>
  <input type="hidden" name="Cost" value="2500"/>
  <input type="hidden" name="Sport" value="Soccer"/>
  <input type="hidden" name="ReferralCode" value="SpecialDiscount"/>
  <input type="text" name="First" placeholder="First name"/>
  <input type="text" name="Last" placeholder="Last name"/>
  <input type="text" name="DOB" placeholder="Birth Date" value="2/3/2004"/>

  <br/>
  <input type="text" name="Address" placeholder="Address"/>
  <br/>
  <input type="text" name="City" placeholder="City"/>
  <input type="text" name="State" placeholder="State"/>
  <input type="text" name="Zip" placeholder="Zip"/>
  </br>
  <button type="submit">Get a quote</button>
</form>
```

A [fiddle](https://jsfiddle.net/otpam3qb/1/) demonstrates embedding a form into a registration website which passes the information to [quote.sportsrefund.com](https://quote.sportsrefund.com/quote.html).


## API: Get a Quote

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

## API: Create a Policy

Creation of a policy includes:

- Registrant, which is the name of the person registering for the insurance policy
- Insured: an array of insured parties (athletes), including their birthdate and registration fee
- Credit card information: contact Sports Refund to be set up to be invoiced instead of paying by credit card

Endpoint: `/api/Payment/createpolicy`

Sample Request:

```json
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
    "expirationYear": 2022
  },
}
```

Sample response:

```json
{
  "paymentTransactionID": 1,
  "paymentTransaction": "This transaction has been approved.",
  "amount": 138.0,
  "status": "Success",
  "serviceSubmissionDate": "2020-05-20T11:27:36.6988823Z",
  "transactionID": "60143297830",
  "authorizationCode": "YB9CNL"
}
```
