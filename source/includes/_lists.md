# 5. Lists

<!-- ? get lists -->
<!-- ? get lists -->
<!-- ? get lists -->
## Get Lists

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/lists")
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
curl -X GET "https://oneconnect.uno/api/v1/lists" \
     -u email:api_key
```

> JSON Response:

```json
[
    {
        "id": 1,
        "name": "Test list",
        "members": [
            {
                "id": 1,
                "email": "test@oneconnect.uno",
                "first_name": "John",
                "last_name": "Doe",
                "phone_number": "111111",
                "birthday": "05/05/1997",
                "post_code": "0160",
                "city": "London",
                "street": "221B Baker Street",
                "additional_numbers": [],
                "gender": "Male",
                "created_at": "2019-07-08 12:34:00 +0400",
                "updated_at": "2019-07-10 14:19:22 +0400"
            }
        ],
        "noncontact_members": null,
        "created_at": "2019-05-20 18:02:58 +0400",
        "updated_at": "2019-05-20 18:06:04 +0400"
    }
]
```

`GET https://oneconnect.uno/api/v1/lists`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the list
name | string | name of the list
members | array | array of contacts that are in this list (you can check contact parameters in the contacts section)
noncontact_members | json/hash | hash of arrays, the members that are in this list but aren't saved as contacts. (Noncontact members are added by uploading a list from a CSV file. You can check additional details and rules about CSV uploading on the [OneConnect Manual](https://oneconnect.uno/manual) page.)
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

### You can get the lists in a CSV format with the following request:

`GET https://oneconnect.uno/api/v1/lists_csv`

You can use the following URL as a direct download link for the lists.csv file: `https://oneconnect.uno/sms/lists.csv`.

<!-- ? get a single list by name -->
<!-- ? get a single list by name -->
<!-- ? get a single list by name -->
## Get List by Name

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/lists")
request = Net::HTTP::Get.new(uri)
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
curl -X GET "https://oneconnect.uno/api/v1/lists" \
     -u email:api_key \
     -d 'name=#{name}'
```

> JSON Response:

```json
{
    "id": 1,
    "name": "Test list",
    "members": [
        {
            "id": 1,
            "email": "test@oneconnect.uno",
            "first_name": "John",
            "last_name": "Doe",
            "phone_number": "111111",
            "birthday": "05/05/1997",
            "post_code": "0160",
            "city": "London",
            "street": "221B Baker Street",
            "additional_numbers": [],
            "gender": "Male",
            "created_at": "2019-07-08 12:34:00 +0400",
            "updated_at": "2019-07-10 14:19:22 +0400"
        }
    ],
    "noncontact_members": null,
    "created_at": "2019-05-20 18:02:58 +0400",
    "updated_at": "2019-05-20 18:06:04 +0400"
}
```

You can get the list by its name by passing the name parameter to the request.

`GET https://oneconnect.uno/api/v1/lists?name=#{name}`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the list
name | string | name of the list
members | array | array of contacts that are in this list (you can check contact parameters in the contacts section)
noncontact_members | json/hash | hash of arrays, the members that are in this list but aren't saved as contacts. (Noncontact members are added by uploading a list from a CSV file. You can check additional details and rules about CSV uploading on the [OneConnect Manual](https://oneconnect.uno/manual) page.)
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

<!-- ? get a single list by id -->
<!-- ? get a single list by id -->
<!-- ? get a single list by id -->
## Get List by ID

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/lists/:id")
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
curl -X GET "https://oneconnect.uno/api/v1/lists/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
    "id": 1,
    "name": "Test list",
    "members": [
        {
            "id": 1,
            "email": "test@oneconnect.uno",
            "first_name": "John",
            "last_name": "Doe",
            "phone_number": "111111",
            "birthday": "05/05/1997",
            "post_code": "0160",
            "city": "London",
            "street": "221B Baker Street",
            "additional_numbers": [],
            "gender": "Male",
            "created_at": "2019-07-08 12:34:00 +0400",
            "updated_at": "2019-07-10 14:19:22 +0400"
        }
    ],
    "noncontact_members": null,
    "created_at": "2019-05-20 18:02:58 +0400",
    "updated_at": "2019-05-20 18:06:04 +0400"
}
```

Get a specific list with its id.

`GET https://oneconnect.uno/api/v1/lists/:id`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the list
name | string | name of the list
members | array | array of contacts that are in this list (you can check contact parameters in the contacts section)
noncontact_members | json/hash | hash of arrays, the members that are in this list but aren't saved as contacts. (Noncontact members are added by uploading a list from a CSV file. You can check additional details and rules about CSV uploading on the [OneConnect Manual](https://oneconnect.uno/manual) page.)
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

