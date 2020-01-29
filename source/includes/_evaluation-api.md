# Evaluation API
```shell
curl -X POST https://collection-prod.inspcdn.net/evaluation \
    -H "Authorization: Bearer $API_KEY" \
    -H "Content-Type: application/json" \
    -d '{
        "sale_id": "12345",
        "account_id": "157421",
        "sale_datetime": 1579792758,
        "event_date_id": "23553",
        "sale_total_value": 54.26,
        "first_six_digits_cc": "455326",
        "last_four_digits_cc": "0012",
        "holder_cpf": "741.112.235-53"
    }'
```

Our evaluation API consists of a single resource: `/evaluation`. This resource should be used whenever you have a Sale that you would like to get evaluated by Inspetor.

It is a `POST` endpoint, and the fields it accepts are as follows:

Property                        | Type    | Description
--------                        | ----    | -----------
sale_id                         | String  | The unique identifier for the sale within your platform
account_id                      | String  | The ID of the account attempting the purchase
sale_datetime                   | Integer | The Unix-timestamp corresponding to the date and time of the sale
event_date_id <sup>[*]</sup>    | String  | The event datetime id associated to the sale
sale_total_value                | Float   | The total monetary value of the sale
first_six_digits_cc             | String  | The first six digits of the credit card associated to the sale
last_four_digits_cc             | String  | The last four digits of the credit card associated to the sale
holder_cpf                      | String  | The card holder's CPF. It may contain dots and dashes but it's not required

**All of these fields are required - we cannot evaluate a sale that has any of these missing.**

The success response for this resource is a JSON such as `{"inspetor_decision": "<our decision>"}`; where our decision is either `approve`, `reject` or `manual`.

<aside class="notice">
[*] Even though a sale might have more than one event datetime id associated to it, at this moment, we only require the main one associated to the sale in this endpoint. That is, even if there might be multiple tickets, corresponding to multiple event datetime ids, in a single sale, we only ask for a single event datetime id (usually the event_date_id that will be in your sales table).
</aside>
