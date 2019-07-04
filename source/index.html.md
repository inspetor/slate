---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - php

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Installing the Library


```php
~ composer require inspetor/inspetor-php:[version]
```

> Make sure to replace `[version]` with the most recent library

Our libraries can be found in all the package managers of our supported languages.

<aside class="notice">
You can find the last version of our libraries <a href="https://localhost:4567">here</a>.
</aside>


# Library Setup

```php
<?php

use Inspetor;

$inspetor_config = [
  "appId"       => [your appId] (e.g. company.api),
  "trackerName" => [your trackerName] (e.g. 30cdfed3-9f7f-4aaa-b9f1-033c4dbfef58)
];

$inspetor = new Inspetor($inspetor_config);

?>
```

To setup an Inspetor Library in any language you first need to set some configuration. 

You will need to pass to the library your "AppId" and a "TrackerName", both will be provided to you by the Inspetor Team.

<aside class="notice">
You can find language specific details <a href="localhost:4567">here</a>.
</aside>


# Trackers

The Inspetor Library provides a set of functions that are used to track activities that happen in your application. 

All the information that is collected will help our models indentify frauds. Because of that is super important that they are will cofigured.

## Tracking Account Activities

These are the functions that will be used to track the user inside your application. The main activities that we track for user are the followings:

- Account Creation
- Account Updates
- Account Deletion

### Tracking Account Creation

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackAccountCreation($account);

?>
```

This function is used to send information to Inspetor everytime a new account(e.g user) is created in your plataform.

This function takes an [Account]() object as argument and will return true if everything goes right. If we get any problem it will throw an exception of one of the following types:

- **AccountException** (Meaning that your Account object was not valid)

- **AddressException** (Meaning that your Address object inside the Account object was not valid)

- **TrackException**   (Meaning that we had an internal error. *Hopefully this never happen*)


### Tracking Account Update

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackAccountUpdate($account);

?>
```

This function is used to send information to Inspetor everytime an account(e.g user) updates an 

This function takes an [Account]() object as argument and will return true if everything goes right. If we get any problem it will throw an exception of one of the following types:

- **AccountException** (Meaning that your Account object was not valid)

- **AddressException** (Meaning that your Address object inside the Account object was not valid)

- **TrackException**   (Meaning that we had an internal error. *Hopefully this never happen*)


### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