<!-- ? create a list -->
<!-- ? create a list -->
<!-- ? create a list -->
## Create List

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/lists")
request = Net::HTTP::Post.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "name" => "#{name}",
    "members" => "#{members}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X POST "https://oneconnect.uno/api/v1/lists" \
     -u email:api_key \
     -d 'name=#{name}' \
     -d 'members=#{members}'
```

> JSON Response:

```json
{
    "id": 1,
    "name": "Test list",
    "members": [
        {
            "id": 1,
            "email": "test@oneconnect.uno",
            "first_name": "John",
            "last_name": "Doe",
            "phone_number": "111111",
            "birthday": "05/05/1997",
            "post_code": "0160",
            "city": "London",
            "street": "221B Baker Street",
            "additional_numbers": [],
            "gender": "Male",
            "created_at": "2019-07-08 12:34:00 +0400",
            "updated_at": "2019-07-10 14:19:22 +0400"
        }
    ],
    "noncontact_members": null,
    "created_at": "2019-05-20 18:02:58 +0400",
    "updated_at": "2019-05-20 18:06:04 +0400"
}
```

`POST https://oneconnect.uno/api/v1/lists`

### Request Parameters

Parameter | Type | Description
--------- | ---- | -----------
name | string | name of the list
members | string | ids of contacts that you want to add to this list separated by commas(','). (ex. id1, id2, id3...). Whether you put spaces after commas is entirely up to you.

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the list
name | string | name of the list
members | array | array of contacts that are in this list (you can check contact parameters in the contacts section)
noncontact_members | json/hash | hash of arrays, the members that are in this list but aren't saved as contacts. (Noncontact members are added by uploading a list from a CSV file. You can check additional details and rules about CSV uploading on the [OneConnect Manual](https://oneconnect.uno/manual) page.)
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

In case of any errors you will receive the following parameters:

Parameter | Description
------- | --------
errors | array of errors

<!-- ? update a list -->
<!-- ? update a list -->
<!-- ? update a list -->
## Update List

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/lists")
request = Net::HTTP::Patch.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "name" => "#{name}",
    "members" => "#{members}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X PATCH "https://oneconnect.uno/api/v1/lists" \
     -u email:api_key \
     -d 'name=#{name}' \
     -d 'members=#{members}'
```

> JSON Response:

```json
{
    "id": 1,
    "name": "Test list",
    "members": [
        {
            "id": 1,
            "email": "test@oneconnect.uno",
            "first_name": "John",
            "last_name": "Doe",
            "phone_number": "111111",
            "birthday": "05/05/1997",
            "post_code": "0160",
            "city": "London",
            "street": "221B Baker Street",
            "additional_numbers": [],
            "gender": "Male",
            "created_at": "2019-07-08 12:34:00 +0400",
            "updated_at": "2019-07-10 14:19:22 +0400"
        }
    ],
    "noncontact_members": null,
    "created_at": "2019-05-20 18:02:58 +0400",
    "updated_at": "2019-05-20 18:06:04 +0400"
}
```

`PATCH https://oneconnect.uno/api/v1/lists`

### Request Parameters

<aside class="notice">It's not necessary to pass both name and members parameters. You can pass only the parameters which you want to update.</aside>

Parameter | Type | Description
--------- | ---- | -----------
name | string | name of the list
members | string | ids of contacts that you want to add to this list separated by commas(','). (ex. id1, id2, id3...). Whether you put spaces after commas is entirely up to you.

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the list
name | string | name of the list
members | array | array of contacts that are in this list (you can check contact parameters in the contacts section)
noncontact_members | json/hash | hash of arrays, the members that are in this list but aren't saved as contacts. (Noncontact members are added by uploading a list from a CSV file. You can check additional details and rules about CSV uploading on the [OneConnect Manual](https://oneconnect.uno/manual) page.)
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

