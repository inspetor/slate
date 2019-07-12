---
title: Inspetor Docs

language_tabs: # must be one of https://git.io/vQNgJ
  - php

includes:
  - exception

search: true
---

# Introduction

Inspetor protects your company from losses due to fraud and chargebacks, all while maximizing revenue from valid purchases and maintaining the simple payment flow that your customers love. We accomplish this by making predictions based on past and present user behavior to evaluate the likelihood that a transaction is fraudulent.

But we can't do it alone--we need *you*, the user, to integrate our library into your code base so we can capture sufficient information to train our models. The more information we receive, the better the decision we can make, and the better we can protect your platform from fraud.

What follows is a general guide of how to integrate Inspetor's Client Library into your product. It should be sufficient for you to start with your Inspetor product integration. Should you find yourself in need of further assistance, do not hesitate to reach out to the Inspetor team--we will be happy to help!

# Installing the Client Library


```php
~ composer require inspetor/inspetorphp:${version}
```

The Inspetor collection libraries are avaible via public standard package managers for the following supported languages:

- PHP (via <a href="https://packagist.org/packages/inspetor/inspetor-php">Composer</a>)


# Client Library Setup

```php
<?php

use Inspetor;

$inspetor_config = [
  "appId"       => [your appId] # (e.g. '30cdfed3-9f7f-4aaa-b9f1-033c4dbfef58'),
  "trackerName" => [your trackerName] # (e.g. 'company.api')
];

$inspetor = new InspetorClient($inspetor_config);

?>
```

The first step of integrating Inspetor's antifraud services into your product is instantiating the library.

In order to do so, you will need to pass the `InspetorClient` your product's **App ID** and **Tracker Name**, both of which will be provided to you by the Inspetor Team.

_Et voilà_! You now have an Inspetor client object that is capable of sending all of the information necessary to teach Inspetor's decision layer how to prevent fraud at your company. However, there is a difference between instantiating a client instance and using it properly.

# Using the Client Library

In order to protect your company from fraudsters, our decision models need to be informed with customer behavior.

Events like logins, profile updates, or even unrelated purchases on the same account all contribute to our assessment of whether or not a given transaction is fraudulent. But we can't do it alone--we need _you_, our client, to send this information to us via the Client Library so that we can make better-informed decisions.

At a high level, our decision model understands the e-commerce world in the following primary terms:

- <a href="#inspetoraccount">**Accounts**</a>
- <a href="#inspetorevent">**Events**</a>
- <a href="#inspetorsale">**Sales**</a>
- <a href="#inspetoritem">**Sale Items**</a>
- <a href="#inspetortransfer">**Transfers**</a>

You can think of the relationship between those entities something like this:

If a user purchases tickets for a show on your site, Inspetor interprets the action as:

- the creation of a new <a href="#inspetorsale">*Sale*</a>
- the association of that Sale with an existing <a href="#inspetoraccount">*Account*</a>
- the association of that Sale with an <a href="#inspetoritem">*Item*</a>
- the association of that Item with an existing <a href="#inspetorevent">*Event*</a>

While these are the terms with which our model interprets actions on your platform, Inspetor is unaware of these actions occurring unless you use the Inspetor Client Library to relay this information to us.

<aside class="notice">
Inspetor will never request access to your code base--that means that it is on <i>you</i>, the developer, to integrate our library into your product's code base. We think that's the right way to do things: you know your product's code base, we know fraud.
</aside>

## When to send events to Inspetor

The primary Inspetor entities are **stateful** objects. They have properites that can be updated, and the values of these properties are crucial to our evaluation of transaction validity. Thus, you should send events to Inspetor via the client library whenever properties of these objects are changed.

However, if we base our evaluation upon outdated or incorrect information, the accuracy of our evaluation will suffer. As such, it is critical that you notify Inspetor of any changes to these properties whenever they occur via the Inspetor Client Library.

<aside class="warning">
It is <b>extremely important</b> that you provide us with updated information at any stage that these primary entities are updated. If we are working with outdated or incorrect information, we can't make reliable predictions for you.
</aside>

The Inspetor Client Library provides methods for you to relay state changes to primary entities in any of the following instances:

