# 10. Info

<!-- ? get balance -->
## Get Balance

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/balance")
request = Net::HTTP::Get.new(uri)
request.basic_auth("email", "api_key")

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X GET "https://oneconnect.uno/api/v1/balance" \
     -u email:api_key
```

> JSON Response:

```json
{
    "sms_balance": 930
}
```

`GET https://oneconnect.uno/api/v1/balance`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
sms_balance | integer | your sms balance

<!-- ? get pricing details -->
## Get Pricing Details

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/pricing")
request = Net::HTTP::Get.new(uri)
request.basic_auth("email", "api_key")

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X GET "https://oneconnect.uno/api/v1/pricing" \
     -u email:api_key
```

> JSON Response:

```json
[
    {
        "name": "Basic",
        "price": 9.98,
        "price_yearly": 99.8,
        "messages_history_limit": 100,
        "contacts_limit": 20,
        "lists_limit": 5,
        "titles_limit": 1,
        "campaigns_limit": 0,
        "upload_contacts_from_csv": false,
        "upload_lists_from_csv": false,
        "integrations": false,
        "api_ip_restriction": false
    },
    {
        "name": "Premium",
        "price": 19.98,
        "price_yearly": 199.8,
        "messages_history_limit": 1000,
        "contacts_limit": 100,
        "lists_limit": 20,
        "titles_limit": 5,
        "campaigns_limit": 5,
        "upload_contacts_from_csv": false,
        "upload_lists_from_csv": false,
        "integrations": false,
        "api_ip_restriction": false
    },
    {
        "name": "Business",
        "price": 39.98,
        "price_yearly": 399.8,
        "messages_history_limit": null,
        "contacts_limit": null,
        "lists_limit": null,
        "titles_limit": null,
        "campaigns_limit": null,
        "upload_contacts_from_csv": true,
        "upload_lists_from_csv": true,
        "integrations": true,
        "api_ip_restriction": true
    }
]
```

`GET https://oneconnect.uno/api/v1/pricing`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
name | string | name of the plan.
price | decimal | monthly price of the plan.
price_yearly | decimal | yearly price of the plan.
messages_history_limit | integer | number of messages that will be in the history (null means unlimited).
contacts_limit | integer | maximum number of contacts that you can create (null means unlimited).
lists_limit | integer | maximum number of lists that you can create (null means unlimited).
titles_limit | integer | maximum number of titles that you can create (null means unlimited).
campaigns_limit | integer | maximum number of campaigns that you can create (null means unlimited).
upload_contacts_from_csv | boolean | ability to upload contacts from csv or not.
upload_lists_from_csv | boolean | ability to upload lists from csv or not.
integrations | boolean | whether the integrations are available to you.
api_ip_restriction | boolean | availability of the ip restriction service for the API. You can read more in the [manual](https://oneconnect.uno/manual).