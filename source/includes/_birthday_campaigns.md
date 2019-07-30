# 7. Birthday Campaigns

<!-- ? get birthday campaigns -->
<!-- ? get birthday campaigns -->
<!-- ? get birthday campaigns -->
## Get Birthday Campaigns

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/birthday_campaigns")
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
curl -X GET "https://oneconnect.uno/api/v1/birthday_campaigns" \
     -u email:api_key
```

> JSON Response:

```json
[
    {
        "id": 11,
        "name": "Birthday Campaign 1",
        "active": false,
        "content": "Happy birthday.",
        "recipient_lists": [
            10
        ],
        "title": "",
        "created_at": "2019-06-20 19:43:45 +0400",
        "updated_at": "2019-06-24 09:01:24 +0400"
    },
    {
        "id": 5,
        "name": "Birthday Campaign 2",
        "active": true,
        "content": "Best wishes on your birthday from OneConnect.",
        "recipient_lists": [
            5
        ],
        "title": "",
        "created_at": "2019-06-20 19:41:21 +0400",
        "updated_at": "2019-06-24 09:01:24 +0400"
    }
]
```

`GET https://oneconnect.uno/api/v1/birthday_campaigns`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the birthday campaign
name | string | name of the birthday campaign
active | boolean | status of the birthday campaign
content | text | text of the messages sent by this campaign
recipient_lists | array of integers | ids of the lists that are in this campaign
title | string | a title which will be used as a sender name when sending messages. The title must be active or the sender name will be set to: 'Message'.
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

### You can filter birthday campaigns by the following parameters:

Parameter | Type | Description
-------- | --------- | --------
active | boolean | filter birthday campaigns by their status

<!-- ? get a single birthday campaign -->
<!-- ? get a single birthday campaign -->
<!-- ? get a single birthday campaign -->
## Get Birthday Campaign

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/birthday_campaigns/:id")
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
curl -X GET "https://oneconnect.uno/api/v1/birthday_campaigns/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
    "id": 11,
    "name": "Birthday Campaign 1",
    "active": false,
    "content": "Happy birthday.",
    "recipient_lists": [
        10
    ],
    "title": "",
    "created_at": "2019-06-20 19:43:45 +0400",
    "updated_at": "2019-06-24 09:01:24 +0400"
}
```

Get a specific birthday campaign with its id.

`GET https://oneconnect.uno/api/v1/birthday_campaigns/:id`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the birthday campaign
name | string | name of the birthday campaign
active | boolean | status of the birthday campaign
content | text | text of the messages sent by this campaign
recipient_lists | array of integers | ids of the lists that are in this campaign
title | string | a title which is used as a sender name when sending messages. The title must be active or the sender name will be set to: 'Message'.
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

<!-- ? create a birthday campaign -->
<!-- ? create a birthday campaign -->
<!-- ? create a birthday campaign -->
## Create Birthday Campaign

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/birthday_campaigns")
request = Net::HTTP::Post.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "name" => "#{name}",
    "active" => "#{active}",
    "content" => "#{content}",
    "title" => "#{title}",
    "recipient_lists" => "#{recipient_lists}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X POST "https://oneconnect.uno/api/v1/birthday_campaigns" \
     -u email:api_key \
     -d 'name=#{name}' \
     -d 'active=#{active}' \
     -d 'content=#{content}' \
     -d 'title=#{title}' \
     -d 'recipient_lists=#{recipient_lists}'
```

> JSON Response:

```json
{
    "id": 11,
    "name": "Birthday Campaign 1",
    "active": false,
    "content": "Happy birthday.",
    "recipient_lists": [
        10
    ],
    "title": "",
    "created_at": "2019-06-20 19:43:45 +0400",
    "updated_at": "2019-06-24 09:01:24 +0400"
}
```

`POST https://oneconnect.uno/api/v1/birthday_campaigns`

### Request Parameters

Parameter | Type | Description
--------- | ---- | -----------
name | string | name of the birthday campaign
active | boolean | status of the birthday campaign
content | boolean | text of the messages sent by this campaign
recipient_lists | string | ids of the lists that are in this campaign separated by commas (','). Whether you put spaces after commas is entirely up to you.
title | integer | the id of the title which will be used as a sender name when sending messages. The title must be active or the sender name will be set to: 'Message'.

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the birthday campaign
name | string | name of the birthday campaign
active | boolean | status of the birthday campaign
content | text | text of the messages sent by this campaign
recipient_lists | array of integers | ids of the lists that are in this campaign
title | string | a title which is used as a sender name when sending messages. The title must be active or the sender name will be set to: 'Message'.
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

Errors:

Error code | Description
-------- | ---------
4020 | Invalid ids for recipient_lists.

In case of any additional errors you will receive the following parameters:

Parameter | Description
------- | --------
errors | array of errors

<!-- ? update a birthday campaign -->
<!-- ? update a birthday campaign -->
<!-- ? update a birthday campaign -->
## Update Birthday Campaign

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/birthday_campaigns")
request = Net::HTTP::Patch.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "name" => "#{name}",
    "active" => "#{active}",
    "content" => "#{content}",
    "title" => "#{title}",
    "recipient_lists" => "#{recipient_lists}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X PATCH "https://oneconnect.uno/api/v1/birthday_campaigns" \
     -u email:api_key \
     -d 'name=#{name}' \
     -d 'active=#{active}' \
     -d 'content=#{content}' \
     -d 'title=#{title}' \
     -d 'recipient_lists=#{recipient_lists}'
```

> JSON Response:

```json
{
    "id": 11,
    "name": "Birthday Campaign 1",
    "active": false,
    "content": "Happy birthday.",
    "recipient_lists": [
        10
    ],
    "title": "",
    "created_at": "2019-06-20 19:43:45 +0400",
    "updated_at": "2019-06-24 09:01:24 +0400"
}
```

`PATCH https://oneconnect.uno/api/v1/birthday_campaigns`

### Request Parameters

<aside class="notice">It's not necessary to pass every parameter. You can pass only those parameters which you want to update.</aside>

Parameter | Type | Description
--------- | ---- | -----------
name | string | name of the birthday campaign
active | boolean | status of the birthday campaign
content | boolean | text of the messages sent by this campaign
recipient_lists | string | ids of the lists that are in this campaign separated by commas (','). Whether you put spaces after commas is entirely up to you.
title | integer | the id of the title which will be used as a sender name when sending messages. The title must be active or the sender name will be set to: 'Message'.

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the birthday campaign
name | string | name of the birthday campaign
active | boolean | status of the birthday campaign
content | text | text of the messages sent by this campaign
recipient_lists | array of integers | ids of the lists that are in this campaign
title | string | a title which is used as a sender name when sending messages. The title must be active or the sender name will be set to: 'Message'.
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

Errors:

Error code | Description
-------- | ---------
4020 | Invalid ids for recipient_lists.

In case of any additional errors you will receive the following parameters:

Parameter | Description
------- | --------
errors | array of errors

<!-- ? delete a birthday campaign -->
<!-- ? delete a birthday campaign -->
<!-- ? delete a birthday campaign -->
## Delete Birthday Campaign

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/birthday_campaigns/:id")
request = Net::HTTP::Delete.new(uri)
request.basic_auth("email", "api_key")

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X DELETE "https://oneconnect.uno/api/v1/birthday_campaigns/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
    "error_code": 0,
    "message" : "Birthday Campaign deleted."
}
```

`DELETE https://oneconnect.uno/api/v1/birthday_campaigns/:id`