In case of any errors you will receive the following parameters:

Parameter | Description
------- | --------
errors | array of errors

<!-- ? add members -->
<!-- ? add members -->
<!-- ? add members -->
## Add Members

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/lists/:id/add_members")
request = Net::HTTP::Post.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "ids" => "#{ids}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X POST "https://oneconnect.uno/api/v1/lists/:id/add_members" \
     -u email:api_key \
     -d 'ids=#{ids}'
```

> JSON Response:

```json
{
    "id": 1,
    "name": "Test list",
    "members": [
        {
            "id": 1,
            "email": "test@oneconnect.uno",
            "first_name": "John",
            "last_name": "Doe",
            "phone_number": "111111",
            "birthday": "05/05/1997",
            "post_code": "0160",
            "city": "London",
            "street": "221B Baker Street",
            "additional_numbers": [],
            "gender": "Male",
            "created_at": "2019-07-08 12:34:00 +0400",
            "updated_at": "2019-07-10 14:19:22 +0400"
        }
    ],
    "noncontact_members": null,
    "created_at": "2019-05-20 18:02:58 +0400",
    "updated_at": "2019-05-20 18:06:04 +0400"
}
```

Add members to the list with the ids of contacts.

`POST https://oneconnect.uno/api/v1/lists/:id/add_members`

### Request Parameters

Parameter | Type | Description
--------- | ---- | -----------
ids | string | ids of contacts that you want to add to this list separated by commas(','). (ex. id1, id2, id3...). Whether you put spaces after commas is entirely up to you.

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the list
name | string | name of the list
members | array | array of contacts that are in this list (you can check contact parameters in the contacts section)
noncontact_members | json/hash | hash of arrays, the members that are in this list but aren't saved as contacts. (Noncontact members are added by uploading a list from a CSV file. You can check additional details and rules about CSV uploading on the [OneConnect Manual](https://oneconnect.uno/manual) page.)
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

In case of any errors you will receive the following parameters:

Parameter | Description
------- | --------
errors | array of errors

<!-- ? remove members -->
<!-- ? remove members -->
<!-- ? remove members -->
## Remove Members

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/lists/:id/remove_members")
request = Net::HTTP::Post.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "ids" => "#{ids}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X POST "https://oneconnect.uno/api/v1/lists/:id/remove_members" \
     -u email:api_key \
     -d 'ids=#{ids}'
```

> JSON Response:

```json
{
    "id": 1,
    "name": "Test list",
    "members": [
        {
            "id": 1,
            "email": "test@oneconnect.uno",
            "first_name": "John",
            "last_name": "Doe",
            "phone_number": "111111",
            "birthday": "05/05/1997",
            "post_code": "0160",
            "city": "London",
            "street": "221B Baker Street",
            "additional_numbers": [],
            "gender": "Male",
            "created_at": "2019-07-08 12:34:00 +0400",
            "updated_at": "2019-07-10 14:19:22 +0400"
        }
    ],
    "noncontact_members": null,
    "created_at": "2019-05-20 18:02:58 +0400",
    "updated_at": "2019-05-20 18:06:04 +0400"
}
```

`POST https://oneconnect.uno/api/v1/lists/:id/remove_members`

### Request Parameters

Parameter | Type | Description
--------- | ---- | -----------
ids | string | ids of contacts that you want to remove from this list separated by commas(','). (ex. id1, id2, id3...). Whether you put spaces after commas is entirely up to you.

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the list
name | string | name of the list
members | array | array of contacts that are in this list (you can check contact parameters in the contacts section)
noncontact_members | json/hash | hash of arrays, the members that are in this list but aren't saved as contacts. (Noncontact members are added by uploading a list from a CSV file. You can check additional details and rules about CSV uploading on the [OneConnect Manual](https://oneconnect.uno/manual) page.)
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

In case of any errors you will receive the following parameters:

Parameter | Description
------- | --------
errors | array of errors

<!-- ? delete a list -->
<!-- ? delete a list -->
<!-- ? delete a list -->
## Delete List

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/lists/:id")
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
curl -X DELETE "https://oneconnect.uno/api/v1/lists/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
    "error_code": 0,
    "message" : "List deleted."
}
```

`DELETE https://oneconnect.uno/api/v1/lists/:id`