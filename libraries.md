---
description: Explore official and community UF Cloud client libraries for Python, JavaScript, and more to access the UF Cloud API easily.
title: UF Cloud Client Libraries - UFCloudDocs
---

# UF Cloud Client Libraries

UF Cloud provides both a Python and JavaScript/Typescript client library.

## UF Cloud Python Library

The UF Cloud Python library provides convenient access to the UF Cloud REST API from any Python 3.9+ application. The library includes type definitions for all request params and response fields, and offers both synchronous and asynchronous clients.

### Download

[ufcloud-0.0.1-py3-none-any.whl](https://github.com/lixf331/test-api-reference/raw/refs/heads/main/ufcloud-0.0.1-py3-none-any.whl)

### Installation

```shell
pip install --force-reinstall --no-deps --no-cache-dir ufcloud-0.0.1-py3-none-any.whl
```

### Usage

Use the library and your secret key to run:

```python
import os

from ufcloud import Ufcloud

client = Ufcloud(
    # This is the default and can be omitted
    api_key=os.environ.get("UFCLOUD_API_KEY"),
)

chat_completion = client.chat.completions.create(
    messages=[
        {
            "role": "system",
            "content": "You are a helpful assistant."
        },
        {
            "role": "user",
            "content": "Explain the importance of fast language models",
        }
    ],
    model="openai/gpt-oss-120b",
)

print(chat_completion.choices[0].message.content)
```

While you can provide an `api_key` keyword argument, we recommend using [python-dotenv](https://github.com/theskumar/python-dotenv) to add `UFCLOUD_API_KEY="My API Key"` to your `.env` file so that your API Key is not stored in source control.

The following response is generated:

JSON

```json
{
  "id": "chatcmpl-66d4869e-db6d-4fcf-84e8-4f0aadd78e0c",
  "object": "chat.completion",
  "created": 1769129522,
  "model": "openai/gpt-oss-120b",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "## Why Speed Matters for Language Models  \n\nLanguage models (LLMs) have become the backbone of many modern AI‑driven products—chatbots, search assistants, code generators, translation tools, and more...",
        "refusal": null,
        "annotations": null,
        "audio": null,
        "function_call": null,
        "tool_calls": [],
        "reasoning_content": "User asks: \"Explain the importance of fast language models\". Need to provide explanation, probably for a general audience, covering benefits: real-time applications, resource constraints, cost, user experience, scaling, edge devices, etc. Should be clear, thorough. No disallowed content. Provide well-structured answer."
      },
      "logprobs": null,
      "finish_reason": "stop",
      "stop_reason": null,
      "token_ids": null
    }
  ],
  "service_tier": null,
  "system_fingerprint": null,
  "usage": {
    "prompt_tokens": 86,
    "total_tokens": 1733,
    "completion_tokens": 1647,
    "prompt_tokens_details": null
  },
  "prompt_logprobs": null,
  "prompt_token_ids": null,
  "kv_transfer_params": null
}
```

## UF Cloud JavaScript Library

The UF Cloud JavaScript library provides convenient access to the UF Cloud REST API from server-side TypeScript or JavaScript. The library includes type definitions for all request params and response fields, and offers both synchronous and asynchronous clients.

### Download

[ufcloud-0.0.1.tgz](https://github.com/lixf331/test-api-reference/raw/refs/heads/main/ufcloud-0.0.1.tgz)

### Installation

```shell
npm uninstall ufcloud

npm install ufcloud-0.0.1.tgz
```

### Usage

Use the library and your secret key to run:

```javascript
import Ufcloud from "ufcloud";

const client = new Ufcloud({
  // This is the default and can be omitted
  apiKey: process.env.UFCLOUD_API_KEY,
});

const chatCompletion = await client.chat.completions.create({
  messages: [
    {
      role: "system",
      content: "You are a helpful assistant.",
    },
    {
      role: "user",
      content: "Explain the importance of fast language models",
    },
  ],
  model: "openai/gpt-oss-120b",
});
console.log(chatCompletion.choices[0].message.content);
```

The following response is generated:

JSON

```json
{
  "id": "chatcmpl-66d4869e-db6d-4fcf-84e8-4f0aadd78e0c",
  "object": "chat.completion",
  "created": 1769129522,
  "model": "openai/gpt-oss-120b",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "## Why Speed Matters for Language Models  \n\nLanguage models (LLMs) have become the backbone of many modern AI‑driven products—chatbots, search assistants, code generators, translation tools, and more...",
        "refusal": null,
        "annotations": null,
        "audio": null,
        "function_call": null,
        "tool_calls": [],
        "reasoning_content": "User asks: \"Explain the importance of fast language models\". Need to provide explanation, probably for a general audience, covering benefits: real-time applications, resource constraints, cost, user experience, scaling, edge devices, etc. Should be clear, thorough. No disallowed content. Provide well-structured answer."
      },
      "logprobs": null,
      "finish_reason": "stop",
      "stop_reason": null,
      "token_ids": null
    }
  ],
  "service_tier": null,
  "system_fingerprint": null,
  "usage": {
    "prompt_tokens": 86,
    "total_tokens": 1733,
    "completion_tokens": 1647,
    "prompt_tokens_details": null
  },
  "prompt_logprobs": null,
  "prompt_token_ids": null,
  "kv_transfer_params": null
}
```
