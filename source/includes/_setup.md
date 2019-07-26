# Client Library Setup

```php
<?php

use Inspetor;

$inspetor_config = [
  "appId"       => "your appId" # (e.g. '30cdfed3-9f7f-4aaa-b9f1-033c4dbfef58'),
  "trackerName" => "your trackerName" # (e.g. 'company.api')
];

$inspetor = new InspetorClient($inspetor_config);

?>
```

The first step of integrating Inspetor's antifraud services into your product is instantiating the library.

In order to do so, you will need to pass the `InspetorClient` your product's **App ID** and **Tracker Name**, both of which will be provided to you by the Inspetor Team.

_Et voilà_! You now have an Inspetor client object that is capable of sending all of the information necessary to teach Inspetor's decision layer how to prevent fraud at your company. However, there is a difference between instantiating a client instance and using it properly.