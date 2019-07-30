<!-- ? sms autheticator -->
# 11. SMS Authenticator

SMS Authenticator is an implementation of one factor, that can be a part of Multi-factor authentication (MFA) and allows to make user/client authorization simple. A verification code is generated automatically by our system and sent as an SMS to the recipient phone number specified by your request. The code is also sent to you as a response to the request so that you can check if the code typed by your user/client is valid.

## Code Sending

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/mfa/sms_auth")
request = Net::HTTP::Post.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "phone_number" => "#{phone_number}",
    "only_numbers" => "#{only_numbers}",
    "only_uppercase" => "#{only_uppercase}",
    "length" => "#{length}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X POST "https://oneconnect.uno/api/v1/mfa/sms_auth" \
     -u email:api_key \
     -d 'phone_number=#{phone_number}' \
     -d 'only_numbers=#{only_numbers}' \
     -d 'only_uppercase=#{only_uppercase}' \
     -d 'length=#{length}'
```

> JSON Response:

```json
{
    "code": "9Rs77NuQ",
    "phone_number": "123456789"
}
```

`POST https://oneconnect.uno/api/v1/mfa/sms_auth`

### Request Parameters

Parameter | Type | Description
--------- | ---- | -----------
phone_number | string | (required) recipient phone number.
only_numbers | boolean | (optional) set this parameter to true if you want to generate only numbers. Default value is "false".
only_uppercase | boolean | (optional) setting this parameter to true will generate a code with only upper case letters. Default value is "false".
length | integer | (optional) length of the code. Default value is 4.

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
code | string | code generating by the system and sent as an SMS
phone_number | string | recipient phone number

Errors:

Error code | Description
-------- | ---------
1000 | No balance.
4004 | Invalid phone number.