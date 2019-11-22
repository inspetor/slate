# Authorization

To use our API, you will need to provide authorization. We grant authorization based on an API key that should be provided in a request header with every request in the following format:

`Authorization: <your API key here>`

The API key is customer-specific and will be provided to you by Inspetor.

## Sandbox API Keys

In the initial stages of your integration, you will probably want to test out a few endpoints to make sure everything is working. It is important that this data is differentiated from your production data; otherwise, our antifraud models will use this test data for training. You can test your integration with our collection service and indicate that you are sending test data by providing a "sandbox" API key. (We will provide you with at the same time we issue your production API key.)
