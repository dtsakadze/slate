# 3. SMS

<!-- ? get messages -->
<!-- ? get messages -->
<!-- ? get messages -->
## Get Messages

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/messages")
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
curl -X GET "https://oneconnect.uno/api/v1/messages" \
     -u email:api_key
```

> JSON Response:

```json
[
    {
        "id": 16,
        "final_status": "delivered",
        "campaign_id": 0,
        "birthday_campaign": false,
        "sms": {
            "destination": "123456789",
            "content": "hello."
        },
        "delivery_report": {
            "status": "Delivered",
            "reason": "0"
        },
        "created_at": "2019-06-17 11:16:55 +0400",
        "updated_at": "2019-06-17 11:16:57 +0400"
    },
    {
        "id": 18,
        "final_status": "delivered",
        "campaign_id": 11,
        "birthday_campaign": false,
        "sms": {
            "destination": "987654321",
            "content": "Test message for oneconnect."
        },
        "delivery_report": {
            "status": "Delivered",
            "reason": "0"
        },
        "created_at": "2019-06-17 11:21:01 +0400",
        "updated_at": "2019-06-17 11:21:03 +0400"
    }
]
```

Get the list of all messages.

`GET https://oneconnect.uno/api/v1/messages`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the message
final_status | string | delivery status of the message
campaign_id | integer | id of the campaign (only if the message is sent by a campaign)
birthday_campaign | boolean | whether or not the message is sent by a birthday campaign
sms | hash | message details. Inner parameters: <br> destination (string) --> recipient number, <br> content (string) --> message text
delivery_report | hash | delivery report details. Inner parameters: <br> status (string) --> delivery status, <br> reason (string) --> reason if the message fails
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

### You can filter messages by the following parameters:

You can perform mixed filtering by passing multiple parameters to the request.

Parameter | Type | Description
-------- | ---------
final_status | string | filter messages by their final status (possible values: 'delivered', 'undelivered', 'pending')
campaign_id | integer | filter messages by their campaigns ids (i.e. returns messages which are sent by the specified campaign).
birthday_campaign | boolean | messages which are sent by a birthday campaign (if you specify both campaign_id and birthday_campaign=true and the system will return the messages which are sent with a certain birthday campaign)
start_date | string | e.g. "25.08.2019 22:21" messages sent since the specified date. Format - DD.MM.YYYY HH:MM
end_date | string | e.g. "31.12.2019 23:59" messages sent until the specified date. Format - DD.MM.YYYY HH:MM
limit | the maximum number of messages to be listed
page & per_age | you can paginate the messages by passing the page & per_page parameters (both parameters are required for pagination). per_page parameter specifies the number of records to be fetched on a single page, page parameter specifies the number of the page. e.g. page=3&per_page=100 will get the 3rd page of the paginated messages with 100 records.

<!-- ? get a single message -->
<!-- ? get a single message -->
<!-- ? get a single message -->
## Get Message

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/messages/:id")
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
curl -X GET "https://oneconnect.uno/api/v1/messages/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
        "id": 18,
        "final_status": "delivered",
        "campaign_id": 11,
        "birthday_campaign": false,
        "sms": {
            "destination": "987654321",
            "content": "Test message for oneconnect."
        },
        "delivery_report": {
            "status": "Delivered",
            "reason": "0"
        },
        "created_at": "2019-06-17 11:21:01 +0400",
        "updated_at": "2019-06-17 11:21:03 +0400"
    }
```

Get a specific message with its id.

`GET https://oneconnect.uno/api/v1/messages/:id`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the message
final_status | string | delivery status of the message
campaign_id | integer | id of the campaign (only if the message is sent by a campaign)
birthday_campaign | boolean | whether or not the message is sent by a birthday campaign
sms | hash | message details. Inner parameters: <br> destination (string) --> recipient number, <br> content (string) --> message text
delivery_report | hash | delivery report details. Inner parameters: <br> status (string) --> delivery status, <br> reason (string) --> reason if the message fails
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

