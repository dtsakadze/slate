# 8. Titles

Titles are the sender names that are displayed to the recipient when receiving an SMS. The default value for a title is 'Message', which will be displayed to the recipient unless you specify an active title while sending a message.
The maximum number of titles you can create depends on which subscription plan you are using.

<!-- ? get titles -->
<!-- ? get titles -->
<!-- ? get titles -->
## Get Titles

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/titles")
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
curl -X GET "https://oneconnect.uno/api/v1/titles" \
     -u email:api_key
```

> JSON Response:

```json
[
    {
        "id": 1,
        "active": false,
        "name": "Test title",
        "created_at": "2019-07-09 15:10:07 +0400",
        "updated_at": "2019-07-09 15:10:07 +0400"
    },
    {
        "id": 2,
        "active": false,
        "name": "Test 2",
        "created_at": "2019-07-09 16:55:51 +0400",
        "updated_at": "2019-07-09 16:55:51 +0400"
    }
]
```

Get the list of all titles.

`GET https://oneconnect.uno/api/v1/titles`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the title
active | boolean | status of the title
name | string | name of the title
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

### You can get the titles in a CSV format with the following request:

`GET https://oneconnect.uno/api/v1/titles_csv`

You can use the following URL as a direct download link for the titles.csv file: `https://oneconnect.uno/sms/titles.csv`.

<!-- ? get a single title -->
<!-- ? get a single title -->
<!-- ? get a single title -->
## Get Title

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/titles/:id")
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
curl -X GET "https://oneconnect.uno/api/v1/titles/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
    "id": 1,
    "active": false,
    "name": "Test title",
    "created_at": "2019-07-09 15:10:07 +0400",
    "updated_at": "2019-07-09 15:10:07 +0400"
}
```

Get a specific title with its id.

`GET https://oneconnect.uno/api/v1/titles/:id`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the title
active | boolean | status of the title
name | string | name of the title
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

<!-- ? create a title -->
<!-- ? create a title -->
<!-- ? create a title -->
## Create Title

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/titles")
request = Net::HTTP::Post.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
  "name" => "#{name}"
)

req_options = {
  use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
  http.request(request)
end
```

```shell
curl -X POST "https://oneconnect.uno/api/v1/titles" \
     -u email:api_key \
     -d 'name=#{name}'
```

> JSON Response:

```json
{
    "id": 12,
    "active": false,
    "name": "New title",
    "created_at": "2019-07-19 22:12:17 +0400",
    "updated_at": "2019-07-19 22:12:17 +0400"
}
```
<aside class="warning">After creating a title it needs activation from our side.</aside>

You will receive a notification when the title gets activated.

There are certain rules for creating titles:

<table>
  <tbody>
    <tr>
      <td>maximum length</td>
      <td>11</td>
    </tr>
    <tr>
      <td>allowed characters</td>
      <td>
        a b c d e f g h i j k l m o p q r s t u v w x y z<br />
        A B C D E F G H I J K L M N O P Q R S T U V W X Y Z<br />
        0 1 2 3 4 5 6 7 8 9<br />
        "-" (dash)<br />
        "." (dot)<br />
        " " (free space)
      </td>
    </tr>
  </tbody>
</table>

`POST https://oneconnect.uno/api/v1/titles`

### Request Parameters

Parameter | Type | Description
--------- | ---- | -----------
name | string | name of the title

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the title
active | boolean | status of the title
name | string | name of the title
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

In case of any errors you will receive the following parameters:

Parameter | Description
------- | --------
errors | array of errors

<!-- ? delete a title -->
<!-- ? delete a title -->
<!-- ? delete a title -->
## Delete Title

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/titles/:id")
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
curl -X DELETE "https://oneconnect.uno/api/v1/titles/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
    "error_code": 0,
    "message" : "Title deleted."
}
```

`DELETE https://oneconnect.uno/api/v1/titles/:id`