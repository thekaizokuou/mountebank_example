## Preparation and install software

1. Install nodejs 'https://nodejs.org/en/download/'
2. Install mountebank 'npm install -g mountebank'

## Start mountebank

You can start mountebank by command 'mb' but this is empty of mountebank.

If you already have config file of imposter so you can use the below command to start mountebank with your config.
```bash
mb --configfile ./imposters.ejs --allowInjection --loglevel debug
```
or you can run by use script.
```bash
./start_mb_local.sh
```

## Test request mountebank with Postman

Import share link of Postman then test request it.

Postman share link

`https://www.getpostman.com/collections/c26a7f62b8f063a4c29c`

## Mountebank specification

##### GET /v1/profiles/${user_id}

> - user_id end with *1234 will always get profile success
> - user_id end with *6666 will return error dormant account
> - user_id end with *7777 will return error inactive account
> - user_id end with *8888 will return error suspend account
> - user_id end with *9999 will return error frozen account
> - Other will be user not found

##### POST /v1/profiles
request body

```json
{
    "card_identification": "<card_id>",
    "request_transaction_id": "<tran_id>"
}
```
    
> -  card_id start with XY* will always post profile success
> -  card_id start with USED* will return error card already used
> -  Other will be card not found
 
##### POST /v1/balances
header basic auth \
request body

```json
{
    "card_identification": "<card_id>",
    "request_transaction_id": "<tran_id>"
}
```
        
> -  basic auth user: robot, password: robot other will return authorization failed
> -  card_id start with XY* will always post balances success
> -  Other will be card not found

##### POST /v1/kyc
header basic auth \
request body

```json
{
    "user_id": "<user_id>",
    "request_transaction_id": "<tran_id>",
    "kyc" : {
        "first_name": "robot",
        "last_name": "robot",
        "birthdate": "24/03/2540",
        "jc": "JC1234567890"
    }
}
```
     
> -  basic auth user: robot, password: robot other will return authorization failed
> -  user_id end with *1234 will passed to checked kyc
>     -  If you put kyc data like example above kyc will matched
>     -  If you put kyc data did not like example above kyc will not matched
> -  kyc data is a required field
> -  Other user_id will be user not found
  
##### POST /v1/address
request body

```json
{	
    "user_id": "<user_id>",
    "request_transaction_id": "<tran_id>",
    "address": {
        "en": {
            "address1": "9 Ratchadaphisek Rd",
            "address2": "",
            "sub_district": "Chatuchak",
            "district": "Chatuchak",
            "province": "Bangkok",
            "postcode": "10900"
        },
        "th": {
            "address1": "9 ถนนรัชดาภิเษก",
            "address2": "",
            "sub_district": "แขวงจตุจักร",
            "district": "เขตจตุจักร",
            "province": "กรุงเทพฯ",
            "postcode": "10900"
        }
    }
}
```

> -  user_id end with *1234 will success to post address
> -  address, address.en and address.th data is a required field
> -  Other user_id will be user not found

##### Get /v1/address/${user_id}
request body
 
> -  user_id end with *1234 will success to get address
>    -  Now mock data have 2 `accept-language` (en and th) default is `en`
> -  Other user_id will be user not found
