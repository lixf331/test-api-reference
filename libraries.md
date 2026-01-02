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

from groq import Groq

client = Groq(
    # This is the default and can be omitted
    api_key=os.environ.get("GROQ_API_KEY"),
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
    model="llama-3.3-70b-versatile",
)

print(chat_completion.choices[0].message.content)
```

While you can provide an `api_key` keyword argument, we recommend using [python-dotenv](https://github.com/theskumar/python-dotenv) to add `UFCLOUD_API_KEY="My API Key"` to your `.env` file so that your API Key is not stored in source control.

The following response is generated:

JSON

```json
{
  "id": "34a9110d-c39d-423b-9ab9-9c748747b204",
  "object": "chat.completion",
  "created": 1708045122,
  "model": "mixtral-8x7b-32768",
  "system_fingerprint": "fp_dbffcd8265",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Low latency Large Language Models (LLMs) are important in the field of artificial intelligence and natural language processing (NLP) for several reasons:\n\n1. Real-time applications: Low latency LLMs are essential for real-time applications such as chatbots, voice assistants, and real-time translation services. These applications require immediate responses, and high latency can lead to a poor user experience.\n\n2. Improved user experience: Low latency LLMs provide a more seamless and responsive user experience. Users are more likely to continue using a service that provides quick and accurate responses, leading to higher user engagement and satisfaction.\n\n3. Competitive advantage: In today's fast-paced digital world, businesses that can provide quick and accurate responses to customer inquiries have a competitive advantage. Low latency LLMs can help businesses respond to customer inquiries more quickly, potentially leading to increased sales and customer loyalty.\n\n4. Better decision-making: Low latency LLMs can provide real-time insights and recommendations, enabling businesses to make better decisions more quickly. This can be particularly important in industries such as finance, healthcare, and logistics, where quick decision-making can have a significant impact on business outcomes.\n\n5. Scalability: Low latency LLMs can handle a higher volume of requests, making them more scalable than high-latency models. This is particularly important for businesses that experience spikes in traffic or have a large user base.\n\nIn summary, low latency LLMs are essential for real-time applications, providing a better user experience, enabling quick decision-making, and improving scalability. As the demand for real-time NLP applications continues to grow, the importance of low latency LLMs will only become more critical."
      },
      "finish_reason": "stop",
      "logprobs": null
    }
  ],
  "usage": {
    "prompt_tokens": 24,
    "completion_tokens": 377,
    "total_tokens": 401,
    "prompt_time": 0.009,
    "completion_time": 0.774,
    "total_time": 0.783
  },
  "x_groq": {
    "id": "req_01htzpsmfmew5b4rbmbjy2kv74"
  }
}
```
