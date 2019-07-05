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

These are the functions that will be used to track the user (*e.g. account*) inside your application. The main activities that will be tracked are the followings:

- **Account Creation** (*trackAccountCreation*)
- **Account Updates** (*trackAccountUpdate*)
- **Account Deletion** (*trackAccountDeletion*)

All the functions for tracking accounts (*e.g. user*) **will receive an [Account]() object as argument** and will *return true* if everything goes right. Otherwise they will throw one of the following exceptions:

Exception | Description
--------- | -----------
**AccountException**   | The Account object provided is not a valid one
**AddressException**   | The Address object provided in the Account object is not a valid one
**AbstractException**  | The timestamps that you passed on the objects are not valid ones
**TrackerException**   | An internal error occured. *Hopefully this never happen*

<aside class="notice">
You can find language specific details <a href="localhost:4567">here</a>.
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
account  | Inspetor/Model/[Account]() | The Account that is being created


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
account  | Inspetor/Model/[Account]() | The Account that is being updated


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
account  | Inspetor/Model/[Account]() | The Account that is being deleted

## Tracking Authetication Activities

These are the functions that will be used to track authentications (*e.g. logins and logouts*) that happen in your platform. The main activities that we track are the following:

- **Login** (*trackLogin*)
- **Logout** (*trackLogout*)

All the functions for tracking authentications will **receive an [Auth]() object as argument** and will *return true* if everything goes right. Otherwise they will throw one of the following exceptions:

Exception | Description
--------- | -----------
**AuthException**      | The Auth object provided is not a valid one
**AbstractException**  | The timestamps that you passed on the objects are not valid ones
**TrackerException**   | An internal error occured. *Hopefully this never happen*

<aside class="notice">
You can find language specific details <a href="localhost:4567">here</a>.
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
auth  | Inspetor/Model/[Auth]() | The Auth that is logging in


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
auth  | Inspetor/Model/[Auth]() | The Auth that is logging out

## Tracking Password Activities

These are the functions that will be used to track all password changes initiated by the users that happen in your platform. The main activities that we track are the following:

- **Password Reset** (*trackPasswordReset*)
- **Password Recovery** (*trackPasswordRecovery*)

All the functions for tracking authentications will **receive an [PassRecovery]() object as argument** and will *return true* if everything goes right. Otherwise they will throw one of the following exceptions:

Exception | Description
--------- | -----------
**PassRecoveryException** | The PassRecovery object provided is not a valid one
**AbstractException**     | The timestamps that you passed on the objects are not valid ones
**TrackerException**      | An internal error occured. *Hopefully this never happen*

<aside class="notice">
You can find language specific details <a href="localhost:4567">here</a>.
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
pass_recovery | Inspetor/Model/[PassRecovery]() | The PassRecovery that is being reseted

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
pass_recovery | Inspetor/Model/[PassRecovery]() | The PassRecovery that is being recovered

## Tracking Event Activities

These are the functions that will be used to track the events (*e.g. parties, shows...*) that happen in your platform. The main activities that we track are the following:

- **Event Creation** (*trackEventCreation*)
- **Event Update**   (*trackEventUpdate*)
- **Event Deletion** (*trackEventDeletion*)

All the functions for tracking authentications will **receive an [Event]() object as argument** and will *return true* if everything goes right. Otherwise they will throw one of the following exceptions:

Exception | Description
--------- | -----------
**EventException**     | The Event object provided is not a valid one
**AddressException**   | The Address object provided in the Event object is not a valid one
**AbstractException**  | The timestamps that you passed on the objects are not valid ones
**TrackerException**   | An internal error occured. *Hopefully this never happen*

<aside class="notice">
You can find language specific details <a href="localhost:4567">here</a>.
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
event | Inspetor/Model/[Event]() | The Event that is being created

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
event | Inspetor/Model/[Event]() | The Event that is being updated

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
event | Inspetor/Model/[Event]() | The Event that is being deleted

## Tracking Sale Activities

These are the functions that will be used to track sales that happen in your platform. The main activities that we track are the following:

- **Sale Creation** (*trackSaleCreation*)
- **Sale Update** (*trackSaleUpdate*)

All the functions for tracking authentications will **receive an [Sale]() object as argument** and will *return true* if everything goes right. Otherwise they will throw one of the following exceptions:

Exception | Description
--------- | -----------
**SaleException**      | The Transfer object provided is not a valid one
**ItemException**      | The Item object provided on the Sale is not a valid one
**PaymentException**   | The Payment object provided on the Sale is not a valid one
**AbstractException**  | The timestamps that you passed on the objects are not valid ones
**TrackerException**   | An internal error occured. *Hopefully this never happen*

<aside class="notice">
You can find language specific details <a href="localhost:4567">here</a>.
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
sale | Inspetor/Model/[Sale]() | The Sale that is being created

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
sale | Inspetor/Model/[Sale]() | The Sale that is being updated

## Tracking Items Transfers Activities

These are the functions that will be used to track item (*e.g. ticket*) transfers between users (*e.g. accounts*) that happen in your platform. The main activities that we track are the following:

- **Item Transfer Creation** (*trackItemTransferCreation*)
- **Item Transfer Update** (*trackItemTransferUpdate*)

All the functions for tracking authentications will **receive an [Transfer]() object as argument** and will *return true* if everything goes right. Otherwise they will throw one of the following exceptions:

Exception | Description
--------- | -----------
**TransferException**  | The Transfer object provided is not a valid one
**AbstractException**  | The timestamps that you passed on the objects are not valid ones
**TrackerException**   | An internal error occured. *Hopefully this never happen*

<aside class="notice">
You can find language specific details <a href="localhost:4567">here</a>.
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
transfer | Inspetor/Model/[Transfer]() | The Transfer that is being created

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
transfer | Inspetor/Model/[Transfer]() | The Transfer that is being updated

