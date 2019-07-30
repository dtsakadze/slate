# 9. Templates

Prepare and save repeatable texts in order to save your precious time. All you need to do is create a predefined message template and use it anytime you need.

<!-- ? get templates -->
<!-- ? get templates -->
<!-- ? get templates -->
## Get Templates

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/templates")
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
curl -X GET "https://oneconnect.uno/api/v1/templates" \
     -u email:api_key
```

> JSON Response:

```json
[
    {
        "id": 3,
        "title": "Birthday",
        "body": "Happy birthday.",
        "created_at": "2019-07-13 14:59:30 +0400",
        "updated_at": "2019-07-13 14:59:30 +0400"
    },
    {
        "id": 4,
        "title": "Greeting",
        "body": "Hello, how's your day going?",
        "created_at": "2019-07-13 17:19:56 +0400",
        "updated_at": "2019-07-13 17:19:56 +0400"
    }
]
```

Get the list of all templates.

`GET https://oneconnect.uno/api/v1/templates`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the template
title | boolean | title of the template
body | text | content of the template
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

<!-- ? get a single template -->
<!-- ? get a single template -->
<!-- ? get a single template -->
## Get Template

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/templates/:id")
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
curl -X GET "https://oneconnect.uno/api/v1/templates/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
    "id": 4,
    "title": "Greeting",
    "body": "Hello, how's your day going?",
    "created_at": "2019-07-13 17:19:56 +0400",
    "updated_at": "2019-07-13 17:19:56 +0400"
}
```

Get a specific template with its id.

`GET https://oneconnect.uno/api/v1/templates/:id`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the template
title | boolean | title of the template
body | text | content of the template
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

<!-- ? create a template -->
<!-- ? create a template -->
<!-- ? create a template -->
## Create Template

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/templates")
request = Net::HTTP::Post.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "title" => "#{title}",
    "body" => "#{body}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X POST "https://oneconnect.uno/api/v1/templates" \
     -u email:api_key \
     -d 'title=#{title}' \
     -d 'body=#{body}'
```

> JSON Response:

```json
{
    "id": 5,
    "title": "New Year",
    "body": "Happy new year!",
    "created_at": "2019-08-23 12:11:21 +0400",
    "updated_at": "2019-08-23 12:11:21 +0400"
}
```

`POST https://oneconnect.uno/api/v1/templates`

### Request Parameters

Parameter | Type | Description
--------- | ---- | -----------
title | string | name of the template
body | text | content of the template

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the template
title | boolean | title of the template
body | text | content of the template
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

In case of any errors you will receive the following parameters:

Parameter | Description
------- | --------
errors | array of errors

<!-- ? delete a template -->
<!-- ? delete a template -->
<!-- ? delete a template -->
## Delete Template

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/templates/:id")
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
curl -X DELETE "https://oneconnect.uno/api/v1/templates/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
    "error_code": 0,
    "message" : "Template deleted."
}
```

`DELETE https://oneconnect.uno/api/v1/templates/:id`