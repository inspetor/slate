# Exceptions

The Inspetor Client Library uses the following exceptions:


Exception | Description
--------- | -----------
[TrackerException](#trackerexception) | An error occured when sending information to our trackers
[InspetorGeneralException](#inspetorgeneralexception) | The provided timestamp was not in Unix format
[InspetorAccountException](#inspetoraccountexception) | The provided [InspetorAccount](#inspetoraccount) object was invalid
[InspetorAddressException](#inspetoraddressexception) | The provided [InspetorAddress](#inspetoraddress) object was invalid
[InspetorAuthException](#inspetorauthexception) | The provided [InspetorAuth](#inspetorauth) object was invalid
[InspetorCategoryException](#inspetorcategoryexception) | The provided [InspetorCategory](#inspetorcategory) object was invalid
[InspetorCreditCardException](#inspetorcreditcardexception) | The provided [InspetorCreditCard](#inspetorcreditcard) object was invalid
[InspetorEventException](#inspetoreventexception) | The provided [InspetorEvent](#inspetorevent) object was invalid
[InspetorItemException](#inspetoritemexception) | The provided [InspetorItem](#inspetoritem) object was invalid
[InspetorPassRecoveryException](#inspetorpassrecoveryexception) | The provided [InspetorPassRecovery](#inspetorpassrecovery) object was invalid
[InspetorPaymentException](#inspetorpaymentexception) | The provided [InspetorPayment](#inspetorpayment) object was invalid
[InspetorSaleException](#inspetorsaleexception) | The provided [InspetorSale](#inspetorsale) object was invalid
[InspetorSessionException](#inspetorsessionexception) | The provided [InspetorSession](#inspetorsession) object was invalid
[InspetorTransferException](#inspetortransferexception) | The provided [InspetorTransfer](#inspetortransfer) object was invalid

## TrackerException

This exception is thrown when an error occured while sending information via our trackers

### Types

Category | Meaning
-------- | ------
9001 | AppId and trackerName are required parameters

## InspetorGeneralException

This exception is thrown when you provide a non-Unix-formatted datetime as a timestamp property in a model

### Types

Category | Meaning
-------- | ------
7001 | The timestamp should be an integer

## InspetorAccountException

This exception is thrown when you provide an [InspetorAccount](#inspetoraccount) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | id is a required property. It must not be null
7002 | email is a required property. It must not be null
7003 | timestamp is a required property. It must not be null

## InspetorAddressException

This exception is thrown when you provide an [InspetorAddress](#inspetoraddress) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | street is a required property. It must not be null
7002 | zip_code is a required property. It must not be null
7003 | city is a required property. It must not be null
7004 | state is a required property. It must not be null
7005 | country is a required property. It must not be null

## InspetorAuthException

This exception is thrown when you provide an [InspetorAuth](#inspetorauth) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | account_id is a required property. It must not be null
7002 | timestamp is a required property. It must not be null

## InspetorCreditCardException

This exception is thrown when you provide a [InspetorCreditCard](#inspetorcreditcard) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | first_six_digits is a required property. It must not be null
7002 | last_four_digits is a required property. It must not be null
7003 | holder_name is a required property. It must not be null
7004 | holder_cpf is a required property. It must not be null

## InspetorEventException

This exception is thrown when you provide an [InspetorEvent](#inspetorevent) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001  | id is a required property. It must not be null
7002  | name is a required property. It must not be null
7003  | timestamp is a required property. It must not be null
7004  | producer_id is a required property. It must not be null
7005  | address is a required property. It must not be null
7006  | sessions is a required property. It must not be null neither an empty array
7007  | seating_options should be null or an array of strings
7008  | categories should be null or an array of strings
7009  | The status is not a valid one
7010  | sessions should be an array of one or more sessions
7011  | id and timestamp are required properties of a session
7012  | admins_id should be an array of one or more users

## InspetorItemException

This exception is thrown when you provide an [InspetorItem](#inspetoritem) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | id is a required property. It must not be null
7002 | event_id is a required property. It must not be null
7003 | session_id is a required property. It must not be null
7004 | price is a required property. It must not be null
7005 | price is not valid. It must be a double value equals or greater than zero.
7006 | quantity is a required property. It must be an integer greater than zero.

## InspetorPassRecoveryException

This exception is thrown when you provide a [InspetorPassRecovery](#inspetorpassrecovery) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | recovery_email is a required property. It must not be null
7002 | timestamp is a required property. It must not be null

## InspetorPaymentException

This exception is thrown when you provide a [InspetorPayment](#inspetorpayment) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | id is a required property. It must not be null
7002 | method is a required property. It must not be null
7003 | installments is a required property. It must not be null
7004 | This payment method is not a valid one
7005 | Credit card can't be null when method is credit_card

## InspetorSaleException

This exception is thrown when you provide a [InspetorSale](#inspetorsale) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001  | id is a required property. It must not be null
7002  | account_id is a required property. It must not be null
7003  | status is a required property. It must not be null
7004  | is_fraud is a required property. It must not be null
7005  | timestamp is a required property. It must not be null
7006  | items is a required property. It must not be null neither an empty array
7007  | payment is a required property. It must not be null
7008  | The status is not a valid one
7009  | One or more items have invalid price

## InspetorTransferException

This exception is thrown when you provide a [InspetorTransfer](#inspetortransfer) object with invalid properties or missing required properties

### Types

Category | Meaning
-------- | ------
7001 | id is a required property. It must not be null
7002 | timestamp is a required property. It must not be null
7003 | item_id is a required property. It must not be null
7004 | sender_account_id is a required property. It must not be null
7005 | receiver_email is a required property. It must not be null
7006 | That's an invalid status