<!-- ? send message -->
<!-- ? send message -->
<!-- ? send message -->
## Send Message

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/messages")
request = Net::HTTP::Post.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "title" => "#{title}",
    "contacts" => "#{contacts}",
    "lists" => "#{lists}",
    "destination" => "#{destination}",
    "content" => "#{content}",
    "send_now" => "#{send_now}",
    "reference" => "#{reference}",
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X POST "https://oneconnect.uno/api/v1/messages" \
     -u email:api_key \
     -d 'title=#{title}' \
     -d 'contacts=#{contacts}' \
     -d 'lists=#{lists}' \
     -d 'destination=#{destination}' \
     -d 'content=#{content}' \
     -d 'send_now=#{send_now}' \
     -d 'reference=#{reference}'
```

> JSON Response:

```json
{
    "error_code": 0,
    "status": "OK",
    "message": "Message sent successfully."
}
```

`POST https://oneconnect.uno/api/v1/messages`

### Request Parameters

Parameter | Type | Description
-------- | --------- | ---------
title | integer | id of the title which will be used as a sender name.
contacts | string | array of contact ids separated by commas (','). Whether you put space after commas if entirely up to you.
lists | string | array of lists ids separated by commas (','). Whether you put space after commas if entirely up to you.
destination | string | array of additional phone numbers that are not in your contacts separated by commas (','). Whether you put space after commas if entirely up to you.
content | string | content of the message (max length is 160 characters)
send_now | boolean | whether the message must be sent straight away or scheduled (default value is true). If you set send_now to false then you must pass the sms_date parameter.
sms_date | string | this parameter is passed only if the send_now parameter is set to false. The datetime when the message must be sent (e.g. "11.09.2001 08:46").
reference | string | special id of the message that you assign. Will be used for receiving delivery reports. You won't receive a delivery report if this parameter is not specified.

### Response Parameters

Parameter | Type
--------- | -----------
error_code | integer
status | string
message | string

### Delivery Report Parameters

Delivery report parameters will be sent to the URL that you specify in the "Delivery report callback URL" on your [profile page](https://oneconnect.uno/sms/account)

Parameter | Type | Description
-------- | -------- | ---------
reference | string | reference specified by you while sending a message
status | string | delivery status of the message
reason | string | reason if the message fails
destination | string | recipient number of the message

Errors:

Error code | Description
-------- | ---------
1000 | No balance.
1001 | Content parameter must be specified.
1002 | One of the following parameters must be specified: [:destination, :contacts, :lists].
1004 | The following parameter must be specified when scheduling an SMS: sms_date.
1005 | Invalid datetime.
1010 | Content length can't be more than 160.

<!-- ? send group messages -->
<!-- ? send group messages -->
<!-- ? send group messages -->
## Send Group Message

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/group_sms")
request = Net::HTTP::Post.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "title" => "#{title}",
    "content" => "#{content}",
    "reference" => "#{reference}",
    "genders" => "#{genders}",
    "age_from" => "#{age_from}",
    "age_to" => "#{age_to}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X POST "https://oneconnect.uno/api/v1/group_sms" \
     -u email:api_key \
     -d 'title=#{title}' \
     -d 'content=#{content}' \
     -d 'reference=#{reference}' \
     -d 'genders=#{genders}' \
     -d 'age_from=#{age_from}' \
     -d 'age_to=#{age_to}'
```

> JSON Response:

```json
{
    "error_code": 0,
    "status": "OK"
}
```

`POST https://oneconnect.uno/api/v1/group_sms`

### Request Parameters

Parameter | Type | Description
-------- | --------- | ---------
title | integer | id of the title which will be used as a sender name. Default title is "Message".
content | string | (required) content of the message (max length is 160 characters).
reference | string | special id of the message that you assign. Will be used for receiving delivery reports. You won't receive a delivery report unless this parameter is specified.
genders | string | (required) possible values: "male, female", "male", "female".
age_from | integer | (optional) minimum age of the contacts you want to send a message to. Default value is 0.
age_to | integer | (optional) maximum age of the contacts you want to send a message to. Will be set to maximum by default.

### Response Parameters

Parameter | Type
--------- | -----------
error_code | integer
status | string

Errors:

Error code | Description
-------- | ---------
1001 | Content parameter must be specified.
2005 | Invalid gender parameter.