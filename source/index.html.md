---
title: Inspetor Docs

language_tabs: # must be one of https://git.io/vQNgJ
  - php

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - exception

search: true
---

# Introduction

Inspetor is a product developed to help your company avoid fraudulent transactions. 

# Installing the Library


```php
~ composer require inspetor/inspetor-php:[version]
```

> Make sure to replace `[version]` with the most recent library

Our libraries can be found in all the package managers of our supported languages.

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>


# Library Setup

```php
<?php

use Inspetor;

$inspetor_config = [
  "appId"       => [your appId] (e.g. company.api),
  "trackerName" => [your trackerName] (e.g. 30cdfed3-9f7f-4aaa-b9f1-033c4dbfef58)
];

$inspetor = new InspetorClient($inspetor_config);

?>
```

To setup an Inspetor Library in any language you first need to set some configuration. 

You will need to pass to the library your **"AppId"** and a **"TrackerName"**, both will be provided to you by the Inspetor Team.

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

# Trackers

The Inspetor Library provides a set of functions that are used to track activities that happen in your application. 

**To access all the trackers you will need an instance of the InspetorClient class**, since they are all available there.

All the information that is collected will help our models indentify frauds. Because of that is super important that they are will cofigured.

## Tracking Account Activities

These are the functions that will be used to track the user (*e.g. account*) inside your application. The main activities that will be tracked are the followings:

- **Account Creation** (*trackAccountCreation*)
- **Account Updates** (*trackAccountUpdate*)
- **Account Deletion** (*trackAccountDeletion*)

