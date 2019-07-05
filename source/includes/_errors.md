# Exceptions

<aside class="notice">
This error section is stored in a separate file in <code>includes/_errors.md</code>. Slate allows you to optionally separate out your docs into many files...just save them to the <code>includes</code> folder and add them to the top of your <code>index.md</code>'s frontmatter. Files are included in the order listed.
</aside>

The Kittn API uses the following error codes:


Exception | Description
--------- | -----------
[TrackerException](#trackerexception) | An error occured when sending information to our trackers
[AbstractException](#abstractexception) | An timestamp that was given in one of the models wasn't in unix format
[AccountException](#accountexception) | The [Account](#account) object given was not a valid one
[AddressException](#addressexception) | The [Address](#address) object given was not a valid one
[AuthException](#authexception) | The [Auth](#auth) object given was not a valid one
[CreditCardException](#creditcardexception) | The [CreditCard](#creditcard) object given was not a valid one
[EventException](#eventexception) | The [Event](#event) object given was not a valid one
[ItemException](#itemexception) | The [Item](#item) object given was not a valid one
[PassRecoveryException](#passrecoveryexception) | The [PassRecovery](#passrecovery) object given was not a valid one
[PaymentException](#paymentexception) | The [Payment](#payment) object given was not a valid one
[SaleException](#saleexception) | The [Sale](#sale) object given was not a valid one
[TransferException](#transferexception) | The [Transfer](#transfer) object given was not a valid one

## TrackerException

This exceptions are thrown when an error occured when sending information to our trackers

### Types

Category | Meaning
-------- | ------
9001 | AppId and trackerName are required parameters

## AbstractException

This exceptions are thrown when you you provide a date not in unix format to a timestamp property

### Types

Category | Meaning
-------- | ------
7001 | The timestamp should be an integer

## AccountException

This exceptions are thrown when you you provide an [Account](#account) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | id is a required property. It can't be null
7002 | email is a required property. It can't be null
7003 | update_timestamp is a required property. It can't be null

## AddressException

This exceptions are thrown when you you provide an [Address](#address) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | street is a required property. It can't be null
7002 | number is a required property. It can't be null
7003 | zip_code is a required property. It can't be null
7004 | city is a required property. It can't be null
7005 | state is a required property. It can't be null
7006 | country is a required property. It can't be null

## AuthException

This exceptions are thrown when you you provide an [Auth](#auth) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | account_id is a required property. It can't be null
7002 | timestamp is a required property. It can't be null

## CreditCardException

This exceptions are thrown when you you provide an [CreditCard](#creditcard) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | first_six_digits is a required property. It can't be null
7002 | last_four_digits is a required property. It can't be null
7003 | holder_name is a required property. It can't be null
7004 | holder_cpf is a required property. It can't be null

## EventException

This exceptions are thrown when you you provide an [Event](#event) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001  | id is a required property. It can't be null
7002  | name is a required property. It can't be null
7003  | update_timestamp is a required property. It can't be null
7004  | producer_id is a required property. It can't be null
7005  | address is a required property. It can't be null
7006  | sessions is a required property. It can't be null neither an empty array
7007  | seating_options should be null or an array of strings
7008  | categories should be null or an array of strings
7009  | The status is not a valid one
70010 | sessions should be an array of one or more sessions
70011 | id and timestamp are required properties of a session

## ItemException

This exceptions are thrown when you you provide an [Item](#item) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | id is a required property. It can't be null
7002 | event_id is a required property. It can't be null
7003 | session_id is a required property. It can't be null
7004 | price is a required property. It can't be null
7005 | seating_option is a required property. It can't be null
7006 | price is not valid
7007 | quantity is a required property. It can't be null

## PassRecoveryException

This exceptions are thrown when you you provide an [PassRecovery](#passrecovery) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | recovery_email is a required property. It can't be null
7002 | timestamp is a required property. It can't be null

## PaymentException

This exceptions are thrown when you you provide an [Payment](#payment) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | id is a required property. It can't be null
7002 | method is a required property. It can't be null
7003 | installments is a required property. It can't be null
7004 | This payment method is not a valid one
7005 | Credit card can't be null when method is credit_card

## SaleException

This exceptions are thrown when you you provide an [Sale](#sale) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001  | id is a required property. It can't be null
7002  | account_id is a required property. It can't be null
7003  | status is a required property. It can't be null
7004  | is_fraud is a required property. It can't be null
7005  | update_timestamp is a required property. It can't be null
7006  | items is a required property. It can't be null neither an empty array
7007  | payment is a required property. It can't be null
7008  | The status is not a valid one
7009  | One or more items have invalid price

## TransferException

This exceptions are thrown when you you provide an [Transfer](#transfer) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | id is a required property. It can't be null
7002 | update_timestamp is a required property. It can't be null
7003 | item_id is a required property. It can't be null
7004 | sender_account_id is a required property. It can't be null
7005 | receiver_email is a required property. It can't be null
7006 | That's an invalid status

