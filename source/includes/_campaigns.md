# 6. Campaigns

<!-- ? get campaigns -->
<!-- ? get campaigns -->
<!-- ? get campaigns -->
## Get Campaigns

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/campaigns")
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
curl -X GET "https://oneconnect.uno/api/v1/campaigns" \
     -u email:api_key
```

> JSON Response:

```json
[
    {
        "id": 4,
        "name": "Test campaign 5",
        "active": false,
        "recipients": "123456789",
        "recipients_list": [],
        "title": null,
        "content": "Hello.",
        "job_type": 0,
        "schedule": {
            "type": "scheduled-certain-dates",
            "dates": [
                "22/05/2019 17:57"
            ]
        },
        "completed": null,
        "created_at": "2019-05-22 15:56:52 +0400",
        "updated_at": "2019-05-22 15:57:07 +0400"
    },
    {
        "id": 9,
        "name": "Test campaign 3",
        "active": false,
        "recipients": "123456789, 987654321",
        "recipients_list": [
            1,
            2
        ],
        "title": "OneConnect",
        "content": "Hello, this is OneConnect.",
        "job_type": 1,
        "schedule": {
            "type": "permanent-recurring",
            "date-range": "18/06/2019 16:00",
            "repeat": "2 days"
        },
        "completed": true,
        "created_at": "2019-06-17 10:54:41 +0400",
        "updated_at": "2019-06-20 17:25:14 +0400"
    }
]
```

`GET https://oneconnect.uno/api/v1/campaigns`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the campaign
name | string | name of the campaign
active | boolean | status of the campaign
recipients | string | recipient phone phone numbers
recipients_list | array of integers | ids of the lists that are engaged in this campaign
title | string | a title which will be used as a sender name when sending messages. The title must be active or the sender name will be set to: 'Message'.
content | text | text of the messages sent by this campaign
job_type | integer | type of the campaign: 0 - scheduled, 1 - permanent. You can read more about campaigns and how they are created on the [OneConnect Manual Page](https://oneconnect.uno/manual).
schedule | hash/json | campaign scheduling. The structure of this parameter depends on the type of the campaing. You can read more about campaigns on the [OneConnect Manual Page](https://oneconnect.uno/manual).
completed | boolean | whether or not the campaign has ended
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

### You can filter campaigns by the following parameters:

Parameter | Type | Description
-------- | --------- | --------
name | boolean | filter campaigns by their names
job_type | integer | filter campaigns by their type (0 - scheduled, 1 - permanent)
title | string | filter campaigns by their title (title is a sender name which is used when sending messages)
content | text | filter campaigns by their content (content is the text of the messages sent by this campaign)

<!-- ? get a single campaign -->
<!-- ? get a single campaign -->
<!-- ? get a single campaign -->
## Get Campaign

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/campaigns/:id")
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
curl -X GET "https://oneconnect.uno/api/v1/campaigns/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
    "id": 9,
    "name": "Test campaign 3",
    "active": false,
    "recipients": "123456789, 987654321",
    "recipients_list": [
        1,
        2
    ],
    "title": "OneConnect",
    "content": "Hello, this is OneConnect.",
    "job_type": 1,
    "schedule": {
        "type": "permanent-recurring",
        "date-range": "18/06/2019 16:00",
        "repeat": "2 days"
    },
    "completed": true,
    "created_at": "2019-06-17 10:54:41 +0400",
    "updated_at": "2019-06-20 17:25:14 +0400"
}
```

Get a specific campaign with its id.

`GET https://oneconnect.uno/api/v1/campaigns/:id`

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the campaign
name | string | name of the campaign
active | boolean | status of the campaign
recipients | string | recipient phone phone numbers
recipients_list | array of integers | ids of the lists that are engaged in this campaign
title | string | a title which will be used as a sender name when sending messages. The title must be active or the sender name will be set to: 'Message'.
content | text | text of the messages sent by this campaign
job_type | integer | type of the campaign: 0 - scheduled, 1 - permanent. You can read more about campaigns and how they are created on the [OneConnect Manual Page](https://oneconnect.uno/manual).
schedule | hash/json | campaign scheduling. The structure of this parameter depends on the type of the campaing. You can read more about campaigns on the [OneConnect Manual Page](https://oneconnect.uno/manual).
completed | boolean | whether or not the campaign has ended
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

<!-- ? create a campaign -->
<!-- ? create a campaign -->
<!-- ? create a campaign -->
## Create Campaign

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/campaigns")
request = Net::HTTP::Post.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "name" => "#{name}",
    "recipients" => "#{recipients}",
    "content" => "#{content}",
    "active" => "#{active}",
    "job_type" => "#{job_type}",
    "title" => "#{title}",
    "recipients_list" => "#{recipients_list}",
    "campaign_type" => "#{campaign_type}",
    "dates" => "#{dates}",
    "repeat" => "#{repeat}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X POST "https://oneconnect.uno/api/v1/campaigns" \
     -u email:api_key \
     -d 'name=#{name}' \
     -d 'recipients=#{recipients}' \
     -d 'content=#{content}' \
     -d 'active=#{active}' \
     -d 'job_type=#{job_type}' \
     -d 'title=#{title}' \
     -d 'recipients_list=#{recipients_list}' \
     -d 'campaign_type=#{campaign_type}' \
     -d 'dates=#{dates}' \
     -d 'repeat=#{repeat}'
```

> JSON Response:

```json
{
    "id": 9,
    "name": "Test campaign 3",
    "active": false,
    "recipients": "123456789, 987654321",
    "recipients_list": [
        1,
        2
    ],
    "title": "OneConnect",
    "content": "Hello, this is OneConnect.",
    "job_type": 1,
    "schedule": {
        "type": "permanent-recurring",
        "date-range": "18/06/2019 16:00",
        "repeat": "2 days"
    },
    "completed": true,
    "created_at": "2019-06-17 10:54:41 +0400",
    "updated_at": "2019-06-20 17:25:14 +0400"
}
```

`POST https://oneconnect.uno/api/v1/campaigns`

### Request Parameters

<table>
    <thead>
        <tr>
            <th>Parameter</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
  <tbody>
        <tr>
            <td>name</td>
            <td>string</td>
            <td>name of the campaign</td>
        </tr>
        <tr>
            <td>recipients</td>
            <td>string</td>
            <td>recipient phone phone numbers</td>
        </tr>
        <tr>
            <td>content</td>
            <td>text</td>
            <td>text of the messages sent by this campaign</td>
        </tr>
        <tr>
            <td>active</td>
            <td>text</td>
            <td>status of the campaign</td>
        </tr>
        <tr>
            <td>job_type</td>
            <td>integer</td>
            <td>type of the campaign: 0 - scheduled, 1 - permanent. You can read more about campaigns and how they are created on the [OneConnect Manual Page](https://oneconnect.uno/manual).</td>
        </tr>
        <tr>
            <td>campaign_type</td>
            <td>integer</td>
            <td>campaign type should be either 0 or 1 (0 - recurring, 1 - certain dates).</td>
        </tr>
        <tr>
            <td>title</td>
            <td>string</td>
            <td>a title which will be used as a sender name when sending messages. The title must be active or the sender name will be set to: "Message".</td>
        </tr>
        <tr>
            <td>recipients_list</td>
            <td>string</td>
            <td>ids of the lists that are engaged in this campaign separated by commas (','). Whether you put spaces after commas is entirely up to you.</td>
        </tr>
        <tr>
            <td>dates, repeat</td>
            <td>string</td>
            <td>
                the value of this parameters depends on the final type of the campaign. Final type of the campaign is constructed from the job_type and campaign_type parameters and can be one of the following: scheduled-recurring, scheduled-certain-dates, permanent-recurring, permanent-certain-dates. These 2 parameters must be specified differently for each type: <br /><br />
                1. scheduled-recurrng --> both parameters are required (dates, repeat): <br />
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dates = "start_date - end_date", (e.g. "25.12.2019 15:33 - 20.04.2020 10:10", the start and end dates and times separated by dash symbol (' - ') with a single space on each side). Format - DD.MM.YYYY HH:MM <br />
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;repeat = "#{number} #{period}" (e.g. "2 days", "1 week", "10 months", "4 years". Period values: "days", "weeks", "months", "years". Number can be anything. This parameter specifies the frequency of sending messages. e.g. if you pass "3 days" the messages will be sent every 3 days starting from the start_date of the dates parameter) <br /><br />
                2. scheduled-certain-dates --> only the dates parameter (don't pass the repeat parameter!): <br />
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dates = "datetime1, datetime2, datetime3..." (e.g. "25.12.2019 15:33, 02.01.2020 10:10, 12.01.2020 20:21". Any number of date-datimes separated by commas (',')). Format - DD.MM.YYYY HH:MM <br/><br />
                3. permanent-recurrng --> both parameters are required (dates, repeat): <br />
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dates = "start_date", (e.g. "25.12.2019 15:33", only the starting date is required as this type of campaign is permanent unless you delete or deactivate it). Format - DD.MM.YYYY HH:MM <br />
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;repeat = "#{number} #{period}" (e.g. "2 days", "1 week", "10 months", "4 years". Period parameter values: "days", "weeks", "months", "years". Number can be anything) <br /><br />
                4. permanent-certain-dates --> only the dates parameter (don't pass the repeat parameter!): <br />
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dates = "datetime1, datetime2, datetime3..." (e.g. "25.12.2019 15:33, 02.01.2020 10:10, 12.01.2020 20:21". Any number of date-datimes separated by commas (',')). Format - DD.MM.YYYY HH:MM <br/>
            </td>
        </tr>
  </tbody>
</table>

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the campaign
name | string | name of the campaign
active | boolean | status of the campaign
recipients | string | recipient phone phone numbers
recipients_list | array of integers | ids of the lists that are engaged in this campaign
title | string | a title which will be used as a sender name when sending messages. The title must be active or the sender name will be set to: 'Message'.
content | text | text of the messages sent by this campaign
job_type | integer | type of the campaign: 0 - scheduled, 1 - permanent. You can read more about campaigns and how they are created on the [OneConnect Manual Page](https://oneconnect.uno/manual).
schedule | hash/json | campaign scheduling. The structure of this parameter depends on the type of the campaing. You can read more about campaigns on the [OneConnect Manual Page](https://oneconnect.uno/manual).
completed | boolean | whether or not the campaign has ended
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

Errors:

Error code | Description
-------- | ---------
3010 | Following parameters must be specified: dates, repeat.
3011 | Invalid dates.
3012 | You must specify 2 dates. (if the type is scheduled-recurring)
3013 | Invalid parameter - repeat.
3020 | Invalid ids for recipient_lists.

In case of any additional errors you will receive the following parameters:

Parameter | Description
------- | --------
errors | array of errors

<!-- ? update a campaign -->
<!-- ? update a campaign -->
<!-- ? update a campaign -->
## Update Campaign

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/campaigns")
request = Net::HTTP::Patch.new(uri)
request.basic_auth("email", "api_key")
request.set_form_data(
    "name" => "#{name}",
    "recipients" => "#{recipients}",
    "content" => "#{content}",
    "active" => "#{active}",
    "title" => "#{title}",
    "recipients_list" => "#{recipients_list}"
)

req_options = {
    use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
    http.request(request)
end
```

```shell
curl -X PATCH "https://oneconnect.uno/api/v1/campaigns" \
     -u email:api_key \
     -d 'name=#{name}' \
     -d 'recipients=#{recipients}' \
     -d 'content=#{content}' \
     -d 'active=#{active}' \
     -d 'title=#{title}' \
     -d 'recipients_list=#{recipients_list}'
```

> JSON Response:

```json
{
    "id": 9,
    "name": "Test campaign 3",
    "active": false,
    "recipients": "123456789, 987654321",
    "recipients_list": [
        1,
        2
    ],
    "title": "OneConnect",
    "content": "Hello, this is OneConnect.",
    "job_type": 1,
    "schedule": {
        "type": "permanent-recurring",
        "date-range": "18/06/2019 16:00",
        "repeat": "2 days"
    },
    "completed": true,
    "created_at": "2019-06-17 10:54:41 +0400",
    "updated_at": "2019-06-20 17:25:14 +0400"
}
```

`PATCH https://oneconnect.uno/api/v1/campaigns`

### Request Parameters

<aside class="notice">It's not necessary to pass every parameter. You can pass only those parameters which you want to update. Campaign type and schedule can't be updated.</aside>

Parameter | Type | Description
--------- | ---- | -----------
name | string | name of the campaign
recipients | string | recipient phone phone numbers
content | text | text of the messages sent by this campaign
active | text | status of the campaign
title | string | a title which will be used as a sender name when sending messages. The title must be active or the sender name will be set to: "Message".
recipients_list | string | ids of the lists that are engaged in this campaign separated by commas (','). Whether you put spaces after commas is entirely up to you.

### Response Parameters

Parameter | Type | Description
--------- | ----------- | ----------
id | integer | ID of the campaign
name | string | name of the campaign
active | boolean | status of the campaign
recipients | string | recipient phone phone numbers
recipients_list | array of integers | ids of the lists that are engaged in this campaign
title | string | a title which will be used as a sender name when sending messages. The title must be active or the sender name will be set to: 'Message'.
content | text | text of the messages sent by this campaign
job_type | integer | type of the campaign: 0 - scheduled, 1 - permanent. You can read more about campaigns and how they are created on the [OneConnect Manual Page](https://oneconnect.uno/manual).
schedule | hash/json | campaign scheduling. The structure of this parameter depends on the type of the campaing. You can read more about campaigns on the [OneConnect Manual Page](https://oneconnect.uno/manual).
completed | boolean | whether or not the campaign has ended
created_at | timestamp | date of creation
updated_at | timestamp | date of the last update

Errors:

Error code | Description
-------- | ---------
3020 | Invalid ids for recipient_lists.

In case of any additional errors you will receive the following parameters:

Parameter | Description
------- | --------
errors | array of errors

<!-- ? delete a campaign -->
<!-- ? delete a campaign -->
<!-- ? delete a campaign -->
## Delete Campaign

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://oneconnect.uno/api/v1/campaigns/:id")
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
curl -X DELETE "https://oneconnect.uno/api/v1/campaigns/:id" \
     -u email:api_key
```

> JSON Response:

```json
{
    "error_code": 0,
    "message" : "Campaign deleted."
}
```

`DELETE https://oneconnect.uno/api/v1/campaigns/:id`