All the functions for tracking accounts (*e.g. user*) **will receive an [Account](#account) object as argument** and will *return true* if everything goes right. Otherwise they will throw one of the following exceptions:

Exception | Description
--------- | -----------
**[AccountException](#accountexception)**   | The Account object provided is not a valid one
**[AddressException](#addressexception)**   | The Address object provided in the Account object is not a valid one
**[AbstractException](#abstractexception)** | The timestamps that you passed on the objects are not valid ones
**[TrackerException](#trackerexception)**   | An internal error occured. *Hopefully this never happen*

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>


### Tracking Account Creation

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackAccountCreation($account);

?>
```

This function is used to send information to Inspetor everytime a new account (*e.g. user*) is created on your plataform.

Argument | Type | Description
-------- | ---- | -----------
account  | Inspetor/Model/[Account](#account) | The Account that is being created


### Tracking Account Update

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackAccountUpdate($account);

?>
```

This function is used to send information to Inspetor everytime an account (*e.g. user*) updates it's informations (email, address, name...) on your application.

Argument | Type | Description
-------- | ---- | -----------
account  | Inspetor/Model/[Account](#account) | The Account that is being updated


### Tracking Account Deletion

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackAccountDeletion($account);

?>
```

This function is used to send information to Inspetor everytime an account (*e.g. user*)  it's deleted on your platform.

Argument | Type | Description
-------- | ---- | -----------
account  | Inspetor/Model/[Account](#account) | The Account that is being deleted

## Tracking Authetication Activities

These are the functions that will be used to track authentications (*e.g. logins and logouts*) that happen in your platform. The main activities that we track are the following:

- **Login** (*trackLogin*)
- **Logout** (*trackLogout*)

All the functions for tracking authentications will **receive an [Auth](#auth) object as argument** and will *return true* if everything goes right. Otherwise they will throw one of the following exceptions:

Exception | Description
--------- | -----------
**[AuthException](#authexception)**          | The Auth object provided is not a valid one
**[AbstractException](#abstractexception)**  | The timestamps that you passed on the objects are not valid ones
**[TrackerException](#trackerexception)**    | An internal error occured. *Hopefully this never happen*

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

### Tracking Login

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackLogin($auth);

?>
```

This function is used to send information to Inspetor everytime an account (*e.g. user*)  tries log in .

Argument | Type | Description
-------- | ---- | -----------
auth  | Inspetor/Model/[Auth](#auth) | The Auth that is logging in


### Tracking Logout

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackLogout($auth);

?>
```

This function is used to send information to Inspetor everytime an account (*e.g. user*) tries log out.

Argument | Type | Description
-------- | ---- | -----------
auth  | Inspetor/Model/[Auth](#auth) | The Auth that is logging out

## Tracking Password Activities

These are the functions that will be used to track all password changes initiated by the users that happen in your platform, independing if the user is logged in or not. The main activities that we track are the following:

- **Password Reset** (*trackPasswordReset*)
- **Password Recovery** (*trackPasswordRecovery*)

All the functions for tracking authentications will **receive an [PassRecovery](#passrecovery) object as argument** and will *return true* if everything goes right. Otherwise they will throw one of the following exceptions:

Exception | Description
--------- | -----------
**[PassRecoveryException](#passrecoveryexception)** | The PassRecovery object provided is not a valid one
**[AbstractException](#abstractexception)**         | The timestamps that you passed on the objects are not valid ones
**[TrackerException](#trackerexception)**           | An internal error occured. *Hopefully this never happen*

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

### Tracking Password Reset

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackPasswordReset($pass_recovery);

?>
```

This function is used to send information to Inspetor everytime an account (*e.g. user*) tries to reset it's password.

Argument | Type | Description
-------- | ---- | -----------
pass_recovery | Inspetor/Model/[PassRecovery](#passrecovery) | The PassRecovery that is being reseted

### Tracking Password Recovery

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackPasswordRecovery($pass_recovery);

?>
```

This function is used to send information to Inspetor everytime an account (*e.g. user*) tries to recover it's password.

Argument | Type | Description
-------- | ---- | -----------
pass_recovery | Inspetor/Model/[PassRecovery](#passrecovery) | The PassRecovery that is being recovered

## Tracking Event Activities

These are the functions that will be used to track the events (*e.g. parties, shows...*) that happen in your platform. The main activities that we track are the following:

- **Event Creation** (*trackEventCreation*)
- **Event Update**   (*trackEventUpdate*)
- **Event Deletion** (*trackEventDeletion*)

All the functions for tracking authentications will **receive an [Event](#event) object as argument** and will *return true* if everything goes right. Otherwise they will throw one of the following exceptions:

Exception | Description
--------- | -----------
**[EventException](#eventexception)**       | The Event object provided is not a valid one
**[AddressException](#addressexception)**   | The Address object provided in the Event object is not a valid one
**[AbstractException](#abstractexception)** | The timestamps that you passed on the objects are not valid ones
**[TrackerException](#trackerexception)**   | An internal error occured. *Hopefully this never happen*

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

### Tracking Event Creation

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackEventCreation($event);

?>
```

This function is used to send information to Inspetor everytime a new event (*e.g. parties, shows...*) is created in your plataform.

Argument | Type | Description
-------- | ---- | -----------
event | Inspetor/Model/[Event](#event) | The Event that is being created

### Tracking Event Update

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackEventUpdate($event);

?>
```

This function is used to send information to Inspetor everytime an event (*e.g. parties, shows...*) updates one of it's informations (*e.g. name, location...*).

Argument | Type | Description
-------- | ---- | -----------
event | Inspetor/Model/[Event](#event) | The Event that is being updated

### Tracking Event Update

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackEventDeletion($event);

?>
```

This function is used to send information to Inspetor everytime an event (*e.g. parties, shows...*) it's deleted on your platform.

Argument | Type | Description
-------- | ---- | -----------
event | Inspetor/Model/[Event](#event) | The Event that is being deleted

## Tracking Sale Activities

These are the functions that will be used to track sales that happen in your platform. The main activities that we track are the following:

- **Sale Creation** (*trackSaleCreation*)
- **Sale Update** (*trackSaleUpdate*)

All the functions for tracking authentications will **receive an [Sale](#sale) object as argument** and will *return true* if everything goes right. Otherwise they will throw one of the following exceptions:

Exception | Description
--------- | -----------
**[SaleException](#saleexception)**         | The Transfer object provided is not a valid one
**[ItemException](#itemexception)**         | The Item object provided on the Sale is not a valid one
**[PaymentException](#paymentexception)**   | The Payment object provided on the Sale is not a valid one
**[AbstractException](#abstractexception)** | The timestamps that you passed on the objects are not valid ones
**[TrackerException](#trackerexception)**   | An internal error occured. *Hopefully this never happen*

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

### Tracking Sale Creation

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackSaleCreation($sale);

?>
```

This function is used to send information to Inspetor everytime a new sale it's created on your platform.

Argument | Type | Description
-------- | ---- | -----------
sale | Inspetor/Model/[Sale](#sale) | The Sale that is being created

### Tracking Sale Update

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackSaleUpdate($sale);

?>
```

This function is used to send information to Inspetor everytime a sale updates it's status.

Argument | Type | Description
-------- | ---- | -----------
sale | Inspetor/Model/[Sale](#sale) | The Sale that is being updated

## Tracking Items Transfers Activities

These are the functions that will be used to track item (*e.g. ticket*) transfers between users (*e.g. accounts*) that happen in your platform. The main activities that we track are the following:

- **Item Transfer Creation** (*trackItemTransferCreation*)
- **Item Transfer Update** (*trackItemTransferUpdate*)

All the functions for tracking authentications will **receive an [Transfer](#transfer) object as argument** and will *return true* if everything goes right. Otherwise they will throw one of the following exceptions:

Exception | Description
--------- | -----------
**[TransferException](#transferexception)**  | The Transfer object provided is not a valid one
**[AbstractException](#abstractexception)**  | The timestamps that you passed on the objects are not valid ones
**[TrackerException](#trackerexception)**    | An internal error occured. *Hopefully this never happen*

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

### Tracking Transfer Creation

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackItemTransferCreation($transfer);

?>
```

This function is used to send information to Inspetor everytime a new item (*e.g. ticket*) transfer is created on your platform.

Argument | Type | Description
-------- | ---- | -----------
transfer | Inspetor/Model/[Transfer](#transfer) | The Transfer that is being created

### Tracking Transfer Update

```php
<?php

use Inspetor;

$inspetor = $this->getConfiguredInspetor();

//Using the Inspetor instace that is already configured
$inspetor->trackItemTransferUpdate($transfer);

?>
```

This function is used to send information to Inspetor everytime a item (*e.g. ticket*) transfer has it's status updated. 

Argument | Type | Description
-------- | ---- | -----------
transfer | Inspetor/Model/[Transfer](#transfer) | The Transfer that is being updated

# Models

The Inspetor Library provides a set of classes (*e.g. models*) that are used to help you collect the information that we need.

To get new instances of which model we suggest that you use the pre-built "gets" that are available in the InspetorClient class. They are an easy way to have access to every model without having to import every class.

All the models have some optional properties, but it's important that you try to send us as much information as you can. Since this helps our machine learning models make better decisions.

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>


## Account

The Account Model will contain information about an user. 

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_account = $inspetor->getInspetorAuth();

// Filling model with company data
$inspetor_account->setId("123"); //getId()
$inspetor_account->setName("Test Name"); //getName()
$inspetor_account->setEmail("test@email.com"); //getEmail()
$inspetor_account->setDocument("07206094880"); //getDocument()
$inspetor_account->setPhoneNumber("11953891736"); //getPhoneNumber()
$inspetor_account->setAddress($inspetor_address); //getAddress()
$inspetor_account->setBillingAddress($inspetor_billing_address); //getBillingAddress()
$inspetor_account->setCreationTimestamp(time()); //getCreationTimestamp()
$inspetor_account->setUpdateTimestamp(time()); //getUpdateTimestamp()

?>
```

All the properties can be defined and accessed through **gets** and **sets**

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | An unique indentifier of this user in your platform
**email** | Yes | String | The email of the user
**update_timestamp** | Yes | Integer | The unix format of the time and date that the action happend
name | No | String | The name of the user
document | No | String | The user CPF
phone_number | No | String | The user phone number
address | No | [Address](#address) | The address of the user
billing_address | No | [Address](#address) | The billing address of the user
creation_timestamp | No | Integer | The unix format of the time and date that the user account was created

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

## Address

The Address Model will contain information address that are used in other models (Account and Event). 

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_address = $inspetor->getInspetorAddress();

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

All the properties can be defined and accessed through **gets** and **sets**

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**street** | Yes | String | The street of the address
**number** | Yes | String | The street number of the address
**zip_code** | Yes | String | The zip code (*e.g. cep*) of the address
**city** | Yes | String | The city on which the address is located
**state** | Yes | String | The state on which the address is located
**country** | Yes | String | The country on which the address is located
latitude | No | String | The exact latitude of the address
longitude | No | String | The exact longitude of the address

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

## Auth

The Auth Model will contain information about log ins and log outs in your platform. 

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_auth = $inspetor->getInspetorAuth();

// Filling model with company data
$inspetor_auth->setAccountId("123"); //getAccountId()
$inspetor_auth->setAccountEmail("test@email.com"); //getAccountEmail()
$inspetor_auth->setTimestamp(time()); //getTimestamp()

?>
```

All the properties can be defined and accessed through **gets** and **sets**

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**account_id** | Yes | String | The id of the user that is making the login or logout
**timestamp** | Yes | Integer | The unix format of the time and date that the authentication happend
account_email | No | String | The email that is being used to log in or log out

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

## CreditCard

The Credit Card Model will contain information about credit cards that are used in [sales](#sale). 

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_cc = $inspetor->getInspetorCreditCard();

// Filling model with company data
$inspetor_cc->setFirstSixDigits("123456"); //getFirstSixDigits()
$inspetor_cc->setLastFourDigits("1234"); //getLastFourDigits()
$inspetor_cc->setHolderName("Holder Name"); //getHolderName()
$inspetor_cc->setHolderCpf("07206094880"); //getHolderCpf()

?>
```

All the properties can be defined and accessed through **gets** and **sets**

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**first_six_digits** | Yes | String | The first six digits of the credit card number
**last_four_digits** | Yes | Integer | The last four digits of the credit card number
**holder_name** | Yes | String | The name of the owner of the credit card
**holder_cpf** | Yes | String | The cpf of the owner of the credit card

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

## Event

The Event Model will contain information about parties, shows... that are registered in your platform

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_event = $inspetor->getInspetorEvent();

// Filling model with company data
$inspetor_event->setId("8000"); //getId()
$inspetor_event->setName("Name Test"); //getName()
$inspetor_event->setDescription("Description Test"); //getDescription()
$inspetor_event->setCreationTimestamp(time()); //getCreationTimestamp()
$inspetor_event->setUpdateTimestamp(time()); //getUpdateTimestamp()
$inspetor_event->setSessions([
    [
        "id"        => "123",
        "timestamp" => $event_session_date1
    ],
    [
        "id"        => "124",
        "timestamp" => $event_session_date2
    ]
]); //getSession()
$inspetor_event->setStatus("private"); //getStatus()
$inspetor_event->setCategories(["Category1", "Category2"]); //getCategories()
$inspetor_event->setAddress($inspetor_event_address); //getAddress()
$inspetor_event->setUrl("cool-company-event"); //getUrl()
$inspetor_event->setProducerId("123"); //getProducerId()
$inspetor_event->setAdminsId(["123", "234"]); //getAdminsId()
$inspetor_event->setSeatingOptions(["Pista", "VIP"]); //getSeatingOptions()

?>
```

All the properties can be defined and accessed through **gets** and **sets**

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | An unique indentifier of this event in your platform
**name** | Yes | String | The name of the event
**status** | Yes | String | The status of the event. *We have some pre-built status (draft, private and published) but you can use others if you want*
**address** | Yes | [Address](#address) | The address of where the event is happening
**sessions** | Yes | Array | All the dates that the event happens (if it has more than one) and the id of which date.
**producer_id** | Yes | String | The id of the user who created the event
**admins_id** | Yes | Array | An array containing the id of all the users who can make changes to the event
**update_timestamp** | Yes | Integer | The unix format of the time and date that the action happend
description | No | String | The description of the event
creation_timestamp | No | Integer | The unix format of the time and date that the event was created
seating_options | No | Array | An array containing all names of the different ticket types that can be bought for this event
categories | No | Array | An array containing the names of the categories of the event
url | No | String | The url where the event is being sold

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

## Item

The Item Model will contain information about the ticket that is being sold in a [sale](#sale). 

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_item = $inspetor->getInspetorItem();

// Filling model with company data
$inspetor_item->setId("9000"); //getId()
$inspetor_item->setEventId("8000"); //getEventId()
$inspetor_item->setSessionId("124"); //getSessionId()
$inspetor_item->setPrice("50.00"); //getPrice()
$inspetor_item->setSeatingOption("PISTA"); //getSeatingOption()
$inspetor_item->setQuantity("2"); //getQuantity()

?>
```

All the properties can be defined and accessed through **gets** and **sets**

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | An unique indentifier of this item (*e.g. ticket*) in your platform
**event_id** | Yes | String | The unique indentifier of the event that the ticket is tied too
**session_id** | Yes | Integer | The unique indentifier of the event session (date and time) that the ticket is tied too
**price** | Yes | String | The price of the ticket. *It should only contain number, dots and commas*
**quantity** | Yes | String | The number of this type of tickets that are being bought. 
seating_option | No | String | The name of the type of ticket that is being bought

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

## PassRecovery

The PassRecovery Model will contain information about all the password changes initiated by the user.

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_pass = $inspetor->getInspetorPassRecovery();

// Filling model with company data
$inspetor_pass->setRecoveryEmail("test@email.com"); //getRecoveryEmail()
$inspetor_pass->setTimestamp(time()); //getTimestamp()

?>
```

All the properties can be defined and accessed through **gets** and **sets**

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**recovery_email** | Yes | String | The email that is being used to recovery or reset the password
**timestamp** | Yes | String | The unix format of the time and date that the action happend

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

## Payment

The Payment Model will contain information about the payment that happens in a sale.

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_payment = $inspetor->getInspetorPayment();

// Filling model with company data
$inspetor_payment->setId("12345"); //getId()
$inspetor_payment->setMethod("credit_card"); //getMethod()
$inspetor_payment->setInstallments("1"); //getInstallments()
$inspetor_payment->setCreditCard($inspetor_cc); //getCreditCard()

?>
```

All the properties can be defined and accessed through **gets** and **sets**

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | The id of the payment. This id is the on eyou send to the bank 
**method** | Yes | String | The method of payment being used. *The allowed values are credit_card, boleto, other*
**installments** | Yes | String | The number of "*parcelas*" that the user will pay
credit_card | No | [CreditCard](#creditcard) | If the method is *credit_card* it should contains a credit card object

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

## Sale

The Sale Model will contain information about a sale that happens in your platform.

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_sale = $inspetor->getInspetorSale();

// Filling model with company data
$inspetor_sale->setId("1234"); //getId()
$inspetor_sale->setAccountId("123"); //getAccountId()
$inspetor_sale->setStatus("pending"); //getStatus()
$inspetor_sale->setIsFraud(false); //getIsFraud()
$inspetor_sale->setCreationTimestamp(time()); //getCreationTimestamp()
$inspetor_sale->setUpdateTimestamp(time()); //getUpdateTimestamp()
$inspetor_sale->setItems([$inspetor_item1, $inspetor_item2]); //getItems()
$inspetor_sale->setPayment($inspetor_payment); //getPayment()

?>
```

All the properties can be defined and accessed through **gets** and **sets**

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | An unique indentifier of the sale in your platform
**account_id** | Yes | String | The id of the user who is making the purchase
**status** | Yes | String | The status of the sale. *The allowed values are: accepted, declined, pending, refunded, manual_analysis*
**is_fraud** | Yes | Boolean | Indicates if the sale was fradulent. This should be false by default and should only be true when you get the confirmation of the cashback
**update_timestamp** | Yes | Integer | The unix format of the time and date that the action happend
**items** | Yes | Array of [Item](#item) | The items (*e.g. tickets*) that are being bought
**payment** | Yes | [Payment](#payment) | The payment used in this purchase
creation_timestamp | No | Integer | The unix format of the time and date that the sale was created
total_value | No | Integer | The value of all items. *This value is not set by you!*

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

## Transfer

The Transfer Model will contain information transfer of [items](#item) (*e.g. tickets*) that happen in your platform

### Properties

```php
<?php

// Calling an instance of Model
$inspetor_transfer = $inspetor->getInspetorTransfer();

// Filling model with company data
$inspetor_transfer->setId("123"); //getId()
$inspetor_transfer->setCreationTimestamp(time()); //getCreationTimestamp()
$inspetor_transfer->setUpdateTimestamp(time()); //getUpdateTimestamp()
$inspetor_transfer->setItemId("9000"); //getItemId()
$inspetor_transfer->setSenderAccountId("124"); //getSenderAccountId()
$inspetor_transfer->setReceiverEmail("test@email.com"); //getReceiverEmail()
$inspetor_transfer->setStatus("pending"); //getStatus()

?>
```

All the properties can be defined and accessed through **gets** and **sets**

Property | Required | Type | Description
-------- | -------- | ---- | -----------
**id** | Yes | String | An unique indentifier of the transfer
**item_id** | Yes | String | The id of the [item](#item) (*e.g. ticket*) that is being transfered 
**sender_account_id** | Yes | String | The id of the user who is sending the item (*e.g. ticket*)
**receiver_email** | Yes | String | The email of the person who is receiving the item (*e.g. ticket*)
**update_timestamp** | Yes | Integer | The unix format of the time and date that the action happend
**status** | Yes | String | The status of the transfer. *The allowed values are: accepted, rejected, pending (should be pending when created)*
creation_timestamp | No | Integer | The unix format of the time and date that the transfer was created

<aside class="notice">
You can find language specific details <a href="#language-specific">here</a>.
</aside>

# Language Specific

## PHP

You can find more php specific documents [here](https://github.com/inspetor/inspetor-php/blob/master/README.md)