### Account
- When an account is <a href="#account-creation">created</a>
- When an account is <a href="#account-updates">updated</a>
- When an account is <a href="#account-deletion">deleted</a>

### Event
- When an event is <a href="#event-creation">created</a>
- When an event is <a href="#event-updates">updated</a>
- When an event is <a href="#event-deletion">deleted</a>

### Transfer
- When a request to transfer a sale item (e.g. a ticket) is <a href="#transfer-creation">created</a>
- When a request to transfer a sale item (e.g. a ticket) is <a href="#transfer-updates">updated</a>

### Sale
- When a sale is <a href="#sale-creation">created</a>
- When a sale is <a href="#sale-updates">updated</a>


Inspetor provides additional methods to allow you to inform us about meaningful user activity, such as:

### Login/Logout
- When a user <a href="#account-login">logs in to an account</a>
- When a user <a href="#account-logout">logs out of an account</a>

### Password Activity
- When a user requests to <a href="#password-recovery">recover</a> their password
- When a user <a href="#password-reset">resets</a> their password

## Where to insert Inspetor collection functions
Where in your code base does the Inspetor client library belong? Frontend? Backend? Loaded on the site?

Fortunately for you, the answer is quite simple at the moment--we only have one version (PHP) of the Client Library implemented! That means you'll need to integrate our library with your PHP application server.

In the future however, our suggested integration model will be:

- Full event coverage within the server/API level of your application (backend): This allows us to know everything about what is hapening within your product.
- 1:1 corresponding coverage within your frontend interfaces (Web, iOS, and Android): This allows us to enrich the knowledge we're gathering from your server-level transactions with additional information that improves our protection capabilities.

You can find additional language-specific implementation details, including suggested architecture and best practices, via the following links:

- [PHP](https://github.com/inspetor/inspetorphp/blob/master/README.md)

## Testing your integration with Inspetor

Integrating with Inspetor is meant to be easy--simply instantiate our library, call our tracking methods, and if there are no errors thrown within your code execution, data will appear within our database. However, for further validation, we also provide our customers with limited-access database credentials that allow the developer in charge of integrating Inspetor to inspect the that data appears in our database. (Note that access is restricted such that your customer account will only be able to view data originating from your company's integration.) The Inspetor team will provide you with access credentials for this phase of validation.

However, ensuring that some data is making its way into our database is not sufficient for validating an Inspetor integration. We need to ensure that our understanding of state updates to primary entities (such as sales or accounts) remains accurate over time. This means that after the initial integration of our client library into your production code, we will need to periodically validate that our representation of sales, accounts, etc. corresponds to the true state of those entities (as represented in the customer database). This phase of validation is highly customer-specific and it will involve coordinated effort from both the customer and the Inspetor integration team.

# Collection API

<aside class="notice">
To access the following library functions, you will need an instance of the InspetorClient class. All functions are accessed through the client instance.
</aside>
## Account Activity

The following functions will be used to relay actions associated with an account:

- <a href="#account-creation">trackAccountCreation</a>
- <a href="#account-updates">trackAccountUpdate</a>
- <a href="#account-deletion">trackAccountDeletion</a>

All the functions for tracking account-related actions require an [InspetorAccount](#inspetoraccount) object as an argument and return `true` upon successful execution. Otherwise, one of the following exceptions will be thrown:

Exception | Description
--------- | -----------
**[AccountException](#accountexception)**   | The Account object provided is not a valid Inspetor Account
**[AddressException](#addressexception)**   | The Address object provided as a property of the Account object invalid
**[generalException](#generalException)** | The timestamps passed as Account object properties are invalid
**[TrackerException](#trackerexception)**   | An internal error occurred (*This should never happen*)


### Account Creation

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackAccountCreation($account);

?>
```

Notify Inspetor any time a new user account is created.

Argument | Type | Description
-------- | ---- | -----------
account  | Inspetor/Model/[InspetorAccount](#inspetoraccount) | The Account that is being created


### Account Updates

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackAccountUpdate($account);

?>
```

Send information to Inspetor any time an account's information (email, address, name...) is altered.

Argument | Type | Description
-------- | ---- | -----------
account  | Inspetor/Model/[InspetorAccount](#inspetoraccount) | The Account that is being updated


### Account Deletion

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackAccountDeletion($account);

?>
```

Send information to Inspetor any time an account is deleted.

Argument | Type | Description
-------- | ---- | -----------
account  | Inspetor/Model/[InspetorAccount](#inspetoraccount) | The Account that is being deleted

## Authentication Activity

The following functions provide Inspetor with information on when a user logs in our out of an account within your product:

- <a href="#account-login">trackLogin</a>
- <a href="#account-logout">trackLogout</a>

All functions for tracking authentication activity require an [InspetorAuth](#inspetorauth) object as an argument and return `true` upon successful execution. Otherwise, one of the following exceptions will be thrown:

Exception | Description
--------- | -----------
**[AuthException](#authexception)**          | The Auth object provided is invalid
**[generalException](#generalException)**  | The timestamps passed as Auth object properties are invalid
**[TrackerException](#trackerexception)**    | An internal error occurred (*This should never happen*)

### Account Login

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackLogin($auth);

?>
```

Send information to Inspetor on every login attempt

Argument | Type | Description
-------- | ---- | -----------
auth  | Inspetor/Model/[InspetorAuth](#inspetorauth) | The Auth object that describes the login


### Account Logout

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackLogout($auth);

?>
```

Send information to Inspetor everytime an account (*e.g. user*) logs out.

Argument | Type | Description
-------- | ---- | -----------
auth  | Inspetor/Model/[InspetorAuth](#inspetorauth) | The Auth object that describes the logout

## Password Activity

The following functions notify Inspetor of password changes initiated by  users within your platform, independent of whether the user is logged in or not:

- <a href="#password-reset">trackPasswordReset</a>
- <a href="#password-recovery">trackPasswordRecovery</a>

All functions for tracking authentication events require an [InspetorPassRecovery](#inspetorpassrecovery) object as an argument and return `true` upon successful execution. Otherwise, one of the following exceptions will be thrown:

Exception | Description
--------- | -----------
**[PassRecoveryException](#passrecoveryexception)** | The PassRecovery object provided is invalid
**[generalException](#generalException)**         | The timestamps passed as PassRecovery object properties are invalid
**[TrackerException](#trackerexception)**           | An internal error occurred (*This should never happen*)

### Password Reset

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackPasswordReset($pass_recovery);

?>
```

Send information to Inspetor anytime a request to reset an account's password is made.

Argument | Type | Description
-------- | ---- | -----------
pass_recovery | Inspetor/Model/[InspetorPassRecovery](#inspetorpassrecovery) | The PassRecovery object that describes the password reset request

### Password Recovery

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackPasswordRecovery($pass_recovery);

?>
```

Send information to Inspetor anytime a request is made to recover a password.

Argument | Type | Description
-------- | ---- | -----------
pass_recovery | Inspetor/Model/[InspetorPassRecovery](#inspetorpassrecovery) | The PassRecovery object that describes the password recovery request

## Event Activity

The following functions provide Inspetor with information regarding the events (*e.g. parties, shows...*) listed on your platform:

- <a href="#event-creation">trackEventCreation</a>
- <a href="#event-updates">trackEventUpdate</a>
- <a href="#event-deletion">trackEventDeletion</a>

All functions for tracking event activity require an [InspetorEvent](#inspetorevent) object as argument and return `true` upon successful execution. Otherwise, one of the following exceptions will be thrown:

Exception | Description
--------- | -----------
**[EventException](#eventexception)**       | The Event object provided is invalid
**[AddressException](#addressexception)**   | The Address object provided as a property of the Event object is invalid
**[generalException](#generalException)** | The timestamps passed as Event object properties are invalid
**[TrackerException](#trackerexception)**   | An internal error occurred (*This should never happen*)

### Event Creation

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackEventCreation($event);

?>
```

Send information to Inspetor anytime a new event (*e.g. pary, shows...*) is created in your platform

Argument | Type | Description
-------- | ---- | -----------
event | Inspetor/Model/[InspetorEvent](#inspetorevent) | The Event that is being created

### Event Updates

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackEventUpdate($event);

?>
```

Send information to Inspetor everytime an event listing's information is updated (event title, location, etc.)

Argument | Type | Description
-------- | ---- | -----------
event | Inspetor/Model/[InspetorEvent](#inspetorevent) | The Event that is being updated

### Event Deletion

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackEventDeletion($event);

?>
```

Send information to Inspetor everytime an Event listing is deleted from your platform

Argument | Type | Description
-------- | ---- | -----------
event | Inspetor/Model/[InspetorEvent](#inspetorevent) | The Event that is being deleted

## Sale Activity

The following functions provide Inspetor with information on sales that happen within your platform. The main activities that we track are the following:

- <a href="#sale-creation">trackSaleCreation</a>
- <a href="#sale-updates">trackSaleUpdate</a>

All functions for tracking Sales activity require a [InspetorSale](#inspetorsale) object as an argument and return `true` upon successful execution. Otherwise, one of the following exceptions will be thrown:

Exception | Description
--------- | -----------
**[SaleException](#saleexception)**         | The Transfer object provided is not a valid one
**[ItemException](#itemexception)**         | The Item object provided on the Sale is not a valid one
**[PaymentException](#paymentexception)**   | The Payment object provided on the Sale is not a valid one
**[generalException](#generalException)** | The timestamps that you passed on the objects are not valid ones
**[TrackerException](#trackerexception)**   | An internal error occurred *Hopefully this never happen*

### Sale Creation

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackSaleCreation($sale);

?>
```

Send information to Inspetor every time a new sale is created on your platform.

Argument | Type | Description
-------- | ---- | -----------
sale | Inspetor/Model/[InspetorSale](#inspetorsale) | The Sale that is being created

### Sale Updates

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackSaleUpdate($sale);

?>
```

Send information to Inspetor everytime a sale's status is updated.
<aside class="notice">
You must call this function <b>any</b> time a sale's status is updated (including post-sale updates, such as refunds). Sale status is extremely crucial to Inspetor's prediction model.
</aside>

Argument | Type | Description
-------- | ---- | -----------
sale | Inspetor/Model/[InspetorSale](#inspetorsale) | The Sale that is being updated

## Items Transfers

The following functions will be used to relay item (*e.g. ticket*) transfers between users (*e.g. accounts*) that happen within your platform:

- **Item Transfer Creation** (*trackItemTransferCreation*)
- <a href="#transfer-creation">trackTransferCreation</a>
- <a href="#transfer-updates">trackTransferUpdate</a>
- **Item Transfer Update** (*trackItemTransferUpdate*)

All the functions for tracking transfer activity require a [InspetorTransfer](#inspetortransfer) object as argument and return `true` if everything goes right. Otherwise, one of the the following exceptions will be thrown:

Exception | Description
--------- | -----------
**[TransferException](#transferexception)**  | The Transfer object provided is not a valid one
**[generalException](#generalException)**  | The timestamps that you passed on the objects are not valid ones
**[TrackerException](#trackerexception)**    | An internal error occurred *Hopefully this never happen*

### Transfer Creation

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackItemTransferCreation($transfer);

?>
```

This function is used to send information to Inspetor everytime a new item (*e.g. ticket*) transfer is created on your platform.

Argument | Type | Description
-------- | ---- | -----------
transfer | Inspetor/Model/[InspetorTransfer](#inspetortransfer) | The Transfer that is being created

### Transfer Updates

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

$inspetor>trackItemTransferUpdate($transfer);

?>
```

This function is used to send information to Inspetor everytime an item (*e.g. ticket*) transfer's status is updated.

Argument | Type | Description
-------- | ---- | -----------
transfer | Inspetor/Model/[InspetorTransfer](#inspetortransfer) | The Transfer that is being updated

# Models

The Inspetor Library provides a set of classes that are used to structure the information required by our fraud prevention platform.

In our current PHP implementation, we suggest using the pre-built `get` accessor methods that are available in the InspetorClient class to get an instance of a given class. Thus you can access every model without having to import every class.

<aside class="notice">
Most models have some optional properties, but it's important that you try to send us as much information as you can. The more information our models have to work with, the better your results will be.
</aside>


## InspetorAccount

Information about a user's account.

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_account = $inspetor>getInspetorAuth();

// Filling model with company data
$inspetor_account->setId("123"); //getId()
$inspetor_account->setName("Test Name"); //getName()
$inspetor_account->setEmail("test@email.com"); //getEmail()
$inspetor_account->setDocument("07206094880"); //getDocument()
$inspetor_account->setPhoneNumber("11953891736"); //getPhoneNumber()
$inspetor_account->setAddress($inspetor_address); //getAddress()
$inspetor_account->setTimestamp(time()); //getTimestamp()

?>
```

All properties can be accesssed or defined via `get` and `set` accessor methods

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | Your unique indentifier for this account in your platform
**email** | Yes | String | The email associated with the account
**timestamp** | Yes | Integer | The Unix-formatted datetime that the account was last updated
name | No | String | The name of the user
document | No | String | The CPF or document number associated with the account
phone_number | No | String | The phone number associated with the account
address | No | [Address](#address) | The address associated with the account

## InspetorAddress

Residential or billing address information that is used in other models ([InspetorAccount](#inspetoraccount), [InspetorEvent](#inspetorevent) and [InspetorCreditCard](#inspetorcreditcard)).

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_address = $inspetor>getInspetorAddress();

// Filling model with company data
$inspetor_address->setStreet("Street Security");  //getStreet()
$inspetor_address->setNumber("123"); //getNumber()
$inspetor_address->setZipCode("05511010"); //getZipCode()
$inspetor_address->setCity("Test City"); //getCity()
$inspetor_address->setState("Test State"); //getState()
$inspetor_address->setCountry("Test Country"); //getCountry()
$inspetor_address->setLatitude("123"); //getLatitude()
$inspetor_address->setLongitude("123"); //getLongitude()

?>
```

All properties can be accesssed or defined via `get` and `set` accessor methods

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**street** | Yes | String | The street of the address
**zip_code** | Yes | String | The zip code (*e.g. CEP*) of the address
**city** | Yes | String | The city in which the address is located
**state** | Yes | String | The state in which the address is located
**country** | Yes | String | The country in which the address is located
number | No | String | The street number of the address
latitude | No | String | The exact latitude of the address
longitude | No | String | The exact longitude of the address

## InspetorAuth

Login and logout event information in your platform

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_auth = $inspetor>getInspetorAuth();

// Filling model with company data
$inspetor_auth->setAccountId("123"); //getAccountId()
$inspetor_auth->setTimestamp(time()); //getTimestamp()

?>
```

All properties can be accesssed or defined via `get` and `set` accessor methods

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**account_id** | Yes | String | The id of the user that is making the login or logout
**timestamp** | Yes | Integer | The unix format of the time and date that the authentication happend

## InspetorCategory

Event categories that are used in the [InspetorEvent](#inspetorevent) model.

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_category = $inspetor>getInspetorCategory();

// Filling model with company data
$inspetor_category->setId("123"); //getId()
$inspetor_category->setName("Category"); //getName()

?>
```

All properties can be accesssed or defined via `get` and `set` accessor methods

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | Your unique indentifier for this category in your platform
**name** | Yes | String | The name of the category

## InspetorCreditCard

Credit card information (used in [InspetorSales](#inspetorsale) ).

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_cc = $inspetor>getInspetorCreditCard();

// Filling model with company data
$inspetor_cc->setFirstSixDigits("123456"); //getFirstSixDigits()
$inspetor_cc->setLastFourDigits("1234"); //getLastFourDigits()
$inspetor_cc->setHolderName("Holder Name"); //getHolderName()
$inspetor_cc->setHolderCpf("07206094880"); //getHolderCpf()
$inspetor_cc->setBillingAddress($inspetor_address); //getBillingAddress

?>
```

All properties can be accesssed or defined via `get` and `set` accessor methods

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**first_six_digits** | Yes | String | The first six digits of the credit card number
**last_four_digits** | Yes | Integer | The last four digits of the credit card number
**holder_name** | Yes | String | The full name of the owner of the credit card
**holder_cpf** | Yes | String | The CPF of the owner of the credit card
**billing_address** | Yes | [InspetorAddress](#inspetoraddress) | The billing address associated with this credit card

## InspetorEvent

The Event Model will contain information about parties, shows, and events that are listed on your platform

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_event = $inspetor>getInspetorEvent();

// Filling model with company data
$inspetor_event->setId("8000"); //getId()
$inspetor_event->setName("Name Test"); //getName()
$inspetor_event->setDescription("Description Test"); //getDescription()
$inspetor_event->setTimestamp(time()); //getTimestamp()
$inspetor_event->setSessions($inspetor_session); //getSession()
$inspetor_event->setStatus("private"); //getStatus()
$inspetor_event->setCategories([$inspetor_category1, $inspetor_category2]); //getCategories()
$inspetor_event->setIsPhysical(true); //getIsPhysical()
$inspetor_event->setAddress($inspetor_address); //getAddress()
$inspetor_event->setSlug("cool-company-event"); //getSlug()
$inspetor_event->setCreatorId("123"); //getCreatorId()
$inspetor_event->setAdminsId(["123", "234"]); //getAdminsId()
$inspetor_event->setSeatingOptions(["Pista", "VIP"]); //getSeatingOptions()

?>
```

All properties can be accesssed or defined via `get` and `set` accessor methods

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | The unique indentifier of this event listing in your platform
**name** | Yes | String | The name of the event
**is_physical** | Yes | Bool | It determines if it's a physical or digital event. *The default value is `true`.*
**sessions** | Yes | Array of [InspetorSession](#inspetorsession) | All available dates and times that the event occurs (if it has more than one) and a unique id for each date/time.
**creator_id** | Yes | String | The id of the user who created the event
**admins_id** | Yes | Array | An array containing the ids of all users who can make changes to the event
**timestamp** | Yes | Integer | The Unix-formatted datetime that the event was last updated
address | No | [InspetorAddress](#inspetoraddress) | The address where the event is happening. *This field is only required if the type of the event is set to physical.*
status | No| String | The status of the event. *Inspetor provides some pre-built statuses (draft, private and published) but you can provide a custom status if you it does not fit with our status model.*
description | No | String | A description of the event
seating_options | No | Array | An array containing all names of the different ticket types that can be bought for this event
categories | No | Array of [InspetorCategory](#inspetorcategory) | An array of categories associated with the event listing
slug | No | String | The slug of the event

## InspetorItem

Information about the item(s) (generally a ticket) associated with a [InspetorSale](#inspetorsale).

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_item = $inspetor>getInspetorItem();

// Filling model with company data
$inspetor_item->setId("9000"); //getId()
$inspetor_item->setEventId("8000"); //getEventId()
$inspetor_item->setSessionId("124"); //getSessionId()
$inspetor_item->setPrice(50.0); //getPrice()
$inspetor_item->setSeatingOption("PISTA"); //getSeatingOption()
$inspetor_item->setQuantity(2); //getQuantity()

?>
```

All properties can be accesssed or defined via `get` and `set` accessor methods

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | A unique indentifier for this item (*e.g. ticket*) within your platform
**event_id** | Yes | String | The unique indentifier of the event that the item is tied too
**session_id** | Yes | String | The unique indentifier of the event session (date and time) that the item is tied to
**price** | Yes | Double | The price of the item. *It should only contain numbers, dots and commas*
**quantity** | Yes | Integer | The number of item of this type being bought.
seating_option | No | String | The name of the type of item that is being bought

## InspetorPassRecovery

Information about password change requests or recoveries initiated by a user.

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_pass = $inspetor>getInspetorPassRecovery();

// Filling model with company data
$inspetor_pass->setRecoveryEmail("test@email.com"); //getRecoveryEmail()
$inspetor_pass->setTimestamp(time()); //getTimestamp()

?>
```

All properties can be accesssed or defined via `get` and `set` accessor methods

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**recovery_email** | Yes | String | The email used to recover or reset the password
**timestamp** | Yes | String | The Unix-formatted datetime when the action occurred.

## InspetorPayment

Information about the payment associated with a [InspetorSale](#inspetorsale).

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_payment = $inspetor>getInspetorPayment();

// Filling model with company data
$inspetor_payment->setId("12345"); //getId()
$inspetor_payment->setMethod("credit_card"); //getMethod()
$inspetor_payment->setInstallments(1); //getInstallments()
$inspetor_payment->setCreditCard($inspetor_cc); //getCreditCard()

?>
```

All properties can be accesssed or defined via `get` and `set` accessor methods

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | The id of the payment. This id should be the same as the one you send to the payment processor.
**method** | Yes | String | The method of payment being used. *The allowed values are `credit_card`, `boleto`, and `other`*
**installments** | Yes | Integer | The number of "*parcelas*" that the user will pay
credit_card | No | [InspetorCreditCard](#inspetorcreditcard) | If the method is *credit_card* it should contains a credit card object

## InspetorSale

Information about a sale within your platform.

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_sale = $inspetor>getInspetorSale();

// Filling model with company data
$inspetor_sale->setId("1234"); //getId()
$inspetor_sale->setAccountId("123"); //getAccountId()
$inspetor_sale->setStatus("pending"); //getStatus()
$inspetor_sale->setIsFraud(false); //getIsFraud()
$inspetor_sale->setTimestamp(time()); //getTimestamp()
$inspetor_sale->setItems([$inspetor_item1, $inspetor_item2]); //getItems()
$inspetor_sale->setPayment($inspetor_payment); //getPayment()

?>
```

All properties can be accesssed or defined via `get` and `set` accessor methods

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | The unique indentifier for the sale within your platform
**account_id** | Yes | String | The id of the user who is making the purchase
**status** | Yes | String | The status of the sale. *The allowed values are: `accepted`, `declined`, `pending`, `refunded`, and `manual_analysis`*
**is_fraud** | Yes | Boolean | Indicates if the sale was fradulent. This should only be `true` when a sale was declined or refunded by antifraud services, or if a chargeback was received for a processed transaction.
**timestamp** | Yes | Integer | The unix format of the time and date that the action happend
**items** | Yes | Array of [InspetorItem](#inspetoritem) | The items (*e.g. tickets*) that are being bought
**payment** | Yes | [InspetorPayment](#inspetorpayment) | The payment used in this purchase


## InspetorSession

Event session that are used in the [InspetorEvent](#inspetorevent) model.

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_session = $inspetor>getInspetorSession();

// Filling model with company data
$inspetor_session->setId("123"); //getId()
$inspetor_session->setDatetime(1234); //getDatetime()

?>
```

All properties can be accesssed or defined via `get` and `set` accessor methods

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | Your unique indentifier for this session in your platform
**datetime** | Yes | String | The date and time of the event session 


## InspetorTransfer

Information regarding the transfer of purchased [InspetorItems](#inspetoritem) (*e.g. tickets*) within your platform.

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_transfer = $inspetor>getInspetorTransfer();

// Filling model with company data
$inspetor_transfer->setId("123"); //getId()
$inspetor_transfer->setTimestamp(time()); //getTimestamp()
$inspetor_transfer->setItemId("9000"); //getItemId()
$inspetor_transfer->setSenderAccountId("124"); //getSenderAccountId()
$inspetor_transfer->setReceiverEmail("test@email.com"); //getReceiverEmail()
$inspetor_transfer->setStatus("pending"); //getStatus()

?>
```

All properties can be accesssed or defined via `get` and `set` accessor methods

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | Your platform-unique indentifier for the transfer
**item_id** | Yes | String | The id of the [InspetorItem](#inspetoritem) (*e.g. ticket*) that is being transfered
**sender_account_id** | Yes | String | The id of the account who is transferring the item (*e.g. ticket*)
**receiver_email** | Yes | String | The email of the user who is receiving the item (*e.g. ticket*)
**timestamp** | Yes | Integer | The Unix-formatted datetime that the action happend
**status** | Yes | String | The status of the transfer. *The allowed values are: `accepted`, `rejected`, and `pending`*


