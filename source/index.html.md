---
title: OneConnect API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby

toc_footers:
  - <a href='https://oneconnect.uno/users/sign_up'>Sign Up for an API Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - sms
  - contacts
  - lists
  - campaigns
  - birthday_campaigns
  - titles
  - templates
  - info
  - additional_stuff
  - errors

search: true
---

# 1. Introduction

Welcome to the OneConnect API. The API enables you to integrate your application with messaging platform. You can check all the features of OneConnect in the documentation below or on our [home page](https://oneconnect.uno).


## How to start
To start using OneConnect API you need to create an account on the OneConnect website. Registration is completely free. After creating an account you will be granted a 15-day free trial and 30 SMS messages to test our platform.

## IP Restrictions

In order to improve the security of the API, you can create a whitelist of IP addresses on your profile page. Every HTTP requrest will be accepted only from those IPs. Every request sent from a different IP address will be rejected.

For now the service of IP restriction is only avalable to customers with Business plan.

# 2. Authentication

> To authorize, use this code:

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("https://api.example.com/")
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
# With shell, you can just pass the correct header with each request
curl "https://api.example.com/"
     -u email:api_key
```

> Make sure to replace `email` and `api_key` with your personal credentials.

We use API keys to allow access to the API. Every requets requires basic authentication with your email address and unique API key provided on your [profile page](https://oneconnect.uno/sms/account).

<aside class="notice">
Make sure to replace <code>email</code> and <code>api_key</code> with your personal credentials.
</aside>