# Index

- [Api Keys](#api-keys)
- [Authentication](#authentication)
- [Giftcards](#giftcards)


## API Keys

### Authenticating your requests
Happs authenticates your API requests using your API keys.
If you do not provide an API key on a request, the API's will return a unauthorized error.

Every vendor is provided with a set of keys, one for our test environment, and one for our production environment.

### Obtaining your keys
To get a set of keys, you need to reach out to the Happs team at [support@happs.dk](mailto:support@happs.dk)

To be able to distinguish the keys, the test key will always be prefixed with `happs_test_`. And the production key will always be prefixed with `happs_prod_`. Examples of this could be `happs_test_u6eP3mBZRJtFWKvsAjbx7h8t9YbbDfSpcJ9p8WQA4VkfXBwzcK` and `happs_prod_u6eP3mBZRJtFWKvsAjbx7h8t9YbbDfSpcJ9p8WQA4VkfXBwzcK`

## Authentication
Authentication to the API is performed via [HTTP Basic Auth](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication). Provide your API key as the basic auth username value. You do not need to provide a password.

## Giftcards

Endpoints
- [POST:/giftcards/:code/redeem](#redeem-value-from-a-giftcard)
- [GET:/giftcards/:code/value_remaining](#get-remaining-value-on-a-giftcard)

### Redeem value from a giftcard
Redeems a given value from the giftcard, if value remaining on the giftcard is 0, it will also mark the giftcard as `Inactive`.

Production
```
curl --location --request POST 'https://vendor-api.happs.dk/api/giftcards/8c34b723599d/redeem' \
-u happs_prod_TJPeCzYz6CX8s675YzbhYXrwrdbekhpPC3U6svv8W4RYKzUAYV: \
-d '{"value": 100}'
```

Test
```
curl --location --request POST 'https://azfun-vendorapi-happs-t.azurewebsites.net/api/giftcards/8c34b723599d/redeem' \
-u happs_test_TJPeCzYz6CX8s675YzbhYXrwrdbekhpPC3U6svv8W4RYKzUAYV: \
-d '{"value": 100}'
```


**Parameters**
| Name | Required | Description |
| ---- | -------- | ----------- |
| value | Yes | The value to redeem on the giftcard

___
**Responses**

200 OK
```
{
  "valueRedeemed": 100,
  "valueRemaining": 200
}
```

400 Bad Request

401 Unauthorized

404 Not Found
```
{
  "message": "Error Message"
}
```

### Get remaining value on a giftcard
Returns the current value on a giftcard

Production
```
curl --location --request GET 'https://vendor-api.happs.dk/api/giftcards/{code}/value_remaining' \
-u happs_prod_TJPeCzYz6CX8s675YzbhYXrwrdbekhpPC3U6svv8W4RYKzUAYV:
```

Test
```
curl --location --request GET 'https://azfun-vendorapi-happs-t.azurewebsites.net/api/giftcards/{code}/value_remaining' \
-u happs_test_TJPeCzYz6CX8s675YzbhYXrwrdbekhpPC3U6svv8W4RYKzUAYV:
```



**Parameters**
None
___
**Responses**

200 OK
```
{
  "valueRemaining": 200
}
```

401 Unauthorized

404 Not Found
```
{
  "message": "Error Message"
}
```