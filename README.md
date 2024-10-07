# Unofficial Inflection AI Cookbook

Examples and guides for using the [Inflection AI API](https://developers.inflection.ai/). To run these examples you'll need an Inflection AI Developers account and an API key [(sign-up and get your API key here)](https://developers.inflection.ai/login). You can login with a Google or GitHub account.

## Getting Started with the Inflection AI API

Read the latest version of these docs on the [Inflection AI API docs page here](https://developers.inflection.ai/docs).

Inflection-3 comprises two models designed for distinct purposes:

- Pi (3.0): the model powering our Pi experience, including a backstory, emotional intelligence, productivity, and safety. It excels in scenarios such as customer support chatbots. Set the config field in the API request JSON to `inflection_3_pi` to use this model.
- Productivity (3.0): the model optimized for following instructions. It is better for tasks requiring JSON output or precise adherence to provided guidelines. Set the config field in the API request JSON to `inflection_3_productivity` to use this model.

### Context Window
Both models currently support a 8k context window.

### Authentication
To access and interact with the Inflection AI API, every request must include a valid API key. This key serves as a token that authenticates your organization or personal account with the API, ensuring secure and authorized usage. Below, we’ll walk through how to obtain your API key and demonstrate the process of including it in your requests.

### Obtaining your API key
To begin using the Inflection AI API, you need to obtain an API key. Follow these steps to retrieve your key:

1. Go to 'API Keys' page: Once signed in, navigate to the "Keys" section.
2. Create API Key: Click on 'Create API Key' and type in a key name. Key name must be at least 3 characters long.
3. Try it out: Either try using the `cUrl` command provided or go to [Playground page](https://developers.inflection.ai/playground) and try the key out.

### API key format
Your API key is a long string that resembles the following example:
```
nfHB2f...IrQNMm4
```

This key must be included in the headers of all API requests to authenticate the client. Ensure that you replace `nfHB2f...IrQNMm4` with your actual key.

### Including the API key in requests
For each request to the Inflection AI API, include the `Authorization` header with the value `Bearer <YOUR_API_KEY>`.

Here’s an example using `cURL` to authenticate:
```bash
curl --location 'https://layercake.pubwestus3.inf7ks8.com/external/api/inference' \
    --header 'Authorization: Bearer <YOUR_API_KEY>' \
    --header 'Content-Type: application/json' \
    --data '{
        "context": [
            {
                "text": "Hi",
                "type": "Human"
            }
        ],
        "config": "inflection_3_pi"
    }'
```

In this example:

- The `Authorization` header is used to pass your API key.
- The `Bearer` prefix is mandatory and must precede your API key.
- The `Content-Type` header specifies that the request is in JSON format.
- The `--data` flag includes the request payload with the input context and configuration.

### Key management
- **Security**: It is crucial to keep your API key secure and confidential. Avoid exposing it in publicly accessible codebases or client-side applications. If you believe your key has been compromised, you can delete the compromised key and generate a new one through the developer portal.

### Handling authentication errors
In the event of an authentication failure, the API will return an appropriate error message. Below are the common authentication-related error codes:

- **401 Unauthorized**: This error indicates that the API key is missing, invalid, or expired. Ensure that the Authorization header is properly configured with the correct API key.
- **403 Forbidden**: This error occurs when the API key does not have the required permissions to access the requested resource.

Example of an authentication error response:
```json
{
    "detail": "Forbidden"
}
```

In such cases, double-check that the API key is valid and that it has the necessary permissions for the API resources you're accessing.


