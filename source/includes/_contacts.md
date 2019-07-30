# 4. Contacts

<!-- ? get contacts -->
<!-- ? get contacts -->
<!-- ? get contacts -->
## Get Contacts

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/contacts")
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
curl -X GET "https://oneconnect.uno/api/v1/contacts" \
     -u email:api_key
```

> JSON Response:

```json
[
    {
        "id": 1,
        "email": "test@oneconnect.uno",
        "first_name": "John",
        "last_name": "Doe",
        "phone_number": "123456789",
        "birthday": "05/05/1997",
        "post_code": "0160",
        "city": "London",
        "street": "221B Baker Street",
        "additional_numbers": [],
        "gender": "Male",
        "created_at": "2019-07-08 12:34:00 +0400",
        "updated_at": "2019-07-10 14:19:22 +0400"
    }
]
```

`GET https://oneconnect.uno/api/v1/contacts`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the contact
email | string | email of the contact
first_name | string | first name of the contact
last_name | string | last name of the contact
phone_number | string | phone number of the contact
birthday | string | birthday of the contact (format: DD.MM.YYYY)
post_code | string | post code of the contact
city | string | city of the contact
street | string | city of the contact
additional_numbers | array of strings | additioanl phone numbers of the contact
gender | string | gender of the contact
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

### You can filter contacts by the following parameters:

You can perform mixed filtering by passing multiple parameters to the request.

Parameter | Description
-------- | ---------
first_name | list contacts with the given first name
last_name | list contacts with the given last name
phone_number | list contacts with the given phone number
email | list contacts with the given email
birthday | list contacts with the given birthday
post_code | list contacts with the given post code
city | list contacts with the given city
street | list contacts with the given street
gender | list contacts with the given gender
additional_numbers | list contacts with the given additional numbers
limit | the maximum number of contacts to be listed
sort | The parameter specifies the field in the contact database after which the data sorting will be performed. e.g. sort=first_name will sort the contacts by first name in an ascending order, sort=-first_name will sort the contacts by first name in a descending order (the '-' symbol reverses the order from ascending to descending). Any parameter that a contact has can be used for sorting. Multiple parameter filtering is possible by passing multiple parameters separated by commas(','). e.g. sort=first_name,-last_name will sort the contacts by first name in an ascending order and then by their last names in a descending order.
page & per_age | you can paginate the contacts by passing the page & per_page parameters (both parameters are required for pagination). per_page parameter specifies the number of records to be fetched on a single page, page parameter specifies the number of the page. e.g. page=2&per_page=20 will get the 2nd page of the paginated contacts with 20 records.

### You can get the contacts in a CSV format with the following request:

`GET https://oneconnect.uno/api/v1/contacts_csv`

You can use the following URL as a direct download link for the contacts.csv file: `https://oneconnect.uno/sms/contacts.csv`.

<!-- ? get a single contact -->
<!-- ? get a single contact -->
<!-- ? get a single contact -->
## Get Contact

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/contacts/:id")
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
curl -X GET "https://oneconnect.uno/api/v1/contacts/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
    "id": 1,
    "email": "test@oneconnect.uno",
    "first_name": "John",
    "last_name": "Doe",
    "phone_number": "123456789",
    "birthday": "05/05/1997",
    "post_code": "0160",
    "city": "London",
    "street": "221B Baker Street",
    "additional_numbers": [],
    "gender": "Male",
    "created_at": "2019-07-08 12:34:00 +0400",
    "updated_at": "2019-07-10 14:19:22 +0400"
}
```

Get a specific contact with its id.

`GET https://oneconnect.uno/api/v1/contacts/:id`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the contact
email | string | email of the contact
first_name | string | first name of the contact
last_name | string | last name of the contact
phone_number | string | phone number of the contact
birthday | string | birthday of the contact (format: DD.MM.YYYY)
post_code | string | post code of the contact
city | string | city of the contact
street | string | city of the contact
additional_numbers | array of strings | additioanl phone numbers of the contact
gender | string | gender of the contact
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

<!-- ? create a contact -->
<!-- ? create a contact -->
<!-- ? create a contact -->
## Create Contact

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/contacts")
request = Net::HTTP::Post.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "email" => "#{email}",
    "first_name" => "#{first_name}",
    "last_name" => "#{last_name}",
    "phone_number" => "#{phone_number}",
    "birthday" => "#{birthday}",
    "post_code" => "#{post_code}",
    "city" => "#{city}",
    "street" => "#{street}",
    "additional_numbers" => "#{additional_numbers}",
    "gender" => "#{gender}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X POST "https://oneconnect.uno/api/v1/contacts" \
     -u email:api_key \
     -d 'email=#{email}' \
     -d 'first_name=#{first_name}' \
     -d 'last_name=#{last_name}' \
     -d 'phone_number=#{phone_number}' \
     -d 'birthday=#{birthday}' \
     -d 'post_code=#{post_code}' \
     -d 'city=#{city}' \
     -d 'street=#{street}' \
     -d 'additional_numbers=#{additional_numbers}' \
     -d 'gender=#{gender}'
