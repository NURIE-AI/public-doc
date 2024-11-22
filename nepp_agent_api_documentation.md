
# NEPP Agent API Documentation

This document will guide you through using the NEPP Agent API to interact with your AI-powered agents. The NEPP API allows developers to make predictions and ask questions by sending HTTP requests to specific endpoints. Below, you will find the API usage details, including how to authenticate and send requests to the NEPP agent.

## Base URL

All NEPP API endpoints are served from the following base URL:

```
https://agents.nepp.nurie.ai/api/v1/
```

## Authentication

To use the NEPP Agent API, you must authenticate your requests with an API token. This token should be included in the headers of every request you make.

### Authentication Header Example

```
Authorization: Bearer <your_api_token>
```

Replace `<your_api_token>` with the token you received from the NEPP platform.

## Prediction Endpoint

### Endpoint

```
POST /prediction/{agent_id}
```

- **URL**: `https://agents.nepp.nurie.ai/api/v1/prediction/{agent_id}`
- **Method**: `POST`
- **Path Parameters**:
  - `agent_id` (required): The unique ID of the NEPP agent you wish to interact with. The NEPP support team will provide you with this ID.
- **Headers**:
  - `Content-Type`: `application/json`
  - `Authorization`: `Bearer <your_api_token>`

### Request Body

The request body should be in JSON format and include a field called `question`. Additionally, you can optionally include a `chatId` parameter to maintain conversation context.

Example:

```json
{
  "question": "Hey, how are you?",
  "chatId": "12345"
}
```

- `question` (required): The user's question or input.
- `chatId` (optional): A unique identifier for the conversation. If provided, the conversation context will be maintained within the same session. Users must manage the `chatId` themselves.

### Response

The response will include the agent's prediction or response to your question.

Example response:

```json
{
  "response": "I'm an AI, so I'm always here to help!"
}
```

## Example Request

Below is an example of how to use `curl` to make a request to the NEPP Agent API.

```sh
curl https://agents.nepp.nurie.ai/api/v1/prediction/{agent_id}      -X POST      -d '{"question": "Hey, how are you?", "chatId": "12345"}'      -H "Content-Type: application/json"      -H "Authorization: Bearer <your_secret_key>"
```

This example sends a `POST` request to the `/prediction/{agent_id}` endpoint, specifying the question and `chatId` in the request body and including the necessary authentication token in the headers.

## Error Handling

The NEPP Agent API returns standard HTTP error codes to indicate the status of requests:

- `400 Bad Request`: The request was not properly formatted.
- `401 Unauthorized`: Authentication failed. Check your API token.
- `404 Not Found`: The specified agent was not found.
- `500 Internal Server Error`: An error occurred on the server.

## More Information

The default rate limits for API access in NEPP are set to:
- **Message Limit per Duration**: 20 messages
- **Duration in Seconds**: 60 seconds

This means that by default, the system allows up to 20 messages to be processed every minute. If this limit is exceeded, a message such as "Quota Exceeded" will be returned to the user. These settings can be adjusted based on the purchase of seats.

If you have questions or need further support, please contact our support team.
cs@nurie.ai
