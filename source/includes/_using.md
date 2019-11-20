# Using the Inspetor collection service

In order to protect your company from fraudsters, our decision models need to be informed with customer behavior.

 But we can't do it alone--we need _you_, our client, to send this information to us via the Client Library so that we can make better-informed decisions.

At a high level, our decision model understands the e-commerce world in the following primary terms:

- <a href="#account-activity">**Accounts**</a>
- <a href="#event-activity">**Events**</a>
- <a href="#sale-activity">**Sales**</a>
- <a href="#inspetoritem">**Sale Items**</a>
- <a href="#inspetortransfer">**Transfers**</a>

You can think of the relationship between those entities something like this:

If a user purchases tickets for a show on your site, Inspetor interprets the action as:

- the creation of a new <a href="#sale-activity">*Sale*</a>
- the association of that Sale with an existing <a href="#account-activity">*Account*</a>
- the association of that Sale with one or more <a href="#inspetoritem">*Items*</a>
- the association of that Item with an existing <a href="#event-activity">*Event*</a>

While these are the terms with which our model interprets actions on your platform, Inspetor is unaware of these actions occurring unless you use the Inspetor Collection API to relay this information to us.

<aside class="notice">
Inspetor will never request write access to your code base--that means that it is on <i>you</i>, the developer, to integrate our library into your product's code base. We think that's the right way to do things: you know your product's code base, we know fraud.
</aside>

## When to send events to Inspetor

The primary Inspetor entities are **stateful** objects. They have properties that can be updated, and the values of these properties are crucial to our evaluation of transaction validity. Thus, you should send events to Inspetor via the client library whenever properties of these objects are changed.

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
- When a user attempts to <a href="#account-login">log in to an account</a>
- When a user attempts to <a href="#account-logout">log out of an account</a>

### Password Activity
- When a user requests to <a href="#password-recovery">recover</a> their password
- When a user <a href="#password-reset">resets</a> their password

## Where to insert Inspetor collection functions
Where in your code base does the Inspetor client library belong? Frontend? Backend? Loaded on the site?

The answer is in as many places as possible. From your frontend interfaces (iOS/Android apps, JS websites), we're able to derive valuable information such as device characteristics, user behavior, and IP information, while from the backend you can provide us with a more holistic representation of your data in terms of business logic. Both of these types of data are extremely valuable for detecting fraud. As such, we suggest the following:

- Full event coverage within the server/API level of your application (backend): This allows us to know everything about what is happening within your product.
- 1:1 corresponding coverage within your frontend interfaces (Web, iOS, and Android): This allows us to enrich the knowledge we're gathering from your server-level transactions with additional information that improves our protection capabilities.

Note that the information that you provide in either environment will vary. In the frontend integrations, you can rely on our SDKs to automatically relay the majority of the information we use to make a decision. You can read more about integrating with our frontend SDKs [here](https://inspetor.github.io/docs-frontend).


## Testing your integration with Inspetor

Integrating with Inspetor is meant to be easy--simply instantiate our library or hit our REST API with valid authentication, and if there are no errors thrown within your code execution, data will appear within our database. For further validation, we also provide our customers with limited-access database credentials that allow the developer in charge of integrating Inspetor to inspect that data appears in our database. (Note that access is restricted such that your customer account will only be able to view data originating from your company's integration.) The Inspetor team will provide you with access credentials for this phase of validation.

However, ensuring that some data is making its way into our database is not sufficient for validating an Inspetor integration. We need to ensure that our understanding of state updates to primary entities (such as sales or accounts) remains accurate over time. This means that after the initial integration of our client library into your production code, we will need to periodically validate that our representation of sales, accounts, etc. corresponds to the true state of those entities (as represented in the customer database). This phase of validation is highly customer-specific and it will involve coordinated effort from both the customer and the Inspetor integration team.