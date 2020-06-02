# Sports Refund / GotSoccer Integration

## Terms

|Got Soccer Term|Sports Refund Term|
|-|-|
club name|organization|
program name|**ignored for now**|
start date|effective|
end date|expires|
sport|sport|
parent first/last name|registrant|
athlete first/last name|insured|
athlete date of birth|birthDate|
registration fee|registrationFee|


## HTML: Embedded Form

When using a json-based embedded form, pass Json using a form with a hidden `Policy` field:

``` html
<form target="_blank" method="get" action="https://quote.sportsrefund.com/quote.html">
  <input type="hidden" name="Policy" value="{see json below}"/>
  <button type="submit">Get a quote</button>
</form>
```

Sample Request:

```json
{
  "sport": "Soccer",
  "program": "Individual",
  "effective": "2020-06-08",
  "expires": "2020-06-08",
  "referralCode": "GotSoccer",
  "organization": "ABC Soccer Club",
  "registrant": {
    "firstName": "Adam",
    "lastName": "Ant",
    "email": "a.ant@gmail.com",
  },
  "insured": [
    {
      "contact": {
        "fisrtName": "Bobby"
        "lastName": "Beaman"
      },
      "registrationFee": 2500,
      "birthDate": "2010-01-01"
    },
    {
      "contact": {
        "fisrtName": "Charlie"
        "lastName": "Chaplin"
      },
      "registrationFee": 2255.75,
      "birthDate": "2010-02-02"
    }
  ],
}
```