```

> JSON Response:

```json
{
    "id": 1,
    "email": "test@oneconnect.uno",
    "first_name": "John",
    "last_name": "Doe",
    "phone_number": "123456789",
    "birthday": "05/05/1997",
    "post_code": "0160",
    "city": "London",
    "street": "221B Baker Street",
    "additional_numbers": [],
    "gender": "Male",
    "created_at": "2019-07-08 12:34:00 +0400",
    "updated_at": "2019-07-10 14:19:22 +0400"
}
```

`POST https://oneconnect.uno/api/v1/contacts`

### Request Parameters

Parameter | Type | Description
--------- | ---- | -----------
email | string | email of the contact
first_name | string | first name of the contact
last_name | string | last name of the contact
phone_number | string | phone number of the contact
birthday | string | birthday of the contact  (format: DD.MM.YYYY)
post_code | string | post code of the contact
city | string | city of the contact
street | string | street of the contact
additional_numbers | array of string | additional numbers of the contact separated by commas (','). Whether you put spaces after commas is entirely up to you.

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the contact
email | string | email of the contact
first_name | string | first name of the contact
last_name | string | last name of the contact
phone_number | string | phone number of the contact
birthday | string | birthday of the contact (format: DD.MM.YYYY)
post_code | string | post code of the contact
city | string | city of the contact
street | string | city of the contact
additional_numbers | array of strings | additioanl phone numbers of the contact
gender | string | gender of the contact
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

In case of any errors you will receive the following parameters:

Parameter | Description
------- | --------
errors | array of errors

<!-- ? update a contact -->
<!-- ? update a contact -->
<!-- ? update a contact -->
## Update Contact

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/contacts")
request = Net::HTTP::Patch.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "email" => "#{email}",
    "first_name" => "#{first_name}",
    "last_name" => "#{last_name}",
    "phone_number" => "#{phone_number}",
    "birthday" => "#{birthday}",
    "post_code" => "#{post_code}",
    "city" => "#{city}",
    "street" => "#{street}",
    "additional_numbers" => "#{additional_numbers}",
    "gender" => "#{gender}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X PATCH "https://oneconnect.uno/api/v1/contacts" \
     -u email:api_key \
     -d 'email=#{email}' \
     -d 'first_name=#{first_name}' \
     -d 'last_name=#{last_name}' \
     -d 'phone_number=#{phone_number}' \
     -d 'birthday=#{birthday}' \
     -d 'post_code=#{post_code}' \
     -d 'city=#{city}' \
     -d 'street=#{street}' \
     -d 'additional_numbers=#{additional_numbers}' \
     -d 'gender=#{gender}'
```

> JSON Response:

```json
{
    "id": 1,
    "email": "test@oneconnect.uno",
    "first_name": "John",
    "last_name": "Doe",
    "phone_number": "123456789",
    "birthday": "05/05/1997",
    "post_code": "0160",
    "city": "London",
    "street": "221B Baker Street",
    "additional_numbers": [],
    "gender": "Male",
    "created_at": "2019-07-08 12:34:00 +0400",
    "updated_at": "2019-07-10 14:19:22 +0400"
}
```

`PATCH https://oneconnect.uno/api/v1/contacts`

### Request Parameters

<aside class="notice">It's not necessary to pass every parameter. You can pass only those parameters which you want to update.</aside>

Parameter | Type | Description
--------- | ---- | -----------
email | string | email of the contact
first_name | string | first name of the contact
last_name | string | last name of the contact
phone_number | string | phone number of the contact
birthday | string | birthday of the contact  (format: DD.MM.YYYY)
post_code | string | post code of the contact
city | string | city of the contact
street | string | street of the contact
additional_numbers | array of string | additional numbers of the contact separated by commas (','). Whether you put spaces after commas is entirely up to you.

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the contact
email | string | email of the contact
first_name | string | first name of the contact
last_name | string | last name of the contact
phone_number | string | phone number of the contact
birthday | string | birthday of the contact  (format: DD.MM.YYYY)
post_code | string | post code of the contact
city | string | city of the contact
street | string | city of the contact
additional_numbers | array of strings | additioanl phone numbers of the contact
gender | string | gender of the contact
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

In case of any errors you will receive the following parameters:

Parameter | Description
------- | --------
errors | array of errors

<!-- ? delete a contact -->
<!-- ? delete a contact -->
<!-- ? delete a contact -->
## Delete Contact

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/contacts/:id")
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
curl -X DELETE "https://oneconnect.uno/api/v1/contacts/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
    "error_code": 0,
    "message" : "Contact deleted."
}
```

`DELETE https://oneconnect.uno/api/v1/contacts/:id`