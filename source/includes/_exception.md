# Exceptions

The Inspetor Client Library uses the following exceptions:


Exception | Description
--------- | -----------
[TrackerException](#trackerexception) | An error occured when sending information to our trackers
[generalException](#generalException) | The provided timestamp was not in Unix format
[AccountException](#accountexception) | The provided [Account](#account) object was invalid
[AddressException](#addressexception) | The provided [Address](#address) object was invalid
[AuthException](#authexception) | The provided [Auth](#auth) object was invalid
[CreditCardException](#creditcardexception) | The provided [CreditCard](#creditcard) object was invalid
[EventException](#eventexception) | The provided [Event](#event) object was invalid
[ItemException](#itemexception) | The provided [Item](#item) object was invalid
[PassRecoveryException](#passrecoveryexception) | The provided [PassRecovery](#passrecovery) object was invalid
[PaymentException](#paymentexception) | The provided [Payment](#payment) object was invalid
[SaleException](#saleexception) | The provided [Sale](#sale) object was invalid
[TransferException](#transferexception) | The provided [Transfer](#transfer) object was invalid

## TrackerException

This exception is thrown when an error occured while sending information via our trackers

### Types

Category | Meaning
-------- | ------
9001 | AppId and trackerName are required parameters

## GeneralException

This exception is thrown when you provide a non-Unix-formatted datetime as a timestamp property in a model

### Types

Category | Meaning
-------- | ------
7001 | The timestamp should be an integer

## AccountException

This exception is thrown when you provide an [Account](#account) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | id is a required property. It must not be null
7002 | email is a required property. It must not be null
7003 | update_timestamp is a required property. It must not be null

## AddressException

This exception is thrown when you provide an [Address](#address) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | street is a required property. It must not be null
7002 | number is a required property. It must not be null
7003 | zip_code is a required property. It must not be null
7004 | city is a required property. It must not be null
7005 | state is a required property. It must not be null
7006 | country is a required property. It must not be null

## AuthException

This exception is thrown when you provide an [Auth](#auth) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | account_id is a required property. It must not be null
7002 | timestamp is a required property. It must not be null

## CreditCardException

This exception is thrown when you provide a [CreditCard](#creditcard) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | first_six_digits is a required property. It must not be null
7002 | last_four_digits is a required property. It must not be null
7003 | holder_name is a required property. It must not be null
7004 | holder_cpf is a required property. It must not be null

## EventException

This exception is thrown when you provide an [Event](#event) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001  | id is a required property. It must not be null
7002  | name is a required property. It must not be null
7003  | update_timestamp is a required property. It must not be null
7004  | producer_id is a required property. It must not be null
7005  | address is a required property. It must not be null
7006  | sessions is a required property. It must not be null neither an empty array
7007  | seating_options should be null or an array of strings
7008  | categories should be null or an array of strings
7009  | The status is not a valid one
7010  | sessions should be an array of one or more sessions
7011  | id and timestamp are required properties of a session
7012  | admins_id should be an array of one or more users

## ItemException

This exception is thrown when you provide an [Item](#item) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | id is a required property. It must not be null
7002 | event_id is a required property. It must not be null
7003 | session_id is a required property. It must not be null
7004 | price is a required property. It must not be null
7005 | seating_option is a required property. It must not be null
7006 | price is not valid
7007 | quantity is a required property. It must not be null

## PassRecoveryException

This exception is thrown when you provide a [PassRecovery](#passrecovery) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | recovery_email is a required property. It must not be null
7002 | timestamp is a required property. It must not be null

## PaymentException

This exception is thrown when you provide a [Payment](#payment) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | id is a required property. It must not be null
7002 | method is a required property. It must not be null
7003 | installments is a required property. It must not be null
7004 | This payment method is not a valid one
7005 | Credit card can't be null when method is credit_card

## SaleException

This exception is thrown when you provide a [Sale](#sale) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001  | id is a required property. It must not be null
7002  | account_id is a required property. It must not be null
7003  | status is a required property. It must not be null
7004  | is_fraud is a required property. It must not be null
7005  | update_timestamp is a required property. It must not be null
7006  | items is a required property. It must not be null neither an empty array
7007  | payment is a required property. It must not be null
7008  | The status is not a valid one
7009  | One or more items have invalid price

## TransferException

This exception is thrown when you provide a [Transfer](#transfer) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | id is a required property. It must not be null
7002 | update_timestamp is a required property. It must not be null
7003 | item_id is a required property. It must not be null
7004 | sender_account_id is a required property. It must not be null
7005 | receiver_email is a required property. It must not be null
7006 | That's an invalid status

