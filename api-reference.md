---
description: Comprehensive reference documentation for the UF Cloud API, including endpoints, parameters, and examples.
title: API Reference - UFCloudDocs
---

# UF Cloud API Reference

## Chat

### Create chat completion

**POST {{ BACKEND_HOST_URL }}/openai/v1/chat/completions**

Creates a model response for the given chat conversation.

#### Request Body

```json
{
  "title": "CreateChatCompletionRequest",
  "type": "object",
  "$defs": {
    "ImageURL": {
      "type": "object",
      "properties": {
        "url": {
          "type": "string",
          "title": "Url"
        },
        "detail": {
          "type": "string",
          "enum": ["auto", "low", "high"],
          "title": "Detail"
        }
      },
      "required": ["url"],
      "title": "ImageURL"
    },
    "InputAudio": {
      "type": "object",
      "properties": {
        "data": {
          "type": "string",
          "title": "Data"
        },
        "format": {
          "type": "string",
          "enum": ["wav", "mp3"],
          "title": "Format"
        }
      },
      "required": ["data", "format"],
      "title": "InputAudio"
    },
    "Audio": {
      "type": "object",
      "properties": {
        "id": {
          "type": "string",
          "title": "Id"
        }
      },
      "required": ["id"],
      "title": "Audio"
    },
    "FileFile": {
      "type": "object",
      "properties": {
        "file_data": {
          "type": "string",
          "title": "File Data"
        },
        "file_id": {
          "type": "string",
          "title": "File Id"
        },
        "filename": {
          "type": "string",
          "title": "Filename"
        }
      },
      "title": "FileFile"
    },
    "FunctionCall": {
      "type": "object",
      "description": "Deprecated function call information.",
      "properties": {
        "arguments": {
          "type": "string",
          "title": "Arguments"
        },
        "name": {
          "type": "string",
          "title": "Name"
        }
      },
      "required": ["arguments", "name"],
      "title": "FunctionCall"
    },
    "Function": {
      "type": "object",
      "properties": {
        "arguments": {
          "type": "string",
          "title": "Arguments"
        },
        "name": {
          "type": "string",
          "title": "Name"
        }
      },
      "required": ["arguments", "name"],
      "title": "Function"
    },
    "ChatCompletionContentPartTextParam": {
      "type": "object",
      "properties": {
        "text": {
          "type": "string",
          "title": "Text"
        },
        "type": {
          "type": "string",
          "enum": ["text"],
          "title": "Type"
        }
      },
      "required": ["text", "type"],
      "title": "ChatCompletionContentPartTextParam"
    },
    "ChatCompletionContentPartRefusalParam": {
      "type": "object",
      "properties": {
        "refusal": {
          "type": "string",
          "title": "Refusal"
        },
        "type": {
          "type": "string",
          "enum": ["refusal"],
          "title": "Type"
        }
      },
      "required": ["refusal", "type"],
      "title": "ChatCompletionContentPartRefusalParam"
    },
    "ChatCompletionContentPartImageParam": {
      "type": "object",
      "properties": {
        "image_url": {
          "$ref": "#/$defs/ImageURL"
        },
        "type": {
          "type": "string",
          "enum": ["image_url"],
          "title": "Type"
        }
      },
      "required": ["image_url", "type"],
      "title": "ChatCompletionContentPartImageParam"
    },
    "ChatCompletionContentPartInputAudioParam": {
      "type": "object",
      "properties": {
        "input_audio": {
          "$ref": "#/$defs/InputAudio"
        },
        "type": {
          "type": "string",
          "enum": ["input_audio"],
          "title": "Type"
        }
      },
      "required": ["input_audio", "type"],
      "title": "ChatCompletionContentPartInputAudioParam"
    },
    "File": {
      "type": "object",
      "properties": {
        "file": {
          "$ref": "#/$defs/FileFile"
        },
        "type": {
          "type": "string",
          "enum": ["file"],
          "title": "Type"
        }
      },
      "required": ["file", "type"],
      "title": "File"
    },
    "ChatCompletionMessageToolCallParam": {
      "type": "object",
      "properties": {
        "id": {
          "type": "string",
          "title": "Id"
        },
        "function": {
          "$ref": "#/$defs/Function"
        },
        "type": {
          "type": "string",
          "enum": ["function"],
          "title": "Type"
        }
      },
      "required": ["id", "function", "type"],
      "title": "ChatCompletionMessageToolCallParam"
    },
    "ChatCompletionSystemMessageParam": {
      "type": "object",
      "properties": {
        "content": {
          "anyOf": [
            {
              "type": "string",
              "title": "StringContent"
            },
            {
              "type": "array",
              "title": "ArrayContent",
              "items": {
                "$ref": "#/$defs/ChatCompletionContentPartTextParam"
              }
            }
          ],
          "title": "Content"
        },
        "role": {
          "type": "string",
          "enum": ["system"],
          "title": "Role"
        },
        "name": {
          "type": "string",
          "title": "Name"
        }
      },
      "required": ["content", "role"],
      "title": "System Message"
    },
    "ChatCompletionUserMessageParam": {
      "type": "object",
      "properties": {
        "content": {
          "anyOf": [
            {
              "type": "string",
              "title": "StringContent",
              "description": "Simple text content."
            },
            {
              "type": "array",
              "title": "ArrayContent",
              "items": {
                "anyOf": [
                  {
                    "$ref": "#/$defs/ChatCompletionContentPartTextParam"
                  },
                  {
                    "$ref": "#/$defs/ChatCompletionContentPartImageParam"
                  },
                  {
                    "$ref": "#/$defs/ChatCompletionContentPartInputAudioParam"
                  },
                  {
                    "$ref": "#/$defs/File"
                  }
                ]
              }
            }
          ],
          "title": "Content",
          "description": "The contents of the user message."
        },
        "role": {
          "type": "string",
          "enum": ["user"],
          "title": "Role",
          "description": "The role of the message sender."
        },
        "name": {
          "type": "string",
          "title": "Name",
          "description": "An optional name for the participant."
        }
      },
      "required": ["content", "role"],
      "title": "User Message"
    },
    "ChatCompletionAssistantMessageParam": {
      "type": "object",
      "properties": {
        "role": {
          "type": "string",
          "enum": ["assistant"],
          "title": "Role",
          "description": "The role of the message sender."
        },
        "audio": {
          "$ref": "#/$defs/Audio"
        },
        "content": {
          "anyOf": [
            {
              "type": "string",
              "title": "StringContent"
            },
            {
              "type": "array",
              "title": "ArrayContent",
              "items": {
                "anyOf": [
                  {
                    "$ref": "#/$defs/ChatCompletionContentPartTextParam"
                  },
                  {
                    "$ref": "#/$defs/ChatCompletionContentPartRefusalParam"
                  }
                ]
              }
            }
          ],
          "title": "Content",
          "description": "The contents of the assistant message."
        },
        "function_call": {
          "$ref": "#/$defs/FunctionCall"
        },
        "name": {
          "type": "string",
          "title": "Name",
          "description": "An optional name for the participant."
        },
        "refusal": {
          "type": "string",
          "title": "Refusal",
          "description": "Refusal message if the model refuses to respond."
        },
        "tool_calls": {
          "type": "array",
          "items": {
            "$ref": "#/$defs/ChatCompletionMessageToolCallParam"
          },
          "title": "Tool Calls",
          "description": "The tool calls made by the assistant."
        }
      },
      "required": ["role"],
      "title": "Assistant Message"
    },
    "ChatCompletionToolMessageParam": {
      "type": "object",
      "properties": {
        "content": {
          "anyOf": [
            {
              "type": "string",
              "title": "StringContent"
            },
            {
              "type": "array",
              "title": "ArrayContent",
              "items": {
                "$ref": "#/$defs/ChatCompletionContentPartTextParam"
              }
            }
          ],
          "title": "Content",
          "description": "The contents of the tool message."
        },
        "role": {
          "type": "string",
          "enum": ["tool"],
          "title": "Role",
          "description": "The role of the message sender."
        },
        "tool_call_id": {
          "type": "string",
          "title": "Tool Call Id",
          "description": "The ID of the tool call that this message is responding to."
        }
      },
      "required": ["role", "content", "tool_call_id"],
      "title": "Tool Message"
    },
    "ChatCompletionFunctionMessageParam": {
      "type": "object",
      "properties": {
        "content": {
          "type": "string",
          "title": "Content",
          "description": "The contents of the function message."
        },
        "name": {
          "type": "string",
          "title": "Name",
          "description": "The name of the function that this message is responding to."
        },
        "role": {
          "type": "string",
          "enum": ["function"],
          "title": "Role",
          "description": "The role of the message sender."
        }
      },
      "required": ["role", "content", "name"],
      "title": "Function Message"
    },
    "ChatCompletionDeveloperMessageParam": {
      "type": "object",
      "properties": {
        "content": {
          "anyOf": [
            {
              "type": "string",
              "title": "StringContent"
            },
            {
              "type": "array",
              "title": "ArrayContent",
              "items": {
                "$ref": "#/$defs/ChatCompletionContentPartTextParam"
              }
            }
          ],
          "title": "Content",
          "description": "The contents of the developer message."
        },
        "role": {
          "type": "string",
          "enum": ["developer"],
          "title": "Role",
          "description": "The role of the message sender."
        },
        "name": {
          "type": "string",
          "title": "Name",
          "description": "An optional name for the participant."
        }
      },
      "required": ["role", "content"],
      "title": "Developer Message"
    },
    "LogitsProcessorConstructor": {
      "type": "object",
      "properties": {
        "qualname": {
          "type": "string",
          "title": "Qualname"
        },
        "args": {
          "type": "array",
          "items": {
            "type": "object"
          },
          "title": "Args"
        },
        "kwargs": {
          "type": "object",
          "title": "Kwargs"
        }
      },
      "required": ["qualname"],
      "title": "LogitsProcessorConstructor"
    },
    "StreamOptions": {
      "type": "object",
      "properties": {
        "include_usage": {
          "type": "boolean",
          "default": true,
          "title": "Include Usage",
          "description": "Whether to include usage statistics in streaming responses. If true, usage information (tokens used, etc.) will be included in the stream events."
        },
        "continuous_usage_stats": {
          "type": "boolean",
          "default": false,
          "title": "Continuous Usage Stats",
          "description": "Whether to include usage statistics in each streaming chunk. If true, usage stats are included continuously as tokens are generated. If false, usage stats are only included in the final message."
        }
      },
      "title": "StreamOptions"
    },
    "JsonSchemaResponseFormat": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string",
          "title": "Name"
        },
        "description": {
          "type": "string",
          "title": "Description"
        },
        "schema": {
          "type": "object",
          "title": "Schema"
        },
        "strict": {
          "type": "boolean",
          "title": "Strict"
        }
      },
      "required": ["name"],
      "title": "JsonSchemaResponseFormat"
    },
    "StructuralTag": {
      "type": "object",
      "properties": {
        "begin": {
          "type": "string",
          "title": "Begin"
        },
        "schema": {
          "type": "object",
          "title": "Schema"
        },
        "end": {
          "type": "string",
          "title": "End"
        }
      },
      "required": ["begin", "end"],
      "title": "StructuralTag"
    },
    "ResponseFormat": {
      "type": "object",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["text", "json_object", "json_schema"],
          "title": "Type"
        },
        "json_schema": {
          "$ref": "#/$defs/JsonSchemaResponseFormat"
        }
      },
      "required": ["type"],
      "title": "ResponseFormat"
    },
    "StructuralTagResponseFormat": {
      "type": "object",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["structural_tag"],
          "title": "Type"
        },
        "structures": {
          "type": "array",
          "items": {
            "$ref": "#/$defs/StructuralTag"
          },
          "title": "Structures"
        },
        "triggers": {
          "type": "array",
          "items": {
            "type": "string"
          },
          "title": "Triggers"
        }
      },
      "required": ["type", "structures", "triggers"],
      "title": "StructuralTagResponseFormat"
    },
    "FunctionDefinition": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string",
          "title": "Name"
        },
        "description": {
          "type": "string",
          "title": "Description"
        },
        "parameters": {
          "type": "object",
          "title": "Parameters"
        }
      },
      "required": ["name"],
      "title": "FunctionDefinition"
    },
    "ChatCompletionToolsParam": {
      "type": "object",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["function"],
          "title": "Type",
          "default": "function"
        },
        "function": {
          "$ref": "#/$defs/FunctionDefinition"
        }
      },
      "required": ["function"],
      "title": "ChatCompletionToolsParam"
    },
    "ChatCompletionNamedFunction": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string",
          "title": "Name"
        }
      },
      "required": ["name"],
      "title": "ChatCompletionNamedFunction"
    },
    "ChatCompletionNamedToolChoiceParam": {
      "type": "object",
      "properties": {
        "function": {
          "$ref": "#/$defs/ChatCompletionNamedFunction"
        },
        "type": {
          "type": "string",
          "enum": ["function"],
          "title": "Type",
          "default": "function"
        }
      },
      "required": ["function"],
      "title": "ChatCompletionNamedToolChoiceParam"
    }
  },
  "properties": {
    "messages": {
      "description": "A list of messages comprising the conversation so far.",
      "type": "array",
      "items": {
        "anyOf": [
          {
            "$ref": "#/$defs/ChatCompletionDeveloperMessageParam"
          },
          {
            "$ref": "#/$defs/ChatCompletionSystemMessageParam"
          },
          {
            "$ref": "#/$defs/ChatCompletionUserMessageParam"
          },
          {
            "$ref": "#/$defs/ChatCompletionAssistantMessageParam"
          },
          {
            "$ref": "#/$defs/ChatCompletionToolMessageParam"
          },
          {
            "$ref": "#/$defs/ChatCompletionFunctionMessageParam"
          }
        ]
      }
    },
    "model": {
      "description": "ID of the model to use.",
      "type": "string"
    },
    "n": {
      "type": "integer",
      "default": 1,
      "description": "How many chat completion choices to generate for each input message."
    },
    "best_of": {
      "type": "integer",
      "description": "Generate multiple completions and return the best one. Ignored when n is set."
    },
    "temperature": {
      "type": "number",
      "minimum": 0,
      "maximum": 2,
      "description": "What sampling temperature to use, between 0 and 2. Higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic. We generally recommend altering this or top_p but not both."
    },
    "presence_penalty": {
      "type": "number",
      "minimum": -2,
      "maximum": 2,
      "description": "Number between -2.0 and 2.0. Positive values penalize new tokens based on whether they appear in the text so far, increasing the model's likelihood to talk about new topics."
    },
    "frequency_penalty": {
      "type": "number",
      "minimum": -2,
      "maximum": 2,
      "description": "Number between -2.0 and 2.0. Positive values penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim."
    },
    "repetition_penalty": {
      "type": "number",
      "description": "Penalty for repeating tokens. Values > 1.0 reduce repetition. Default is 1.0 (no penalty). Higher values (e.g., 1.2) make the model less likely to repeat the same token."
    },
    "top_p": {
      "type": "number",
      "minimum": 0,
      "maximum": 1,
      "description": "An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So 0.1 means only the tokens comprising the top 10% probability mass are considered. We generally recommend altering this or temperature but not both."
    },
    "top_k": {
      "type": "integer",
      "description": "Limit sampling to the top K most likely tokens. For example, top_k=10 means only the 10 most probable tokens are considered. Lower values make output more focused, higher values more diverse."
    },
    "min_p": {
      "type": "number",
      "minimum": 0,
      "maximum": 1,
      "description": "Minimum probability threshold relative to the most likely token. Only tokens with probability >= (max_probability * min_p) are considered. For example, if the top token has probability 0.4 and min_p=0.1, only tokens with probability >= 0.04 are sampled."
    },
    "seed": {
      "type": "integer",
      "description": "If specified, our system will make a best effort to sample deterministically, such that repeated requests with the same seed and parameters should return the same result."
    },
    "stop": {
      "oneOf": [
        {
          "type": "string"
        },
        {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      ],
      "description": "where the API will stop generating further tokens. The returned text will not contain the stop sequence."
    },
    "stop_token_ids": {
      "type": "array",
      "items": {
        "type": "integer"
      },
      "description": "List of token IDs where the API will stop generating further tokens. The returned text will not contain these tokens. Useful when you know specific token IDs to stop at (e.g., end-of-text tokens)."
    },
    "include_stop_str_in_output": {
      "type": "boolean",
      "default": false,
      "description": "If true, the stop sequence that triggered the stop will be included in the output text. By default (false), stop sequences are removed from the output."
    },
    "ignore_eos": {
      "type": "boolean",
      "default": false,
      "description": "If true, ignore the EOS (End of Sequence) token and continue generating. When false, generation stops when EOS token is encountered."
    },
    "max_tokens": {
      "type": "integer",
      "description": "The maximum number of tokens that can be generated in the chat completion. The total length of input tokens and generated tokens is limited by the model's context length."
    },
    "min_tokens": {
      "type": "integer",
      "description": "The minimum number of tokens to generate. Generation will continue until at least this many tokens are produced, even if stop sequences or EOS tokens are encountered. Useful for ensuring a minimum response length."
    },
    "logprobs": {
      "type": "boolean",
      "default": false,
      "description": "Whether to return log probabilities of the output tokens or not. If true, returns the log probabilities of each output token returned in the content of message."
    },
    "prompt_logprobs": {
      "type": "integer",
      "description": "Number of most likely tokens to return at each prompt token position, from the end of the prompt. For example, prompt_logprobs=5 will return the top 5 most likely tokens and their log probabilities for the last 5 tokens in the prompt. Useful for analyzing model confidence on input."
    },
    "skip_special_tokens": {
      "type": "boolean",
      "default": true,
      "description": "Whether to skip special tokens (e.g., BOS, EOS, padding tokens) in the output text. If true, special tokens are filtered out from the response. If false, special tokens are included in the output, which may be useful for debugging or token-level analysis."
    },
    "spaces_between_special_tokens": {
      "type": "boolean",
      "default": true,
      "description": "Whether to add spaces between special tokens when decoding. If true, spaces are inserted between special tokens in the output. If false, special tokens are concatenated without spaces. This affects the formatting of the decoded text output."
    },
    "logits_processors": {
      "type": "array",
      "items": {
        "anyOf": [
          {
            "type": "string",
            "title": "StringContent"
          },
          {
            "$ref": "#/$defs/LogitsProcessorConstructor"
          }
        ]
      },
      "title": "Logits Processors",
      "description": "A list of either qualified names of logits processors, or constructor objects, to apply when sampling. A constructor is a JSON object with a required 'qualname' field specifying the qualified name of the processor class/factory, and optional 'args' and 'kwargs' fields containing positional and keyword arguments. For example: {'qualname': 'my_module.MyLogitsProcessor', 'args': [1, 2], 'kwargs': {'param': 'value'}}."
    },
    "truncate_prompt_tokens": {
      "type": "integer",
      "minimum": -1,
      "title": "Truncate Prompt Tokens",
      "description": "Maximum number of prompt tokens to keep. If prompt exceeds this limit, tokens will be truncated. Use -1 to disable truncation. Positive values truncate from the beginning, keeping the end. Useful when prompt is too long for the model's context window."
    },
    "output_kind": {
      "type": "string",
      "enum": ["cumulative", "delta", "final_only"],
      "title": "Output Kind",
      "description": "Controls the format of streaming output for incremental text generation. - cumulative: Return the full accumulated text so far (default for most use cases). - delta: Return only the newly generated tokens since the last update (useful for streaming UIs). - final_only: Return only the complete final response, no intermediate updates."
    },
    "logit_bias": {
      "type": "object",
      "additionalProperties": {
        "type": "integer"
      },
      "description": "Modify the likelihood of specified tokens appearing in the completion. Accepts a JSON object that maps tokens (specified by their token ID in the tokenizer) to an associated bias value from -100 to 100. Mathematically, the bias is added to the logits generated by the model prior to sampling. The exact effect will vary per model, but values between -1 and 1 should decrease or increase likelihood of selection; values like -100 or 100 should result in a ban or exclusive selection of the relevant token."
    },
    "allowed_token_ids": {
      "type": "array",
      "items": {
        "type": "integer"
      },
      "description": "Whitelist of token IDs that can be generated. Only tokens in this list will be considered during sampling. If specified, all other tokens are excluded. Useful for constrained generation, structured output, or limiting output to specific vocabulary (e.g., only numbers, only specific keywords). If null, all tokens are allowed."
    },
    "extra_args": {
      "type": "object",
      "description": "Additional model-specific or implementation-specific arguments not covered by standard parameters. This allows passing custom parameters that may be specific to certain models or backends. The structure and accepted keys depend on the model and implementation being used."
    },
    "stream": {
      "type": "boolean",
      "default": false,
      "description": "If set, partial message deltas will be sent. Tokens will be sent as data-only server-sent events as they become available, with the stream terminated by a data: [DONE] message."
    },
    "stream_options": {
      "$ref": "#/$defs/StreamOptions",
      "description": "Options for controlling streaming behavior. Only used when stream is true. Controls whether usage statistics are included and how they are reported during streaming."
    },
    "response_format": {
      "anyOf": [
        {
          "$ref": "#/$defs/ResponseFormat"
        },
        {
          "$ref": "#/$defs/StructuralTagResponseFormat"
        }
      ],
      "description": "Specifies the format of the response. Controls how the model structures its output. - text: Plain text output (default) - json_object: Ensures the response is valid JSON - json_schema: Validates response against a JSON schema - structural_tag: Uses custom structural tags for structured output"
    },
    "tools": {
      "type": "array",
      "items": {
        "$ref": "#/$defs/ChatCompletionToolsParam"
      },
      "description": "A list of tools (functions) the model may call. The model can choose to call one or more of these functions during the conversation. Each tool defines a function with a name, description, and parameters (JSON schema). The model will generate function calls in a structured format when it determines a function should be invoked."
    },
    "tool_choice": {
      "anyOf": [
        {
          "type": "string",
          "title": "StringContent",
          "enum": ["none", "auto", "required"]
        },
        {
          "$ref": "#/$defs/ChatCompletionNamedToolChoiceParam",
          "title": "ChatCompletionNamedToolChoiceParam"
        }
      ],
      "default": "none",
      "description": "Controls which (if any) tool is called by the model. none means the model will not call any tool and instead generates a message. auto means the model can pick between generating a message or calling one or more tools. required means the model must call one or more tools. Specifying a particular tool via {\"type\": \"function\", \"function\": {\"name\": \"my_function\"}} forces the model to call that tool. none is the default when no tools are present. auto is the default if tools are present."
    },
    "extra_body": {
      "type": "object",
      "description": "Additional parameters to include in the request body that are not part of the standard API schema. These parameters are passed directly to the underlying model or backend service. Useful for accessing experimental features, model-specific options, or implementation-specific parameters that haven't been standardized yet. The structure and accepted keys depend on the specific model and backend implementation being used."
    },
    "reasoning_effort": {
      "type": "string",
      "enum": ["low", "medium", "high"],
      "description": "Controls the amount of reasoning effort the model applies when generating responses. Higher values typically result in more thorough reasoning but may increase latency and cost."
    },
    "chat_template_kwargs": {
      "type": "object",
      "description": "Additional keyword args to pass to the template renderer. Will be accessible by the chat template."
    }
  },
  "required": ["model", "messages"]
}
```

#### Response Object

```json
{
  "title": "CreateChatCompletionResponse",
  "type": "object",
  "$defs": {
    "Logprob": {
      "type": "object",
      "properties": {
        "logprob": {
          "type": "number",
          "title": "Logprob",
          "description": "The logprob of chosen token."
        },
        "rank": {
          "type": "integer",
          "title": "Rank",
          "description": "The vocab rank of chosen token (>=1)."
        },
        "decoded_token": {
          "type": "string",
          "title": "Decoded Token",
          "description": "The decoded chosen token index"
        }
      },
      "required": ["logprob"],
      "title": "Logprob"
    },
    "ChatCompletionLogProb": {
      "type": "object",
      "properties": {
        "token": {
          "type": "string",
          "title": "Token",
          "description": "The token."
        },
        "logprob": {
          "type": "number",
          "default": -9999.0,
          "title": "Logprob",
          "description": "The log probability of the token."
        },
        "bytes": {
          "type": "array",
          "items": {
            "type": "integer"
          },
          "title": "Bytes",
          "description": "A list of integers representing the UTF-8 bytes representation of the token."
        }
      },
      "required": ["token", "logprob"],
      "title": "ChatCompletionLogProb"
    },
    "ChatCompletionLogProbsContent": {
      "allOf": [
        {
          "$ref": "#/$defs/ChatCompletionLogProb"
        },
        {
          "type": "object",
          "properties": {
            "top_logprobs": {
              "type": "array",
              "items": {
                "$ref": "#/$defs/ChatCompletionLogProb"
              },
              "title": "Top Logprobs",
              "description": "List of top log probabilities for alternative tokens."
            }
          }
        }
      ],
      "title": "ChatCompletionLogProbsContent"
    },
    "ChatCompletionLogProbs": {
      "type": "object",
      "description": "Log probability information for the choice.",
      "properties": {
        "content": {
          "type": "array",
          "items": {
            "$ref": "#/$defs/ChatCompletionLogProbsContent"
          },
          "title": "Content",
          "description": "A list of message content tokens with log probability information."
        }
      },
      "title": "ChatCompletionLogProbs"
    },
    "FunctionCall": {
      "type": "object",
      "description": "Deprecated function call information.",
      "properties": {
        "arguments": {
          "type": "string",
          "title": "Arguments"
        },
        "name": {
          "type": "string",
          "title": "Name"
        }
      },
      "required": ["arguments", "name"],
      "title": "FunctionCall"
    },
    "ToolCall": {
      "type": "object",
      "properties": {
        "id": {
          "type": "string",
          "title": "Id",
          "description": "The ID of the tool call."
        },
        "type": {
          "type": "string",
          "enum": ["function"],
          "default": "function",
          "title": "Type",
          "description": "The type of the tool. Currently, only function is supported."
        },
        "function": {
          "$ref": "#/$defs/FunctionCall"
        }
      },
      "required": ["id", "type", "function"],
      "title": "ToolCall"
    },
    "ChatMessage": {
      "type": "object",
      "properties": {
        "role": {
          "type": "string",
          "title": "Role",
          "description": "The role of the author of this message."
        },
        "content": {
          "type": "string",
          "title": "Content",
          "description": "The content of the message."
        },
        "refusal": {
          "type": "string",
          "title": "Refusal",
          "description": "Refusal message if the model refuses to respond."
        },
        "annotations": {
          "type": "object",
          "title": "Annotations",
          "description": "OpenAI annotation information."
        },
        "audio": {
          "type": "object",
          "title": "Audio",
          "description": "OpenAI chat completion audio information."
        },
        "function_call": {
          "$ref": "#/$defs/FunctionCall"
        },
        "tool_calls": {
          "type": "array",
          "items": {
            "$ref": "#/$defs/ToolCall"
          },
          "title": "Tool Calls",
          "description": "List of tool calls made by the model."
        },
        "reasoning": {
          "type": "string",
          "title": "Reasoning",
          "description": "Reasoning content generated by the model."
        },
        "reasoning_content": {
          "type": "string",
          "title": "Reasoning Content",
          "description": "Reasoning content generated by the model."
        }
      },
      "required": ["role"],
      "title": "ChatMessage"
    },
    "PromptTokensDetails": {
      "type": "object",
      "properties": {
        "cached_tokens": {
          "type": "integer",
          "title": "Cached Tokens",
          "description": "Number of tokens that were cached and reused."
        }
      },
      "title": "PromptTokensDetails"
    },
    "UsageInfo": {
      "type": "object",
      "description": "Usage statistics for the completion request.",
      "properties": {
        "prompt_tokens": {
          "type": "integer",
          "title": "Prompt Tokens",
          "description": "Number of tokens in the prompt."
        },
        "total_tokens": {
          "type": "integer",
          "title": "Total Tokens",
          "description": "Total number of tokens used in the request (prompt + completion)."
        },
        "completion_tokens": {
          "type": "integer",
          "title": "Completion Tokens",
          "description": "Number of tokens in the generated completion."
        },
        "prompt_tokens_details": {
          "$ref": "#/$defs/PromptTokensDetails",
          "description": "Breakdown of tokens in the prompt."
        }
      },
      "required": ["prompt_tokens", "total_tokens"],
      "title": "UsageInfo"
    },
    "ChatCompletionResponseChoice": {
      "type": "object",
      "properties": {
        "index": {
          "type": "integer",
          "title": "Index",
          "description": "The index of the choice in the list of choices."
        },
        "message": {
          "$ref": "#/$defs/ChatMessage"
        },
        "logprobs": {
          "$ref": "#/$defs/ChatCompletionLogProbs"
        },
        "finish_reason": {
          "type": "string",
          "default": "stop",
          "title": "Finish Reason",
          "description": "The reason the model stopped generating tokens."
        },
        "stop_reason": {
          "anyOf": [
            {
              "type": "integer"
            },
            {
              "type": "string"
            }
          ],
          "title": "Stop Reason",
          "description": "Not part of OpenAI spec but included for legacy reasons."
        },
        "token_ids": {
          "type": "array",
          "items": {
            "type": "integer"
          },
          "title": "Token Ids",
          "description": "Not part of OpenAI spec but useful for tracing tokens in agent scenarios."
        }
      },
      "required": ["index", "message"],
      "title": "ChatCompletionResponseChoice"
    }
  },
  "properties": {
    "id": {
      "type": "string",
      "title": "Id",
      "description": "A unique identifier for the chat completion."
    },
    "object": {
      "type": "string",
      "enum": ["chat.completion"],
      "title": "Object",
      "description": "The object type, which is always `chat.completion`."
    },
    "created": {
      "type": "integer",
      "title": "Created",
      "description": "The Unix timestamp (in seconds) of when the chat completion was created."
    },
    "model": {
      "type": "string",
      "title": "Model",
      "description": "The model used for the chat completion."
    },
    "choices": {
      "type": "array",
      "items": {
        "$ref": "#/$defs/ChatCompletionResponseChoice"
      },
      "title": "Choices",
      "description": "A list of chat completion choices. Can be more than one if `n` is greater than 1."
    },
    "service_tier": {
      "type": "string",
      "enum": ["auto", "default", "flex", "scale", "priority"],
      "title": "Service Tier",
      "description": "The service tier used for the request."
    },
    "system_fingerprint": {
      "type": "string",
      "title": "System Fingerprint",
      "description": "This fingerprint represents the backend configuration that the model runs with.\n\nCan be used in conjunction with the `seed` request parameter to understand when backend changes have been made that might impact determinism."
    },
    "usage": {
      "$ref": "#/$defs/UsageInfo"
    },
    "prompt_logprobs": {
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": {
          "$ref": "#/$defs/Logprob"
        }
      },
      "title": "Prompt Logprobs",
      "description": "Array of dictionaries or null values, where each dictionary maps token index (as string) to a Logprob object containing log probability, rank, and decoded token information. Each element can be a dictionary (dict[int, Logprob]) or null. The entire field can also be null. The length of this array should match the number of prompt tokens reported in the usage statistics."
    },
    "prompt_token_ids": {
      "type": "array",
      "items": {
        "type": "integer"
      },
      "title": "Prompt Token Ids",
      "description": "Array of token IDs representing how the prompt was tokenized by the model's tokenizer. Each integer corresponds to a token ID in the tokenizer's vocabulary. This field is useful for debugging tokenization, verifying token counts against `usage.prompt_tokens`, and performing token-level analysis. The length of this array should match the number of prompt tokens reported in the usage statistics."
    },
    "kv_transfer_params": {
      "type": "object",
      "title": "Kv Transfer Params",
      "description": "KVTransfer parameters."
    }
  },
  "required": ["choices", "created", "id", "model", "object"],
  "description": "Represents a chat completion response returned by model, based on the provided input."
}
```

#### Example Requests

- cURL

```curl
curl "{{ BACKEND_HOST_URL }}/openai/v1/chat/completions" \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${UFCLOUD_API_KEY}" \
  -d '{
        "messages": [
          {
            "role": "user",
            "content": "Explain the importance of fast language models"
          }
        ],
        "model": "deepseek-ai/DeepSeek-R1"
      }'
```

- Python SDK

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
            "role": "user",
            "content": "Explain the importance of fast language models",
        }
    ],
    model="deepseek-ai/DeepSeek-R1",
)

print(chat_completion.choices[0].message.content)
```

- TypeScript SDK

```javascript
import Ufcloud from "ufcloud";

const client = new Ufcloud({
  // This is the default and can be omitted
  apiKey: process.env.UFCLOUD_API_KEY,
});

const chatCompletion = await client.chat.completions.create({
  messages: [
    {
      role: "user",
      content: "Explain the importance of fast language models",
    },
  ],
  model: "deepseek-ai/DeepSeek-R1",
});
console.log(chatCompletion.choices[0].message.content);
```

- OpenAI Python

```python
import os

from openai import OpenAI

client = OpenAI(
    base_url="{{ BACKEND_HOST_URL }}/openai/v1",
    # This is the default and can be omitted
    api_key=os.environ.get("UFCLOUD_API_KEY"),
)

chat_completion = client.chat.completions.create(
    messages=[
        {
            "role": "user",
            "content": "Explain the importance of fast language models",
        }
    ],
    model="deepseek-ai/DeepSeek-R1",
)

print(chat_completion.choices[0].message.content)
```

- OpenAI TS

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "{{ BACKEND_HOST_URL }}/openai/v1",
  // This is the default and can be omitted
  apiKey: process.env.UFCLOUD_API_KEY,
});

const chatCompletion = await client.chat.completions.create({
  messages: [
    {
      role: "user",
      content: "Explain the importance of fast language models",
    },
  ],
  model: "deepseek-ai/DeepSeek-R1",
});

console.log(chatCompletion.choices[0].message.content);
```

#### Example Response

```json
{
  "id": "chatcmpl-5c027541-5867-4e79-945a-c89b5efb87a2",
  "object": "chat.completion",
  "created": 1767577856,
  "model": "deepseek-ai/DeepSeek-R1",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Okay, so I need to explain the importance of fast language models ...",
        "refusal": null,
        "annotations": null,
        "audio": null,
        "function_call": null,
        "tool_calls": [],
        "reasoning": null,
        "reasoning_content": null
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
    "prompt_tokens": 12,
    "total_tokens": 1143,
    "completion_tokens": 1131,
    "prompt_tokens_details": null
  },
  "prompt_logprobs": null,
  "prompt_token_ids": null,
  "kv_transfer_params": null
}
```

## Responses

### Create response

**POST {{ BACKEND_HOST_URL }}/openai/v1/responses**

Creates a model response for the given input.

#### Request Body

```json
{
  "title": "CreateResponseRequest",
  "type": "object",
  "$defs": {
    "InputTextContent": {
      "type": "object",
      "title": "Input text",
      "description": "A text input to the model.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["input_text"],
          "description": "The type of the input item. Always `input_text`."
        },
        "text": {
          "type": "string",
          "description": "The text input to the model."
        }
      },
      "required": ["type", "text"]
    },
    "InputImageContent": {
      "type": "object",
      "title": "Input image",
      "description": "An image input to the model.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["input_image"],
          "description": "The type of the input item. Always `input_image`."
        },
        "image_url": {
          "type": "string",
          "description": "The URL of the image to be sent to the model. A fully qualified URL or base64 encoded image in a data URL."
        },
        "file_id": {
          "type": "string",
          "description": "The ID of the file to be sent to the model."
        },
        "detail": {
          "type": "string",
          "enum": ["low", "high", "auto"],
          "description": "The detail level of the image to be sent to the model. One of `high`, `low`, or `auto`."
        }
      },
      "required": ["type", "detail"]
    },
    "InputFileContent": {
      "type": "object",
      "title": "Input file",
      "description": "A file input to the model.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["input_file"],
          "description": "The type of the input item. Always `input_file`."
        },
        "file_id": {
          "type": "string",
          "description": "The ID of the file to be sent to the model."
        },
        "filename": {
          "type": "string",
          "description": "The name of the file to be sent to the model."
        },
        "file_url": {
          "type": "string",
          "description": "The URL of the file to be sent to the model."
        },
        "file_data": {
          "type": "string",
          "description": "The content of the file to be sent to the model."
        }
      },
      "required": ["type"]
    },
    "FileCitationBody": {
      "type": "object",
      "title": "File citation",
      "description": "A citation to a file.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["file_citation"],
          "description": "The type of the file citation. Always `file_citation`."
        },
        "file_id": {
          "type": "string",
          "description": "The ID of the file."
        },
        "index": {
          "type": "integer",
          "description": "The index of the file in the list of files."
        },
        "filename": {
          "type": "string",
          "description": "The filename of the file cited."
        }
      },
      "required": ["type", "file_id", "index", "filename"]
    },
    "UrlCitationBody": {
      "type": "object",
      "title": "URL citation",
      "description": "A citation for a web resource used to generate a model response.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["url_citation"],
          "description": "The type of the URL citation. Always `url_citation`."
        },
        "url": {
          "type": "string",
          "description": "The URL of the web resource."
        },
        "start_index": {
          "type": "integer",
          "description": "The index of the first character of the URL citation in the message."
        },
        "end_index": {
          "type": "integer",
          "description": "The index of the last character of the URL citation in the message."
        },
        "title": {
          "type": "string",
          "description": "The title of the web resource."
        }
      },
      "required": ["type", "url", "start_index", "end_index", "title"]
    },
    "ContainerFileCitationBody": {
      "type": "object",
      "title": "Container file citation",
      "description": "A citation for a container file used to generate a model response.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["container_file_citation"],
          "description": "The type of the container file citation. Always `container_file_citation`."
        },
        "container_id": {
          "type": "string",
          "description": "The ID of the container file."
        },
        "file_id": {
          "type": "string",
          "description": "The ID of the file."
        },
        "start_index": {
          "type": "integer",
          "description": "The index of the first character of the container file citation in the message."
        },
        "end_index": {
          "type": "integer",
          "description": "The index of the last character of the container file citation in the message."
        },
        "filename": {
          "type": "string",
          "description": "The filename of the container file cited."
        }
      },
      "required": [
        "type",
        "container_id",
        "file_id",
        "start_index",
        "end_index",
        "filename"
      ]
    },
    "FilePath": {
      "type": "object",
      "title": "File path",
      "description": "A path to a file.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["file_path"],
          "description": "The type of the file path. Always `file_path`."
        },
        "file_id": {
          "type": "string",
          "description": "The ID of the file."
        },
        "index": {
          "type": "integer",
          "description": "The index of the file in the list of files."
        }
      },
      "required": ["type", "file_id", "index"]
    },
    "EasyInputMessage": {
      "type": "object",
      "title": "Input message",
      "description": "A message input to the model with a role indicating instruction following hierarchy. Instructions given with the `developer` or `system` role take precedence over instructions given with the `user` role. Messages with the `assistant` role are presumed to have been generated by the model in previous interactions.",
      "properties": {
        "role": {
          "type": "string",
          "enum": ["user", "assistant", "system", "developer"],
          "description": "The role of the message input. One of `user`, `assistant`, `system`, or `developer`."
        },
        "content": {
          "description": "Text, image, or audio input to the model, used to generate a response. Can also contain previous assistant responses.",
          "anyOf": [
            {
              "type": "string",
              "title": "Text input",
              "description": "A text input to the model."
            },
            {
              "type": "array",
              "title": "Input item content list",
              "description": "A list of one or many input items to the model, containing different content types.",
              "items": {
                "anyOf": [
                  {
                    "$ref": "#/$defs/InputTextContent"
                  },
                  {
                    "$ref": "#/$defs/InputImageContent"
                  },
                  {
                    "$ref": "#/$defs/InputFileContent"
                  }
                ]
              }
            }
          ]
        },
        "type": {
          "type": "string",
          "enum": ["message"],
          "description": "The type of the message input. Always `message`."
        }
      },
      "required": ["role", "content"]
    },
    "OutputTextContent": {
      "type": "object",
      "title": "Output text",
      "description": "A text output from the model.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["output_text"],
          "description": "The type of the output text. Always `output_text`."
        },
        "text": {
          "type": "string",
          "description": "The text output from the model."
        },
        "annotations": {
          "type": "array",
          "description": "The annotations of the text output.",
          "items": {
            "anyOf": [
              {
                "$ref": "#/$defs/FileCitationBody"
              },
              {
                "$ref": "#/$defs/UrlCitationBody"
              },
              {
                "$ref": "#/$defs/ContainerFileCitationBody"
              },
              {
                "$ref": "#/$defs/FilePath"
              }
            ]
          }
        },
        "logprobs": {
          "type": "array",
          "description": "Log probability information for the output."
        }
      },
      "required": ["type", "text", "annotations"]
    },
    "RefusalContent": {
      "type": "object",
      "title": "Refusal",
      "description": "A refusal from the model.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["refusal"],
          "description": "The type of the refusal. Always `refusal`."
        },
        "refusal": {
          "type": "string",
          "description": "The refusal explanation from the model."
        }
      },
      "required": ["type", "refusal"]
    },
    "ClickParam": {
      "type": "object",
      "title": "Click",
      "description": "A click action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["click"],
          "description": "Specifies the event type. For a click action, this property is always `click`."
        },
        "button": {
          "type": "string",
          "enum": ["left", "right", "wheel", "back", "forward"],
          "description": "Indicates which mouse button was pressed during the click. One of `left`, `right`, `wheel`, `back`, or `forward`."
        },
        "x": {
          "type": "integer",
          "description": "The x-coordinate where the click occurred."
        },
        "y": {
          "type": "integer",
          "description": "The y-coordinate where the click occurred."
        }
      },
      "required": ["type", "button", "x", "y"]
    },
    "DoubleClickAction": {
      "type": "object",
      "title": "DoubleClick",
      "description": "A double click action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["double_click"],
          "description": "Specifies the event type. For a double click action, this property is always set to `double_click`."
        },
        "x": {
          "type": "integer",
          "description": "The x-coordinate where the double click occurred."
        },
        "y": {
          "type": "integer",
          "description": "The y-coordinate where the double click occurred."
        }
      },
      "required": ["type", "x", "y"]
    },
    "Drag": {
      "type": "object",
      "title": "Drag",
      "description": "A drag action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["drag"],
          "description": "Specifies the event type. For a drag action, this property is always set to `drag`."
        },
        "path": {
          "type": "array",
          "description": "An array of coordinates representing the path of the drag action. Coordinates will appear as an array of objects, eg [{ x: 100, y: 200 }, { x: 200, y: 300 }]",
          "items": {
            "type": "object",
            "title": "Coordinate",
            "description": "An x/y coordinate pair, e.g. `{ x: 100, y: 200 }`.",
            "properties": {
              "x": {
                "type": "integer",
                "description": "The x-coordinate."
              },
              "y": {
                "type": "integer",
                "description": "The y-coordinate."
              }
            },
            "required": ["x", "y"]
          }
        }
      },
      "required": ["type", "path"]
    },
    "KeyPressAction": {
      "type": "object",
      "title": "KeyPress",
      "description": "A collection of keypresses the model would like to perform.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["keypress"],
          "description": "Specifies the event type. For a keypress action, this property is always set to `keypress`."
        },
        "keys": {
          "type": "array",
          "description": "The combination of keys the model is requesting to be pressed. This is an array of strings, each representing a key.",
          "items": {
            "type": "string"
          }
        }
      },
      "required": ["type", "keys"]
    },
    "Move": {
      "type": "object",
      "title": "Move",
      "description": "A mouse move action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["move"],
          "description": "Specifies the event type. For a move action, this property is always set to `move`."
        },
        "x": {
          "type": "integer",
          "description": "The x-coordinate to move to."
        },
        "y": {
          "type": "integer",
          "description": "The y-coordinate to move to."
        }
      },
      "required": ["type", "x", "y"]
    },
    "Screenshot": {
      "type": "object",
      "title": "Screenshot",
      "description": "A screenshot action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["screenshot"],
          "description": "Specifies the event type. For a screenshot action, this property is always set to `screenshot`."
        }
      },
      "required": ["type"]
    },
    "Scroll": {
      "type": "object",
      "title": "Scroll",
      "description": "A scroll action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["scroll"],
          "description": "Specifies the event type. For a scroll action, this property is always set to `scroll`."
        },
        "x": {
          "type": "integer",
          "description": "The x-coordinate where the scroll occurred."
        },
        "y": {
          "type": "integer",
          "description": "The y-coordinate where the scroll occurred."
        },
        "scroll_x": {
          "type": "integer",
          "description": "The horizontal scroll distance."
        },
        "scroll_y": {
          "type": "integer",
          "description": "The vertical scroll distance."
        }
      },
      "required": ["type", "x", "y", "scroll_x", "scroll_y"]
    },
    "Type": {
      "type": "object",
      "title": "Type",
      "description": "An action to type in text.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["type"],
          "description": "Specifies the event type. For a type action, this property is always set to `type`."
        },
        "text": {
          "type": "string",
          "description": "The text to type."
        }
      },
      "required": ["type", "text"]
    },
    "Wait": {
      "type": "object",
      "title": "Wait",
      "description": "A wait action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["wait"],
          "description": "Specifies the event type. For a wait action, this property is always set to `wait`."
        }
      },
      "required": ["type"]
    },
    "ComputerScreenshotImage": {
      "type": "object",
      "title": "Computer screenshot image",
      "description": "A computer screenshot image used with the computer use tool.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["computer_screenshot"],
          "description": "Specifies the event type. For a computer screenshot, this property is always set to `computer_screenshot`.`."
        },
        "image_url": {
          "type": "string",
          "description": "The URL of the screenshot image."
        },
        "file_id": {
          "type": "string",
          "description": "The identifier of an uploaded file that contains the screenshot."
        }
      },
      "required": ["type"]
    },
    "ComputerCallSafetyCheckParam": {
      "type": "object",
      "title": "Computer call safety check",
      "description": "A pending safety check for the computer call.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The ID of the pending safety check."
        },
        "code": {
          "type": "string",
          "description": "The type of the pending safety check."
        },
        "message": {
          "type": "string",
          "description": "Details about the pending safety check."
        }
      },
      "required": ["id"]
    },
    "WebSearchActionSearch": {
      "type": "object",
      "title": "Search action",
      "description": "Action type \"search\" - Performs a web search query.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["search"],
          "description": "The action type."
        },
        "query": {
          "type": "string",
          "description": "The search query."
        },
        "sources": {
          "type": "array",
          "description": "The sources used in the search.",
          "items": {
            "type": "object",
            "properties": {
              "type": {
                "type": "string",
                "enum": ["url"],
                "description": "The type of source. Always `url`."
              },
              "url": {
                "type": "string",
                "description": "The URL of the source."
              }
            },
            "required": ["type", "url"]
          }
        }
      },
      "required": ["type", "query"]
    },
    "WebSearchActionOpenPage": {
      "type": "object",
      "title": "Open page action",
      "description": "Action type \"open_page\" - Opens a specific URL from search results.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["open_page"],
          "description": "The action type."
        },
        "url": {
          "type": "string",
          "description": "The URL opened by the model."
        }
      },
      "required": ["type", "url"]
    },
    "WebSearchActionFind": {
      "type": "object",
      "title": "Find action",
      "description": "Action type \"find\": Searches for a pattern within a loaded page.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["find"],
          "description": "The action type."
        },
        "url": {
          "type": "string",
          "description": "The URL of the page searched for the pattern."
        },
        "pattern": {
          "type": "string",
          "description": "The pattern or text to search for within the page."
        }
      },
      "required": ["type", "url", "pattern"]
    },
    "InputMessage": {
      "type": "object",
      "title": "Input message",
      "description": "A message input to the model with a role indicating instruction following hierarchy. Instructions given with the `developer` or `system` role take precedence over instructions given with the `user` role.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["message"],
          "description": "The type of the message input. Always set to `message`."
        },
        "role": {
          "type": "string",
          "enum": ["user", "system", "developer"],
          "description": "The role of the message input. One of `user`, `system`, or `developer`."
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of item. One of `in_progress`, `completed`, or `incomplete`. Populated when items are returned via API."
        },
        "content": {
          "type": "array",
          "description": "A list of one or many input items to the model, containing different content types.",
          "items": {
            "anyOf": [
              {
                "$ref": "#/$defs/InputTextContent"
              },
              {
                "$ref": "#/$defs/InputImageContent"
              },
              {
                "$ref": "#/$defs/InputFileContent"
              }
            ]
          }
        }
      },
      "required": ["role", "content"]
    },
    "OutputMessage": {
      "type": "object",
      "title": "Output message",
      "description": "An output message from the model.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique ID of the output message."
        },
        "type": {
          "type": "string",
          "enum": ["message"],
          "description": "The type of the output message. Always `message`."
        },
        "role": {
          "type": "string",
          "enum": ["assistant"],
          "description": "The role of the output message. Always `assistant`."
        },
        "content": {
          "type": "array",
          "description": "A list of one or many output items from the model, containing different content types.",
          "items": {
            "anyOf": [
              {
                "$ref": "#/$defs/OutputTextContent"
              },
              {
                "$ref": "#/$defs/RefusalContent"
              }
            ]
          }
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the message input. One of `in_progress`, `completed`, or `incomplete`. Populated when input items are returned via API."
        }
      },
      "required": ["id", "type", "role", "content", "status"]
    },
    "FileSearchToolCall": {
      "type": "object",
      "title": "File search tool call",
      "description": "The results of a file search tool call.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique ID of the file search tool call."
        },
        "type": {
          "type": "string",
          "enum": ["file_search_call"],
          "description": "The type of the file search tool call. Always `file_search_call`."
        },
        "status": {
          "type": "string",
          "enum": [
            "in_progress",
            "searching",
            "completed",
            "incomplete",
            "failed"
          ],
          "description": "The status of the file search tool call. One of `in_progress`, `searching`, `incomplete` or `failed`,"
        },
        "queries": {
          "type": "array",
          "description": "The queries used to search for files.",
          "items": {
            "type": "string"
          }
        },
        "results": {
          "type": "array",
          "description": "The results of the file search tool call.",
          "items": {
            "type": "object",
            "properties": {
              "file_id": {
                "type": "string",
                "description": "The unique ID of the file."
              },
              "text": {
                "type": "string",
                "description": "The text that was retrieved from the file."
              },
              "filename": {
                "type": "string",
                "description": "The name of the file."
              },
              "attributes": {
                "type": "object",
                "description": "Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters, booleans, or numbers."
              },
              "score": {
                "type": "number",
                "description": "The relevance score of the file - a value between 0 and 1."
              }
            }
          }
        }
      },
      "required": ["id", "type", "status", "queries"]
    },
    "ComputerToolCall": {
      "type": "object",
      "title": "Computer tool call",
      "description": "A tool call to a computer use tool.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["computer_call"],
          "description": "The type of the computer call. Always `computer_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the computer call."
        },
        "call_id": {
          "type": "string",
          "description": "An identifier used when responding to the tool call with output."
        },
        "action": {
          "anyOf": [
            {
              "$ref": "#/$defs/ClickParam"
            },
            {
              "$ref": "#/$defs/DoubleClickAction"
            },
            {
              "$ref": "#/$defs/Drag"
            },
            {
              "$ref": "#/$defs/KeyPressAction"
            },
            {
              "$ref": "#/$defs/Move"
            },
            {
              "$ref": "#/$defs/Screenshot"
            },
            {
              "$ref": "#/$defs/Scroll"
            },
            {
              "$ref": "#/$defs/Type"
            },
            {
              "$ref": "#/$defs/Wait"
            }
          ]
        },
        "pending_safety_checks": {
          "type": "array",
          "description": "The pending safety checks for the computer call.",
          "items": {
            "type": "object",
            "description": "A pending safety check for the computer call.",
            "properties": {
              "id": {
                "type": "string",
                "description": "The ID of the pending safety check."
              },
              "code": {
                "type": "string",
                "description": "The type of the pending safety check."
              },
              "message": {
                "type": "string",
                "description": "Details about the pending safety check."
              }
            },
            "required": ["id"]
          }
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the item. One of `in_progress`, `completed`, or `incomplete`. Populated when items are returned via API."
        }
      },
      "required": [
        "type",
        "id",
        "action",
        "call_id",
        "pending_safety_checks",
        "status"
      ]
    },
    "ComputerCallOutputItemParam": {
      "type": "object",
      "title": "Computer tool call output",
      "description": "The output of a computer tool call.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The ID of the computer tool call output."
        },
        "call_id": {
          "type": "string",
          "description": "The ID of the computer tool call that produced the output."
        },
        "type": {
          "type": "string",
          "enum": ["computer_call_output"],
          "description": "The type of the computer tool call output. Always `computer_call_output`."
        },
        "output": {
          "$ref": "#/$defs/ComputerScreenshotImage"
        },
        "acknowledged_safety_checks": {
          "type": "array",
          "description": "The safety checks reported by the API that have been acknowledged by the developer.",
          "items": {
            "$ref": "#/$defs/ComputerCallSafetyCheckParam"
          }
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the message input. One of `in_progress`, `completed`, or `incomplete`. Populated when input items are returned via API."
        }
      },
      "required": ["call_id", "type", "output"]
    },
    "WebSearchToolCall": {
      "type": "object",
      "title": "Web search tool call",
      "description": "The results of a web search tool call.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique ID of the web search tool call."
        },
        "type": {
          "type": "string",
          "enum": ["web_search_call"],
          "description": "The type of the web search tool call. Always `web_search_call`."
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "searching", "completed", "failed"],
          "description": "The status of the web search tool call."
        },
        "action": {
          "description": "The action performed by the web search tool call.",
          "anyOf": [
            {
              "$ref": "#/$defs/WebSearchActionSearch"
            },
            {
              "$ref": "#/$defs/WebSearchActionOpenPage"
            },
            {
              "$ref": "#/$defs/WebSearchActionFind"
            }
          ]
        }
      },
      "required": ["id", "type", "status", "action"]
    },
    "FunctionToolCall": {
      "type": "object",
      "title": "Function tool call",
      "description": "A tool call to run a function.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique ID of the function tool call."
        },
        "type": {
          "type": "string",
          "enum": ["function_call"],
          "description": "The type of the function tool call. Always `function_call`."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the function tool call generated by the model."
        },
        "name": {
          "type": "string",
          "description": "The name of the function to run."
        },
        "arguments": {
          "type": "string",
          "description": "A JSON string of the arguments to pass to the function."
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the item. One of `in_progress`, `completed`, or `incomplete`. Populated when items are returned via API."
        }
      },
      "required": ["type", "call_id", "name", "arguments"]
    },
    "FunctionCallOutputItemParam": {
      "type": "object",
      "title": "Function tool call output",
      "description": "The output of a function tool call.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique ID of the function tool call output. Populated when this item is returned via API."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the function tool call generated by the model."
        },
        "type": {
          "type": "string",
          "enum": ["function_call_output"],
          "description": "The type of the function tool call output. Always `function_call_output`."
        },
        "output": {
          "description": "Text, image, or file output of the function tool call.",
          "anyOf": [
            {
              "type": "string",
              "title": "TextOutput",
              "description": "A JSON string of the output of the function tool call."
            },
            {
              "type": "array",
              "title": "ArrayOutput",
              "description": "An array of output items from the function tool call.",
              "items": {
                "anyOf": [
                  {
                    "$ref": "#/$defs/InputTextContent"
                  },
                  {
                    "$ref": "#/$defs/InputImageContent"
                  },
                  {
                    "$ref": "#/$defs/InputFileContent"
                  }
                ]
              }
            }
          ]
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the item. One of `in_progress`, `completed`, or `incomplete`. Populated when items are returned via API."
        }
      },
      "required": ["call_id", "type", "output"]
    },
    "ReasoningItem": {
      "type": "object",
      "title": "Reasoning",
      "description": "A description of the chain of thought used by a reasoning model while generating a response.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["reasoning"],
          "description": "The type of the object. Always `reasoning`."
        },
        "id": {
          "type": "string",
          "description": "The unique identifier of the reasoning content."
        },
        "encrypted_content": {
          "type": "string",
          "description": "The encrypted content of the reasoning item - populated when a response is generated with `reasoning.encrypted_content` in the `include` parameter."
        },
        "summary": {
          "type": "array",
          "description": "Reasoning summary content.",
          "items": {
            "type": "object",
            "title": "Summary text",
            "description": "A summary text from the model.",
            "properties": {
              "type": {
                "type": "string",
                "enum": ["summary_text"],
                "description": "The type of the object. Always `summary_text`."
              },
              "text": {
                "type": "string",
                "description": "A summary of the reasoning output from the model so far."
              }
            },
            "required": ["type", "text"]
          }
        },
        "content": {
          "type": "array",
          "description": "Reasoning text content.",
          "items": {
            "type": "object",
            "title": "ReasoningTextContent",
            "description": "Reasoning text from the model.",
            "properties": {
              "type": {
                "type": "string",
                "enum": ["reasoning_text"],
                "description": "The type of the reasoning text. Always `reasoning_text`."
              },
              "text": {
                "type": "string",
                "description": "The reasoning text from the model."
              }
            },
            "required": ["type", "text"]
          }
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the item. One of `in_progress`, `completed`, or `incomplete`. Populated when items are returned via API."
        }
      },
      "required": ["id", "summary", "type"]
    },
    "CompactionSummaryItemParam": {
      "type": "object",
      "title": "Compaction item",
      "description": "A compaction item",
      "properties": {
        "id": {
          "type": "string",
          "description": "The ID of the compaction item."
        },
        "type": {
          "type": "string",
          "enum": ["compaction"],
          "description": "The type of the item. Always `compaction`."
        },
        "encrypted_content": {
          "type": "string"
        }
      },
      "required": ["type", "encrypted_content"]
    },
    "ImageGenToolCall": {
      "type": "object",
      "title": "Image generation call",
      "description": "An image generation request made by the model.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["image_generation_call"],
          "description": "The type of the image generation call. Always `image_generation_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the image generation call."
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "generating", "failed"],
          "description": "The status of the image generation call."
        },
        "result": {
          "type": "string",
          "description": "The generated image encoded in base64."
        }
      },
      "required": ["type", "id", "status", "result"]
    },
    "CodeInterpreterToolCall": {
      "type": "object",
      "title": "Code interpreter tool call",
      "description": "A tool call to run code.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["code_interpreter_call"],
          "description": "The type of the code interpreter tool call. Always `code_interpreter_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the code interpreter tool call."
        },
        "status": {
          "type": "string",
          "enum": [
            "in_progress",
            "completed",
            "incomplete",
            "interpreting",
            "failed"
          ],
          "description": "The status of the code interpreter tool call. Valid values are `in_progress`, `completed`, `incomplete`, `interpreting`, and `failed`."
        },
        "container_id": {
          "type": "string",
          "description": "The ID of the container used to run the code."
        },
        "code": {
          "type": "string",
          "description": "The code to run, or null if not available."
        },
        "outputs": {
          "type": "array",
          "description": "The outputs generated by the code interpreter, such as logs or images. Can be null if no outputs are available.",
          "items": {
            "anyOf": [
              {
                "type": "object",
                "title": "Code interpreter output logs",
                "description": "The logs output from the code interpreter.",
                "properties": {
                  "type": {
                    "type": "string",
                    "enum": ["logs"],
                    "description": "The type of the output. Always `logs`."
                  },
                  "logs": {
                    "type": "string",
                    "description": "The logs output from the code interpreter."
                  }
                },
                "required": ["type", "logs"]
              },
              {
                "type": "object",
                "title": "Code interpreter output image",
                "description": "The image output from the code interpreter.",
                "properties": {
                  "type": {
                    "type": "string",
                    "enum": ["image"],
                    "description": "The type of the output. Always `image`."
                  },
                  "url": {
                    "type": "string",
                    "description": "The URL of the image output from the code interpreter."
                  }
                },
                "required": ["type", "url"]
              }
            ]
          }
        }
      },
      "required": ["type", "id", "status", "container_id", "code", "outputs"]
    },
    "LocalShellToolCall": {
      "type": "object",
      "title": "Local shell call",
      "description": "A tool call to run a command on the local shell.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["local_shell_call"],
          "description": "The type of the local shell call. Always `local_shell_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the local shell call."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the local shell tool call generated by the model."
        },
        "action": {
          "type": "object",
          "title": "Local shell exec action",
          "description": "Execute a shell command on the server.",
          "properties": {
            "type": {
              "type": "string",
              "enum": ["exec"],
              "description": "The type of the local shell action. Always `exec`."
            },
            "command": {
              "type": "array",
              "description": "The command to run.",
              "items": {
                "type": "string"
              }
            },
            "timeout_ms": {
              "type": "integer",
              "description": "Optional timeout in milliseconds for the command."
            },
            "working_directory": {
              "type": "string",
              "description": "Optional working directory to run the command in."
            },
            "env": {
              "type": "object",
              "description": "Environment variables to set for the command."
            },
            "user": {
              "type": "string",
              "description": "Optional user to run the command as."
            }
          },
          "required": ["type", "command", "env"]
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the local shell call."
        }
      },
      "required": ["type", "id", "call_id", "action", "status"]
    },
    "LocalShellToolCallOutput": {
      "type": "object",
      "title": "Local shell call output",
      "description": "The output of a local shell tool call.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["local_shell_call_output"],
          "description": "The type of the local shell tool call output. Always `local_shell_call_output`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the local shell tool call generated by the model."
        },
        "output": {
          "type": "string",
          "description": "A JSON string of the output of the local shell tool call."
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the item. One of `in_progress`, `completed`, or `incomplete`."
        }
      },
      "required": ["id", "type", "call_id", "output"]
    },
    "FunctionShellCallItemParam": {
      "type": "object",
      "title": "Shell tool call",
      "description": "A tool representing a request to execute one or more shell commands.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique ID of the shell tool call. Populated when this item is returned via API."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the shell tool call generated by the model."
        },
        "type": {
          "type": "string",
          "enum": ["shell_call"],
          "description": "The type of the item. Always `shell_call`."
        },
        "action": {
          "type": "object",
          "title": "Shell action",
          "description": "Commands and limits describing how to run the shell tool call.",
          "properties": {
            "commands": {
              "type": "array",
              "description": "Ordered shell commands for the execution environment to run.",
              "items": {
                "type": "string"
              }
            },
            "timeout_ms": {
              "type": "integer",
              "description": "Maximum wall-clock time in milliseconds to allow the shell commands to run."
            },
            "max_output_length": {
              "type": "integer",
              "description": "Maximum number of UTF-8 characters to capture from combined stdout and stderr output."
            }
          },
          "required": ["commands"]
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the shell call. One of `in_progress`, `completed`, or `incomplete`."
        }
      },
      "required": ["call_id", "type", "action"]
    },
    "FunctionShellCallOutputItemParam": {
      "type": "object",
      "title": "Shell tool call output",
      "description": "The streamed output items emitted by a shell tool call.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique ID of the shell tool call output. Populated when this item is returned via API."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the shell tool call generated by the model."
        },
        "type": {
          "type": "string",
          "enum": ["shell_call_output"],
          "description": "The type of the item. Always `shell_call_output`."
        },
        "output": {
          "type": "array",
          "description": "Captured chunks of stdout and stderr output, along with their associated outcomes.",
          "items": {
            "type": "object",
            "title": "Shell output content",
            "description": "Captured stdout and stderr for a portion of a shell tool call output.",
            "properties": {
              "stdout": {
                "type": "string",
                "description": "Captured stdout output for the shell call."
              },
              "stderr": {
                "type": "string",
                "description": "Captured stderr output for the shell call."
              },
              "outcome": {
                "anyOf": [
                  {
                    "type": "object",
                    "title": "Shell call timeout outcome",
                    "description": "Indicates that the shell call exceeded its configured time limit.",
                    "properties": {
                      "type": {
                        "type": "string",
                        "enum": ["timeout"],
                        "description": "The outcome type. Always `timeout`."
                      }
                    },
                    "required": ["type"]
                  },
                  {
                    "type": "object",
                    "title": "Shell call exit outcome",
                    "description": "Indicates that the shell commands finished and returned an exit code.",
                    "properties": {
                      "type": {
                        "type": "string",
                        "enum": ["exit"],
                        "description": "The outcome type. Always `exit`."
                      },
                      "exit_code": {
                        "type": "integer",
                        "description": "The exit code returned by the shell process."
                      }
                    },
                    "required": ["type"]
                  }
                ]
              }
            },
            "required": ["stdout", "stderr", "outcome"]
          }
        },
        "max_output_length": {
          "type": "integer",
          "description": "The maximum number of UTF-8 characters captured for this shell call's combined output."
        }
      },
      "required": ["call_id", "type", "output"]
    },
    "ApplyPatchToolCallItemParam": {
      "type": "object",
      "title": "Apply patch tool call",
      "description": "A tool call representing a request to create, delete, or update files using diff patches.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["apply_patch_call"],
          "description": "The type of the item. Always `apply_patch_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the apply patch tool call. Populated when this item is returned via API."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the apply patch tool call generated by the model."
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed"],
          "description": "The status of the apply patch tool call. One of `in_progress` or `completed`."
        },
        "operation": {
          "description": "The specific create, delete, or update instruction for the apply_patch tool call.",
          "anyOf": [
            {
              "type": "object",
              "title": "Apply patch create file operation",
              "description": "Instruction for creating a new file via the apply_patch tool.",
              "properties": {
                "type": {
                  "type": "string",
                  "enum": ["create_file"],
                  "description": "The operation type. Always `create_file`."
                },
                "path": {
                  "type": "string",
                  "description": "Path of the file to create relative to the workspace root."
                },
                "diff": {
                  "type": "string",
                  "description": "Unified diff content to apply when creating the file."
                }
              },
              "required": ["type", "path", "diff"]
            },
            {
              "type": "object",
              "title": "Apply patch delete file operation",
              "description": "Instruction for deleting an existing file via the apply_patch tool.",
              "properties": {
                "type": {
                  "type": "string",
                  "enum": ["delete_file"],
                  "description": "The operation type. Always `delete_file`."
                },
                "path": {
                  "type": "string",
                  "description": "Path of the file to delete relative to the workspace root."
                }
              },
              "required": ["type", "path"]
            },
            {
              "type": "object",
              "title": "Apply patch update file operation",
              "description": "Instruction for updating an existing file via the apply_patch tool.",
              "properties": {
                "type": {
                  "type": "string",
                  "enum": ["update_file"],
                  "description": "The operation type. Always `update_file`."
                },
                "path": {
                  "type": "string",
                  "description": "Path of the file to update relative to the workspace root."
                },
                "diff": {
                  "type": "string",
                  "description": "Unified diff content to apply to the existing file."
                }
              },
              "required": ["type", "path", "diff"]
            }
          ]
        }
      },
      "required": ["type", "call_id", "status", "operation"]
    },
    "ApplyPatchToolCallOutputItemParam": {
      "type": "object",
      "title": "Apply patch tool call output",
      "description": "The streamed output emitted by an apply patch tool call.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["apply_patch_call_output"],
          "description": "The type of the item. Always `apply_patch_call_output`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the apply patch tool call output. Populated when this item is returned via API."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the apply patch tool call generated by the model."
        },
        "status": {
          "type": "string",
          "enum": ["completed", "failed"],
          "description": "The status of the apply patch tool call output. One of `completed` or `failed`."
        },
        "output": {
          "type": "string",
          "description": "Optional human-readable log text from the apply patch tool (e.g., patch results or errors)."
        }
      },
      "required": ["type", "call_id", "status"]
    },
    "MCPListTools": {
      "type": "object",
      "title": "MCP list tools",
      "description": "A list of tools available on an MCP server.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["mcp_list_tools"],
          "description": "The type of the item. Always `mcp_list_tools`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the list."
        },
        "server_label": {
          "type": "string",
          "description": "The label of the MCP server."
        },
        "tools": {
          "type": "array",
          "description": "The tools available on the server.",
          "items": {
            "type": "object",
            "title": "MCP list tools tool",
            "description": "A tool available on an MCP server.",
            "properties": {
              "name": {
                "type": "string",
                "description": "The name of the tool."
              },
              "description": {
                "type": "string",
                "description": "The description of the tool."
              },
              "input_schema": {
                "type": "object",
                "description": "The JSON schema describing the tool's input."
              },
              "annotations": {
                "type": "object",
                "description": "Additional annotations about the tool."
              }
            },
            "required": ["name", "input_schema"]
          }
        }
      },
      "required": ["type", "id", "server_label", "tools"]
    },
    "MCPApprovalRequest": {
      "type": "object",
      "title": "MCP approval request",
      "description": "A request for human approval of a tool invocation.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["mcp_approval_request"],
          "description": "The type of the item. Always `mcp_approval_request`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the approval request."
        },
        "server_label": {
          "type": "string",
          "description": "The label of the MCP server making the request."
        },
        "name": {
          "type": "string",
          "description": "The name of the tool to run."
        },
        "arguments": {
          "type": "string",
          "description": "A JSON string of arguments for the tool."
        }
      },
      "required": ["type", "id", "server_label", "name", "arguments"]
    },
    "MCPApprovalResponse": {
      "type": "object",
      "title": "MCP approval response",
      "description": "A response to an MCP approval request.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["mcp_approval_response"],
          "description": "The type of the item. Always `mcp_approval_response`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the approval response"
        },
        "approval_request_id": {
          "type": "boolean",
          "description": "The ID of the approval request being answered."
        },
        "approve": {
          "type": "boolean",
          "description": "Whether the request was approved."
        },
        "reason": {
          "type": "string",
          "description": "Optional reason for the decision."
        }
      },
      "required": ["type", "approve", "approval_request_id"]
    },
    "MCPToolCall": {
      "type": "object",
      "title": "MCP tool call",
      "description": "An invocation of a tool on an MCP server.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["mcp_call"],
          "description": "The type of the item. Always `mcp_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the tool call."
        },
        "server_label": {
          "type": "string",
          "description": "The label of the MCP server running the tool."
        },
        "name": {
          "type": "string",
          "description": "The name of the tool that was run."
        },
        "arguments": {
          "type": "string",
          "description": "A JSON string of the arguments passed to the tool."
        },
        "output": {
          "type": "string",
          "description": "The output from the tool call."
        },
        "error": {
          "type": "string",
          "description": "The error from the tool call, if any."
        },
        "status": {
          "type": "string",
          "enum": [
            "in_progress",
            "completed",
            "incomplete",
            "calling",
            "failed"
          ],
          "description": "The status of the tool call. One of `in_progress`, `completed`, `incomplete`, `calling`, or `failed`."
        },
        "approval_request_id": {
          "type": "string",
          "description": "Unique identifier for the MCP tool call approval request. Include this value in a subsequent `mcp_approval_response` input to approve or reject the corresponding tool call."
        }
      },
      "required": ["type", "id", "server_label", "name", "arguments"]
    },
    "CustomToolCallOutput": {
      "type": "object",
      "title": "Custom tool call output",
      "description": "The output of a custom tool call from your code, being sent back to the model.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["custom_tool_call_output"],
          "description": "The type of the custom tool call output. Always `custom_tool_call_output`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the custom tool call output in the OpenAI platform."
        },
        "call_id": {
          "type": "string",
          "description": "The call ID, used to map this custom tool call output to a custom tool call."
        },
        "output": {
          "description": "The output from the custom tool call generated by your code. Can be a string or an list of output content.",
          "anyOf": [
            {
              "type": "string",
              "title": "string output",
              "description": "A string of the output of the custom tool call."
            },
            {
              "type": "array",
              "title": "output content list",
              "description": "Text, image, or file output of the custom tool call.",
              "items": {
                "anyOf": [
                  {
                    "$ref": "#/$defs/InputTextContent"
                  },
                  {
                    "$ref": "#/$defs/InputImageContent"
                  },
                  {
                    "$ref": "#/$defs/InputFileContent"
                  }
                ]
              }
            }
          ]
        }
      },
      "required": ["type", "call_id", "output"]
    },
    "CustomToolCall": {
      "type": "object",
      "title": "Custom tool call",
      "description": "A call to a custom tool created by the model.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["custom_tool_call"],
          "description": "The type of the custom tool call. Always `custom_tool_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the custom tool call in the OpenAI platform."
        },
        "call_id": {
          "type": "string",
          "description": "An identifier used to map this custom tool call to a tool call output."
        },
        "name": {
          "type": "string",
          "description": "The name of the custom tool being called."
        },
        "input": {
          "type": "string",
          "description": "The input for the custom tool call generated by the model."
        }
      },
      "required": ["type", "call_id", "name", "input"]
    },
    "ItemReferenceParam": {
      "type": "object",
      "title": "Item reference",
      "description": "An internal identifier for an item to reference.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["item_reference"],
          "description": "The type of item to reference. Always `item_reference`."
        },
        "id": {
          "type": "string",
          "description": "The ID of the item to reference."
        }
      },
      "required": ["id"]
    },
    "ResponseFormatJsonSchemaSchema": {
      "type": "object",
      "description": "The schema for the response format, described as a JSON Schema object.",
      "title": "ResponseFormatJsonSchemaSchema"
    },
    "ResponseFormatText": {
      "type": "object",
      "description": "Default response format. Used to generate text responses.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["text"],
          "description": "The type of response format being defined. Always `text`."
        }
      },
      "required": ["type"],
      "title": "ResponseFormatText"
    },
    "TextResponseFormatJsonSchema": {
      "type": "object",
      "description": "JSON Schema response format. Used to generate structured JSON responses.",
      "properties": {
        "type": {
          "type": "string",
          "description": "The type of response format being defined. Always `json_schema`.",
          "enum": ["json_schema"]
        },
        "description": {
          "type": "string",
          "description": "A description of what the response format is for, used by the model to determine how to respond in the format."
        },
        "name": {
          "type": "string",
          "description": "The name of the response format. Must be a-z, A-Z, 0-9, or contain underscores and dashes, with a maximum length of 64."
        },
        "schema": {
          "$ref": "#/$defs/ResponseFormatJsonSchemaSchema"
        },
        "strict": {
          "type": "boolean",
          "default": false,
          "description": "Whether to enable strict schema adherence when generating the output. If set to true, the model will always follow the exact schema defined in the `schema` field. Only a subset of JSON Schema is supported when `strict` is `true`."
        }
      },
      "required": ["type", "name", "schema"],
      "title": "TextResponseFormatJsonSchema"
    },
    "ResponseFormatJsonObject": {
      "type": "object",
      "description": "JSON object response format. An older method of generating JSON responses. Using `json_schema` is recommended for models that support it. Note that the model will not generate JSON without a system or user message instructing it to do so.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["json_object"],
          "description": "The type of response format being defined. Always `json_object`."
        }
      },
      "required": ["type"],
      "title": "ResponseFormatJsonObject"
    },
    "TextResponseFormatConfiguration": {
      "title": "TextResponseFormatConfiguration",
      "description": "An object specifying the format that the model must output.",
      "anyOf": [
        {
          "$ref": "#/$defs/ResponseFormatText"
        },
        {
          "$ref": "#/$defs/TextResponseFormatJsonSchema"
        },
        {
          "$ref": "#/$defs/ResponseFormatJsonObject"
        }
      ]
    },
    "ToolChoiceOptions": {
      "type": "string",
      "enum": ["none", "auto", "required"],
      "title": "ToolChoiceOptions",
      "description": "Controls which (if any) tool is called by the model."
    },
    "ToolChoiceAllowed": {
      "type": "object",
      "title": "ToolChoiceAllowed",
      "description": "Constrains the tools available to the model to a pre-defined set.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["allowed_tools"],
          "description": "Allowed tool configuration type. Always `allowed_tools`."
        },
        "mode": {
          "type": "string",
          "enum": ["auto", "required"],
          "description": "Constrains the tools available to the model to a pre-defined set."
        },
        "tools": {
          "type": "array",
          "description": "A list of tool definitions that the model should be allowed to call.",
          "items": {
            "type": "object",
            "description": "A tool definition that the model should be allowed to call."
          }
        },
        "required": ["type", "mode", "tools"]
      }
    },
    "ToolChoiceTypes": {
      "type": "object",
      "title": "ToolChoiceTypes",
      "description": "Indicates that the model should use a built-in tool to generate a response.",
      "properties": {
        "type": {
          "type": "string",
          "enum": [
            "file_search",
            "web_search_preview",
            "computer_use_preview",
            "web_search_preview_2025_03_11",
            "image_generation",
            "code_interpreter"
          ],
          "description": "Types tool configuration type. Always `types`."
        }
      },
      "required": ["type"]
    },
    "ToolChoiceFunction": {
      "type": "object",
      "title": "ToolChoiceFunction",
      "description": "Use this option to force the model to call a specific function.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["function"],
          "description": "For function calling, the type is always `function`."
        },
        "name": {
          "type": "string",
          "description": "The name of the function to call."
        }
      },
      "required": ["type", "name"]
    },
    "ToolChoiceMCP": {
      "type": "object",
      "title": "ToolChoiceMCP",
      "description": "Use this option to force the model to call a specific tool on a remote MCP server.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["mcp"],
          "description": "For MCP tools, the type is always `mcp`."
        },
        "server_label": {
          "type": "string",
          "description": "The label of the MCP server to use."
        },
        "name": {
          "type": "string",
          "description": "The name of the tool to call on the server."
        }
      },
      "required": ["type", "server_label"]
    },
    "ToolChoiceCustom": {
      "type": "object",
      "title": "ToolChoiceCustom",
      "description": "Use this option to force the model to call a specific custom tool.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["custom"],
          "description": "For custom tool calling, the type is always `custom`."
        },
        "name": {
          "type": "string",
          "description": "The name of the custom tool to call."
        }
      },
      "required": ["type", "name"]
    },
    "SpecificApplyPatchParam": {
      "type": "object",
      "title": "SpecificApplyPatchParam",
      "description": "Forces the model to call the apply_patch tool when executing a tool call.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["apply_patch"],
          "description": "The tool to call. Always `apply_patch`."
        }
      },
      "required": ["type"]
    },
    "SpecificFunctionShellParam": {
      "type": "object",
      "title": "SpecificFunctionShellParam",
      "description": "Forces the model to call the shell tool when a tool call is required.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["shell"],
          "description": "The tool to call. Always `shell`."
        }
      },
      "required": ["type"]
    },
    "ComparisonFilter": {
      "type": "object",
      "title": "ComparisonFilter",
      "description": "A filter used to compare a specified attribute key to a given value using a defined comparison operation.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["eq", "ne", "gt", "gte", "lt", "lte"],
          "description": "Specifies the comparison operator: `eq`, `ne`, `gt`, `gte`, `lt`, `lte`, `in`, `nin`."
        },
        "key": {
          "type": "string",
          "description": "The key to compare against the value."
        },
        "value": {
          "description": "The value to compare against the attribute key; supports string, number, or boolean types.",
          "anyOf": [
            {
              "type": "string"
            },
            {
              "type": "number"
            },
            {
              "type": "boolean"
            },
            {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "string"
                  },
                  {
                    "type": "number"
                  }
                ]
              }
            }
          ]
        }
      },
      "required": ["type", "key", "value"]
    },
    "CompoundFilter": {
      "type": "object",
      "title": "CompoundFilter",
      "description": "Combine multiple filters using `and` or `or`.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["and", "or"],
          "description": "Type of operation: `and` or `or`."
        },
        "filters": {
          "type": "array",
          "description": "Array of filters to combine. Items can be `ComparisonFilter` or `CompoundFilter`.",
          "items": {
            "anyOf": [
              {
                "$ref": "#/$defs/ComparisonFilter"
              }
            ]
          }
        }
      },
      "required": ["type", "filters"]
    },
    "FunctionTool": {
      "type": "object",
      "title": "FunctionTool",
      "description": "Defines a function in your own code the model can choose to call.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["function"],
          "description": "The type of the function tool. Always `function`."
        },
        "name": {
          "type": "string",
          "description": "The name of the function to call."
        },
        "description": {
          "type": "string",
          "description": "A description of the function. Used by the model to determine whether or not to call the function."
        },
        "parameters": {
          "type": "object",
          "description": "A JSON schema object describing the parameters of the function."
        },
        "strict": {
          "type": "boolean",
          "description": "Whether to enforce strict parameter validation. Default `true`."
        }
      },
      "required": ["type", "name", "strict", "parameters"]
    },
    "FileSearchTool": {
      "type": "object",
      "title": "FileSearchTool",
      "description": "A tool that searches for relevant content from uploaded files.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["file_search"],
          "description": "The type of the file search tool. Always `file_search`."
        },
        "vector_store_ids": {
          "type": "array",
          "items": {
            "type": "string"
          },
          "description": "The IDs of the vector stores to search."
        },
        "max_num_results": {
          "type": "integer",
          "description": "The maximum number of results to return. This number should be between 1 and 50 inclusive."
        },
        "ranking_options": {
          "type": "object",
          "description": "Ranking options for search.",
          "properties": {
            "ranker": {
              "type": "string",
              "enum": ["auto", "default-2024-11-15"],
              "description": "The ranker to use for the file search."
            },
            "score_threshold": {
              "type": "number",
              "description": "The score threshold for the file search, a number between 0 and 1. Numbers closer to 1 will attempt to return only the most relevant results, but may return fewer results."
            },
            "hybrid_search": {
              "type": "object",
              "description": "Weights that control how reciprocal rank fusion balances semantic embedding matches versus sparse keyword matches when hybrid search is enabled.",
              "properties": {
                "embedding_weight": {
                  "type": "number",
                  "description": "The weight of the embedding in the reciprocal ranking fusion."
                },
                "text_weight": {
                  "type": "number",
                  "description": "The weight of the text in the reciprocal ranking fusion."
                }
              },
              "required": ["embedding_weight", "text_weight"]
            }
          }
        },
        "filters": {
          "description": "A filter to apply.",
          "anyOf": [
            {
              "$ref": "#/$defs/ComparisonFilter"
            },
            {
              "$ref": "#/$defs/CompoundFilter"
            }
          ]
        }
      },
      "required": ["type", "vector_store_ids"]
    },
    "ComputerUsePreviewTool": {
      "type": "object",
      "title": "ComputerUsePreviewTool",
      "description": "A tool that controls a virtual computer.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["computer_use_preview"],
          "description": "The type of the computer use tool. Always `computer_use_preview`."
        },
        "environment": {
          "type": "string",
          "description": "The type of computer environment to control.",
          "enum": ["windows", "mac", "linux", "ubuntu", "browser"]
        },
        "display_width": {
          "type": "integer",
          "description": "The width of the computer display."
        },
        "display_height": {
          "type": "integer",
          "description": "The height of the computer display."
        }
      },
      "required": ["type", "environment", "display_width", "display_height"]
    },
    "WebSearchTool": {
      "type": "object",
      "title": "WebSearchTool",
      "description": "Search the Internet for sources related to the prompt.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["web_search", "web_search_2025_08_26"],
          "description": "The type of the web search tool. One of `web_search` or `web_search_2025_08_26`."
        },
        "filters": {
          "type": "object",
          "description": "Filters for the search.",
          "properties": {
            "allowed_domains": {
              "type": "array",
              "description": "Allowed domains for the search. If not provided, all domains are allowed. Subdomains of the provided domains are allowed as well.",
              "items": {
                "type": "string"
              }
            }
          }
        },
        "user_location": {
          "type": "object",
          "description": "The approximate location of the user.",
          "properties": {
            "type": {
              "type": "string",
              "enum": ["approximate"],
              "description": "The type of location approximation. Always `approximate`."
            },
            "country": {
              "type": "string",
              "description": "The two-letter [ISO country code](https://en.wikipedia.org/wiki/ISO_3166-1) of the user, e.g. `US`."
            },
            "region": {
              "type": "string",
              "description": "Free text input for the region of the user, e.g. `California`."
            },
            "city": {
              "type": "string",
              "description": "Free text input for the city of the user, e.g. `San Francisco`."
            },
            "timezone": {
              "type": "string",
              "description": "The [IANA timezone](https://timeapi.io/documentation/iana-timezones) of the user, e.g. `America/Los_Angeles`."
            }
          }
        },
        "search_context_size": {
          "type": "string",
          "enum": ["low", "medium", "high"],
          "description": "High level guidance for the amount of context window space to use for the search. One of `low`, `medium`, or `high`. `medium` is the default."
        }
      },
      "required": ["type"]
    },
    "MCPToolFilter": {
      "type": "object",
      "title": "MCP tool filter",
      "description": "A filter object to specify which tools are allowed.",
      "properties": {
        "tool_names": {
          "type": "array",
          "title": "MCP allowed tools",
          "description": "List of allowed tool names.",
          "items": {
            "type": "string"
          }
        },
        "read_only": {
          "type": "boolean",
          "description": "Indicates whether or not a tool modifies data or is read-only."
        }
      }
    },
    "MCPTool": {
      "type": "object",
      "title": "MCPTool",
      "description": "Give the model access to additional tools via remote Model Context Protocol (MCP) servers.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["mcp"],
          "description": "The type of the MCP tool. Always `mcp`."
        },
        "server_label": {
          "type": "string",
          "description": "A label for this MCP server, used to identify it in tool calls."
        },
        "server_url": {
          "type": "string",
          "description": "The URL for the MCP server. One of `server_url` or `connector_id` must be provided."
        },
        "connector_id": {
          "type": "string",
          "description": "Identifier for service connectors, like those available in ChatGPT. One of `server_url` or `connector_id` must be provided.",
          "enum": [
            "connector_dropbox",
            "connector_gmail",
            "connector_googlecalendar",
            "connector_googledrive",
            "connector_microsoftteams",
            "connector_outlookcalendar",
            "connector_outlookemail",
            "connector_sharepoint"
          ]
        },
        "authorization": {
          "type": "string",
          "description": "An OAuth access token that can be used with a remote MCP server, either with a custom MCP server URL or a service connector. Your application must handle the OAuth authorization flow and provide the token here."
        },
        "server_description": {
          "type": "string",
          "description": "Optional description of the MCP server, used to provide more context."
        },
        "headers": {
          "type": "object",
          "description": "Optional HTTP headers to send to the MCP server. Use for authentication or other purposes.",
          "additionalProperties": {
            "type": "string"
          }
        },
        "allowed_tools": {
          "description": "List of allowed tool names or a filter object.",
          "anyOf": [
            {
              "type": "array",
              "title": "AllowedToolNames",
              "description": "A string array of allowed tool names",
              "items": {
                "type": "string"
              }
            },
            {
              "type": "object",
              "title": "MCP tool filter",
              "description": "A filter object to specify which tools are allowed.",
              "properties": {
                "tool_names": {
                  "type": "array",
                  "description": "List of allowed tool names.",
                  "items": {
                    "type": "string"
                  }
                },
                "read_only": {
                  "type": "boolean",
                  "description": "Indicates whether or not a tool modifies data or is read-only."
                }
              }
            }
          ]
        },
        "require_approval": {
          "description": "Specify which of the MCP server's tools require approval.",
          "anyOf": [
            {
              "type": "object",
              "title": "MCP tool approval filter",
              "description": "Specify which of the MCP server's tools require approval. Can be `always`, `never`, or a filter object associated with tools that require approval.",
              "properties": {
                "always": {
                  "$ref": "#/$defs/MCPToolFilter"
                },
                "never": {
                  "$ref": "#/$defs/MCPToolFilter"
                }
              }
            },
            {
              "type": "string",
              "title": "MCP tool approval setting",
              "description": "Specify a single approval policy for all tools. One of `always` or `never`. When set to `always`, all tools will require approval. When set to `never`, all tools will not require approval.",
              "enum": ["always", "never"]
            }
          ]
        }
      },
      "required": ["type", "server_label"]
    },
    "CodeInterpreterTool": {
      "type": "object",
      "title": "CodeInterpreterTool",
      "description": "A tool that runs Python code to help generate a response to a prompt.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["code_interpreter"],
          "description": "The type of the code interpreter tool. Always `code_interpreter`."
        },
        "container": {
          "description": "The code interpreter container. Can be a container ID or an object that specifies uploaded file IDs to make available to your code, along with an optional `memory_limit` setting.",
          "anyOf": [
            {
              "type": "string",
              "title": "Container ID",
              "description": "The container ID."
            },
            {
              "type": "object",
              "title": "CodeInterpreterToolAuto",
              "description": "Configuration for a code interpreter container. Optionally specify the IDs of the files to run the code on.",
              "properties": {
                "type": {
                  "type": "string",
                  "enum": ["auto"],
                  "description": "Always `auto`."
                },
                "file_ids": {
                  "type": "array",
                  "maxItems": 50,
                  "description": "An optional list of uploaded files to make available to your code.",
                  "items": {
                    "type": "string"
                  }
                },
                "memory_limit": {
                  "type": "string",
                  "enum": ["1g", "4g", "16g", "64g"]
                }
              },
              "required": ["type"]
            }
          ]
        }
      },
      "required": ["type", "container"]
    },
    "ImageGenTool": {
      "type": "object",
      "title": "ImageGenTool",
      "description": "A tool that generates images using the GPT image models.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["image_generation"],
          "description": "The type of the image generation tool. Always `image_generation`."
        },
        "model": {
          "type": "string",
          "description": "The image generation model to use."
        },
        "quality": {
          "type": "string",
          "enum": ["low", "medium", "high", "auto"],
          "description": "The quality of the generated image. One of `low`, `medium`, `high`, or `auto`."
        },
        "size": {
          "type": "string",
          "enum": ["1024x1024", "1024x1536", "1536x1024", "auto"],
          "description": "The size of the generated image. One of `1024x1024`, `1024x1536`, `1536x1024`, or `auto`."
        },
        "output_format": {
          "type": "string",
          "enum": ["png", "webp", "jpeg"],
          "description": "The output format of the generated image. One of `png`, `webp`, or `jpeg`."
        },
        "output_compression": {
          "type": "integer",
          "minimum": 0,
          "maximum": 100,
          "description": "Compression level for the output image."
        },
        "moderation": {
          "type": "string",
          "enum": ["auto", "low"],
          "description": "Moderation level for the generated image."
        },
        "background": {
          "type": "string",
          "enum": ["transparent", "opaque", "auto"],
          "description": "Background type for the generated image. One of `transparent`, `opaque`, or `auto`."
        },
        "input_fidelity": {
          "type": "string",
          "enum": ["high", "low"],
          "description": "Control how much effort the model will exert to match the style and features, especially facial features, of input images."
        },
        "input_image_mask": {
          "type": "object",
          "description": "Optional mask for inpainting. Contains `image_url` (string, optional) and `file_id` (string, optional).",
          "properties": {
            "image_url": {
              "type": "string",
              "description": "Base64-encoded mask image."
            },
            "file_id": {
              "type": "string",
              "description": "File ID for the mask image."
            }
          }
        },
        "partial_images": {
          "type": "integer",
          "minimum": 0,
          "maximum": 3,
          "description": "Number of partial images to generate in streaming mode, from 0 (default value) to 3."
        }
      },
      "required": ["type"]
    },
    "LocalShellToolParam": {
      "type": "object",
      "title": "LocalShellToolParam",
      "description": "A tool that allows the model to execute shell commands in a local environment.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["local_shell"],
          "description": "The type of the local shell tool. Always `local_shell`."
        }
      },
      "required": ["type"]
    },
    "FunctionShellToolParam": {
      "type": "object",
      "title": "FunctionShellToolParam",
      "description": "A tool that allows the model to execute shell commands.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["shell"],
          "description": "The type of the shell tool. Always `shell`."
        }
      },
      "required": ["type"]
    },
    "CustomToolParam": {
      "type": "object",
      "title": "CustomToolParam",
      "description": "A custom tool that processes input using a specified format.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["custom"],
          "description": "The type of the custom tool. Always `custom`."
        },
        "name": {
          "type": "string",
          "description": "The name of the custom tool, used to identify it in tool calls."
        },
        "description": {
          "type": "string",
          "description": "Optional description of the custom tool, used to provide more context."
        },
        "format": {
          "description": "The input format for the custom tool. Default is unconstrained text.",
          "anyOf": [
            {
              "type": "string",
              "enum": ["text"],
              "title": "Text format",
              "description": "Unconstrained text format. Always `text`."
            },
            {
              "type": "object",
              "title": "Grammar format",
              "description": "A grammar defined by the user.",
              "properties": {
                "type": {
                  "type": "string",
                  "enum": ["grammar"],
                  "description": "Grammar format. Always `grammar`."
                },
                "syntax": {
                  "type": "string",
                  "enum": ["lark", "regex"],
                  "description": "The syntax of the grammar definition. One of `lark` or `regex`."
                },
                "definition": {
                  "type": "string",
                  "description": "The grammar definition."
                }
              },
              "required": ["type", "syntax", "definition"]
            }
          ]
        }
      },
      "required": ["type", "name"]
    },
    "WebSearchPreviewTool": {
      "type": "object",
      "title": "WebSearchPreviewTool",
      "description": "This tool searches the web for relevant results to use in a response.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["web_search_preview", "web_search_preview_2025_03_11"],
          "description": "The type of the web search tool. One of `web_search_preview` or `web_search_preview_2025_03_11`."
        },
        "user_location": {
          "type": "object",
          "properties": {
            "type": {
              "type": "string",
              "enum": ["approximate"],
              "description": "The type of location approximation. Always `approximate`."
            },
            "country": {
              "type": "string",
              "description": "The two-letter [ISO country code](https://en.wikipedia.org/wiki/ISO_3166-1) of the user, e.g. `US`."
            },
            "region": {
              "type": "string",
              "description": "Free text input for the region of the user, e.g. `California`."
            },
            "city": {
              "type": "string",
              "description": "Free text input for the city of the user, e.g. `San Francisco`."
            },
            "timezone": {
              "type": "string",
              "description": "The [IANA timezone](https://timeapi.io/documentation/iana-timezones) of the user, e.g. `America/Los_Angeles`."
            }
          },
          "required": ["type"]
        },
        "search_context_size": {
          "type": "string",
          "enum": ["low", "medium", "high"],
          "description": "High level guidance for the amount of context window space to use for the search. One of `low`, `medium`, or `high`. `medium` is the default."
        }
      },
      "required": ["type"]
    },
    "ApplyPatchToolParam": {
      "type": "object",
      "title": "ApplyPatchToolParam",
      "description": "Allows the assistant to create, delete, or update files using unified diffs.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["apply_patch"],
          "description": "The type of the tool. Always `apply_patch`."
        }
      },
      "required": ["type"]
    }
  },
  "properties": {
    "input": {
      "description": "Text, image, or file inputs to the model, used to generate a response.",
      "anyOf": [
        {
          "type": "string",
          "title": "Text input",
          "description": "A text input to the model, equivalent to a text input with the `user` role."
        },
        {
          "type": "array",
          "title": "Input item list",
          "description": "A list of one or many input items to the model, containing different content types.",
          "items": {
            "anyOf": [
              {
                "$ref": "#/$defs/EasyInputMessage"
              },
              {
                "$ref": "#/$defs/InputMessage"
              },
              {
                "$ref": "#/$defs/OutputMessage"
              },
              {
                "$ref": "#/$defs/FileSearchToolCall"
              },
              {
                "$ref": "#/$defs/ComputerToolCall"
              },
              {
                "$ref": "#/$defs/ComputerCallOutputItemParam"
              },
              {
                "$ref": "#/$defs/WebSearchToolCall"
              },
              {
                "$ref": "#/$defs/FunctionToolCall"
              },
              {
                "$ref": "#/$defs/FunctionCallOutputItemParam"
              },
              {
                "$ref": "#/$defs/ReasoningItem"
              },
              {
                "$ref": "#/$defs/CompactionSummaryItemParam"
              },
              {
                "$ref": "#/$defs/ImageGenToolCall"
              },
              {
                "$ref": "#/$defs/CodeInterpreterToolCall"
              },
              {
                "$ref": "#/$defs/LocalShellToolCall"
              },
              {
                "$ref": "#/$defs/LocalShellToolCallOutput"
              },
              {
                "$ref": "#/$defs/FunctionShellCallItemParam"
              },
              {
                "$ref": "#/$defs/FunctionShellCallOutputItemParam"
              },
              {
                "$ref": "#/$defs/ApplyPatchToolCallItemParam"
              },
              {
                "$ref": "#/$defs/ApplyPatchToolCallOutputItemParam"
              },
              {
                "$ref": "#/$defs/MCPListTools"
              },
              {
                "$ref": "#/$defs/MCPApprovalRequest"
              },
              {
                "$ref": "#/$defs/MCPApprovalResponse"
              },
              {
                "$ref": "#/$defs/MCPToolCall"
              },
              {
                "$ref": "#/$defs/CustomToolCallOutput"
              },
              {
                "$ref": "#/$defs/CustomToolCall"
              },
              {
                "$ref": "#/$defs/ItemReferenceParam"
              }
            ]
          }
        }
      ]
    },
    "model": {
      "description": "ID of the model to use.",
      "type": "string"
    },
    "background": {
      "type": "boolean",
      "default": false,
      "description": "Whether to run the model response in the background."
    },
    "include": {
      "type": "array",
      "items": {
        "type": "string",
        "enum": [
          "code_interpreter_call.outputs",
          "computer_call_output.output.image_url",
          "file_search_call.results",
          "message.input_image.image_url",
          "message.output_text.logprobs",
          "reasoning.encrypted_content"
        ]
      },
      "description": "Specify additional output data to include in the model response."
    },
    "instructions": {
      "type": "string",
      "description": "A system (or developer) message inserted into the model's context."
    },
    "max_output_tokens": {
      "type": "integer",
      "description": "An upper bound for the number of tokens that can be generated for a response, including visible output tokens and reasoning tokens."
    },
    "max_tool_calls": {
      "type": "integer",
      "description": "The maximum number of total calls to built-in tools that can be processed in a response. This maximum number applies across all built-in tool calls, not per individual tool. Any further attempts to call a tool by the model will be ignored."
    },
    "metadata": {
      "type": "object",
      "description": "Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters."
    },
    "parallel_tool_calls": {
      "type": "boolean",
      "default": true,
      "description": "Whether to allow the model to run tool calls in parallel."
    },
    "previous_response_id": {
      "type": "string",
      "description": "The unique ID of the previous response to the model. Use this to create multi-turn conversations."
    },
    "prompt": {
      "type": "object",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique identifier of the prompt template to use."
        },
        "variables": {
          "type": "object",
          "description": "Optional map of values to substitute in for variables in your prompt. The substitution values can either be strings, or other Response input types like images or files."
        },
        "version": {
          "type": "string",
          "description": "Optional version of the prompt template."
        }
      },
      "required": ["id"],
      "description": "Reference to a prompt template and its variables."
    },
    "reasoning": {
      "type": "object",
      "properties": {
        "effort": {
          "type": "string",
          "enum": ["low", "medium", "high"],
          "description": "Constrains effort on reasoning for reasoning models."
        }
      },
      "description": "Configuration options for reasoning models."
    },
    "service_tier": {
      "type": "string",
      "enum": ["auto", "default", "flex", "scale", "priority"],
      "default": "auto",
      "description": "Specifies the processing type used for serving the request."
    },
    "store": {
      "type": "boolean",
      "default": true,
      "description": "Whether to store the generated model response for later retrieval via API."
    },
    "stream": {
      "type": "boolean",
      "default": false,
      "description": "If set to true, the model response data will be streamed to the client as it is generated using server-sent events."
    },
    "temperature": {
      "type": "number",
      "description": "What sampling temperature to use, between 0 and 2. Higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic. We generally recommend altering this or top_p but not both."
    },
    "text": {
      "type": "object",
      "properties": {
        "format": {
          "$ref": "#/$defs/TextResponseFormatConfiguration"
        },
        "verbosity": {
          "type": "string",
          "enum": ["low", "medium", "high"],
          "description": "Constrains the verbosity of the model's response. Lower values will result in more concise responses, while higher values will result in more verbose responses."
        }
      },
      "description": "Configuration options for a text response from the model. Can be plain text or structured JSON data."
    },
    "tool_choice": {
      "anyOf": [
        {
          "$ref": "#/$defs/ToolChoiceOptions"
        },
        {
          "$ref": "#/$defs/ToolChoiceAllowed"
        },
        {
          "$ref": "#/$defs/ToolChoiceTypes"
        },
        {
          "$ref": "#/$defs/ToolChoiceFunction"
        },
        {
          "$ref": "#/$defs/ToolChoiceMCP"
        },
        {
          "$ref": "#/$defs/ToolChoiceCustom"
        },
        {
          "$ref": "#/$defs/SpecificApplyPatchParam"
        },
        {
          "$ref": "#/$defs/SpecificFunctionShellParam"
        }
      ],
      "description": "How the model should select which tool (or tools) to use when generating a response. See the tools parameter to see how to specify which tools the model can call."
    },
    "tools": {
      "type": "array",
      "items": {
        "anyOf": [
          {
            "$ref": "#/$defs/FunctionTool"
          },
          {
            "$ref": "#/$defs/FileSearchTool"
          },
          {
            "$ref": "#/$defs/ComputerUsePreviewTool"
          },
          {
            "$ref": "#/$defs/WebSearchTool"
          },
          {
            "$ref": "#/$defs/MCPTool"
          },
          {
            "$ref": "#/$defs/CodeInterpreterTool"
          },
          {
            "$ref": "#/$defs/ImageGenTool"
          },
          {
            "$ref": "#/$defs/LocalShellToolParam"
          },
          {
            "$ref": "#/$defs/FunctionShellToolParam"
          },
          {
            "$ref": "#/$defs/CustomToolParam"
          },
          {
            "$ref": "#/$defs/WebSearchPreviewTool"
          },
          {
            "$ref": "#/$defs/ApplyPatchToolParam"
          }
        ]
      },
      "description": "An array of tools the model may call while generating a response. You can specify which tool to use by setting the tool_choice parameter."
    },
    "top_logprobs": {
      "type": "integer",
      "minimum": 0,
      "maximum": 20,
      "description": "An integer between 0 and 20 specifying the number of most likely tokens to return at each token position, each with an associated log probability."
    },
    "top_p": {
      "type": "number",
      "minimum": 0,
      "maximum": 1,
      "description": "An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So 0.1 means only the tokens comprising the top 10% probability mass are considered."
    },
    "truncation": {
      "type": "string",
      "enum": ["auto", "disabled"],
      "default": "disabled",
      "description": "The truncation strategy to use for the model response."
    },
    "user": {
      "type": "string",
      "description": "This field is being replaced by safety_identifier and prompt_cache_key. Use prompt_cache_key instead to maintain caching optimizations. A stable identifier for your end-users. Used to boost cache hit rates by better bucketing similar requests and to help OpenAI detect and prevent abuse. "
    },
    "request_id": {
      "type": "string",
      "description": "The request_id related to this request. If the caller does not set it, a random_uuid will be generated. This id is used through out the inference process and return in response."
    },
    "mm_processor_kwargs": {
      "type": "object",
      "description": "Additional kwargs to pass to the HF processor."
    },
    "priority": {
      "type": "integer",
      "default": 0,
      "description": "The priority of the request (lower means earlier handling; default: 0). Any priority other than 0 will raise an error if the served model does not use priority scheduling."
    },
    "cache_salt": {
      "type": "string",
      "description": "A salt value to add to the prompt cache key. This can be used to create a unique cache key for a request."
    }
  },
  "required": ["model", "input"]
}
```

#### Response Object

```json
{
  "title": "CreateResponseResponse",
  "type": "object",
  "$defs": {
    "ResponseFormatJsonSchemaSchema": {
      "type": "object",
      "description": "The schema for the response format, described as a JSON Schema object.",
      "title": "ResponseFormatJsonSchemaSchema"
    },
    "ResponseFormatText": {
      "type": "object",
      "description": "Default response format. Used to generate text responses.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["text"],
          "description": "The type of response format being defined. Always `text`."
        }
      },
      "required": ["type"],
      "title": "ResponseFormatText"
    },
    "TextResponseFormatJsonSchema": {
      "type": "object",
      "description": "JSON Schema response format. Used to generate structured JSON responses.",
      "properties": {
        "type": {
          "type": "string",
          "description": "The type of response format being defined. Always `json_schema`.",
          "enum": ["json_schema"]
        },
        "description": {
          "type": "string",
          "description": "A description of what the response format is for, used by the model to determine how to respond in the format."
        },
        "name": {
          "type": "string",
          "description": "The name of the response format. Must be a-z, A-Z, 0-9, or contain underscores and dashes, with a maximum length of 64."
        },
        "schema": {
          "$ref": "#/$defs/ResponseFormatJsonSchemaSchema"
        },
        "strict": {
          "type": "boolean",
          "default": false,
          "description": "Whether to enable strict schema adherence when generating the output. If set to true, the model will always follow the exact schema defined in the `schema` field. Only a subset of JSON Schema is supported when `strict` is `true`."
        }
      },
      "required": ["type", "name", "schema"],
      "title": "TextResponseFormatJsonSchema"
    },
    "ResponseFormatJsonObject": {
      "type": "object",
      "description": "JSON object response format. An older method of generating JSON responses. Using `json_schema` is recommended for models that support it. Note that the model will not generate JSON without a system or user message instructing it to do so.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["json_object"],
          "description": "The type of response format being defined. Always `json_object`."
        }
      },
      "required": ["type"],
      "title": "ResponseFormatJsonObject"
    },
    "ComparisonFilter": {
      "type": "object",
      "title": "ComparisonFilter",
      "description": "A filter used to compare a specified attribute key to a given value using a defined comparison operation.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["eq", "ne", "gt", "gte", "lt", "lte"],
          "description": "Specifies the comparison operator: `eq`, `ne`, `gt`, `gte`, `lt`, `lte`, `in`, `nin`."
        },
        "key": {
          "type": "string",
          "description": "The key to compare against the value."
        },
        "value": {
          "description": "The value to compare against the attribute key; supports string, number, or boolean types.",
          "anyOf": [
            {
              "type": "string"
            },
            {
              "type": "number"
            },
            {
              "type": "boolean"
            },
            {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "string"
                  },
                  {
                    "type": "number"
                  }
                ]
              }
            }
          ]
        }
      },
      "required": ["type", "key", "value"]
    },
    "CompoundFilter": {
      "type": "object",
      "title": "CompoundFilter",
      "description": "Combine multiple filters using `and` or `or`.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["and", "or"],
          "description": "Type of operation: `and` or `or`."
        },
        "filters": {
          "type": "array",
          "description": "Array of filters to combine. Items can be `ComparisonFilter` or `CompoundFilter`.",
          "items": {
            "anyOf": [
              {
                "$ref": "#/$defs/ComparisonFilter"
              }
            ]
          }
        }
      },
      "required": ["type", "filters"]
    },
    "ClickParam": {
      "type": "object",
      "title": "Click",
      "description": "A click action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["click"],
          "description": "Specifies the event type. For a click action, this property is always `click`."
        },
        "button": {
          "type": "string",
          "enum": ["left", "right", "wheel", "back", "forward"],
          "description": "Indicates which mouse button was pressed during the click. One of `left`, `right`, `wheel`, `back`, or `forward`."
        },
        "x": {
          "type": "integer",
          "description": "The x-coordinate where the click occurred."
        },
        "y": {
          "type": "integer",
          "description": "The y-coordinate where the click occurred."
        }
      },
      "required": ["type", "button", "x", "y"]
    },
    "DoubleClickAction": {
      "type": "object",
      "title": "DoubleClick",
      "description": "A double click action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["double_click"],
          "description": "Specifies the event type. For a double click action, this property is always set to `double_click`."
        },
        "x": {
          "type": "integer",
          "description": "The x-coordinate where the double click occurred."
        },
        "y": {
          "type": "integer",
          "description": "The y-coordinate where the double click occurred."
        }
      },
      "required": ["type", "x", "y"]
    },
    "Drag": {
      "type": "object",
      "title": "Drag",
      "description": "A drag action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["drag"],
          "description": "Specifies the event type. For a drag action, this property is always set to `drag`."
        },
        "path": {
          "type": "array",
          "description": "An array of coordinates representing the path of the drag action. Coordinates will appear as an array of objects, eg [{ x: 100, y: 200 }, { x: 200, y: 300 }]",
          "items": {
            "type": "object",
            "title": "Coordinate",
            "description": "An x/y coordinate pair, e.g. `{ x: 100, y: 200 }`.",
            "properties": {
              "x": {
                "type": "integer",
                "description": "The x-coordinate."
              },
              "y": {
                "type": "integer",
                "description": "The y-coordinate."
              }
            },
            "required": ["x", "y"]
          }
        }
      },
      "required": ["type", "path"]
    },
    "KeyPressAction": {
      "type": "object",
      "title": "KeyPress",
      "description": "A collection of keypresses the model would like to perform.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["keypress"],
          "description": "Specifies the event type. For a keypress action, this property is always set to `keypress`."
        },
        "keys": {
          "type": "array",
          "description": "The combination of keys the model is requesting to be pressed. This is an array of strings, each representing a key.",
          "items": {
            "type": "string"
          }
        }
      },
      "required": ["type", "keys"]
    },
    "Move": {
      "type": "object",
      "title": "Move",
      "description": "A mouse move action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["move"],
          "description": "Specifies the event type. For a move action, this property is always set to `move`."
        },
        "x": {
          "type": "integer",
          "description": "The x-coordinate to move to."
        },
        "y": {
          "type": "integer",
          "description": "The y-coordinate to move to."
        }
      },
      "required": ["type", "x", "y"]
    },
    "Screenshot": {
      "type": "object",
      "title": "Screenshot",
      "description": "A screenshot action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["screenshot"],
          "description": "Specifies the event type. For a screenshot action, this property is always set to `screenshot`."
        }
      },
      "required": ["type"]
    },
    "Scroll": {
      "type": "object",
      "title": "Scroll",
      "description": "A scroll action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["scroll"],
          "description": "Specifies the event type. For a scroll action, this property is always set to `scroll`."
        },
        "x": {
          "type": "integer",
          "description": "The x-coordinate where the scroll occurred."
        },
        "y": {
          "type": "integer",
          "description": "The y-coordinate where the scroll occurred."
        },
        "scroll_x": {
          "type": "integer",
          "description": "The horizontal scroll distance."
        },
        "scroll_y": {
          "type": "integer",
          "description": "The vertical scroll distance."
        }
      },
      "required": ["type", "x", "y", "scroll_x", "scroll_y"]
    },
    "Type": {
      "type": "object",
      "title": "Type",
      "description": "An action to type in text.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["type"],
          "description": "Specifies the event type. For a type action, this property is always set to `type`."
        },
        "text": {
          "type": "string",
          "description": "The text to type."
        }
      },
      "required": ["type", "text"]
    },
    "Wait": {
      "type": "object",
      "title": "Wait",
      "description": "A wait action.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["wait"],
          "description": "Specifies the event type. For a wait action, this property is always set to `wait`."
        }
      },
      "required": ["type"]
    },
    "WebSearchActionSearch": {
      "type": "object",
      "title": "Search action",
      "description": "Action type \"search\" - Performs a web search query.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["search"],
          "description": "The action type."
        },
        "query": {
          "type": "string",
          "description": "The search query."
        },
        "sources": {
          "type": "array",
          "description": "The sources used in the search.",
          "items": {
            "type": "object",
            "properties": {
              "type": {
                "type": "string",
                "enum": ["url"],
                "description": "The type of source. Always `url`."
              },
              "url": {
                "type": "string",
                "description": "The URL of the source."
              }
            },
            "required": ["type", "url"]
          }
        }
      },
      "required": ["type", "query"]
    },
    "WebSearchActionOpenPage": {
      "type": "object",
      "title": "Open page action",
      "description": "Action type \"open_page\" - Opens a specific URL from search results.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["open_page"],
          "description": "The action type."
        },
        "url": {
          "type": "string",
          "description": "The URL opened by the model."
        }
      },
      "required": ["type", "url"]
    },
    "WebSearchActionFind": {
      "type": "object",
      "title": "Find action",
      "description": "Action type \"find\": Searches for a pattern within a loaded page.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["find"],
          "description": "The action type."
        },
        "url": {
          "type": "string",
          "description": "The URL of the page searched for the pattern."
        },
        "pattern": {
          "type": "string",
          "description": "The pattern or text to search for within the page."
        }
      },
      "required": ["type", "url", "pattern"]
    },
    "FileCitationBody": {
      "type": "object",
      "title": "File citation",
      "description": "A citation to a file.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["file_citation"],
          "description": "The type of the file citation. Always `file_citation`."
        },
        "file_id": {
          "type": "string",
          "description": "The ID of the file."
        },
        "index": {
          "type": "integer",
          "description": "The index of the file in the list of files."
        },
        "filename": {
          "type": "string",
          "description": "The filename of the file cited."
        }
      },
      "required": ["type", "file_id", "index", "filename"]
    },
    "UrlCitationBody": {
      "type": "object",
      "title": "URL citation",
      "description": "A citation for a web resource used to generate a model response.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["url_citation"],
          "description": "The type of the URL citation. Always `url_citation`."
        },
        "url": {
          "type": "string",
          "description": "The URL of the web resource."
        },
        "start_index": {
          "type": "integer",
          "description": "The index of the first character of the URL citation in the message."
        },
        "end_index": {
          "type": "integer",
          "description": "The index of the last character of the URL citation in the message."
        },
        "title": {
          "type": "string",
          "description": "The title of the web resource."
        }
      },
      "required": ["type", "url", "start_index", "end_index", "title"]
    },
    "ContainerFileCitationBody": {
      "type": "object",
      "title": "Container file citation",
      "description": "A citation for a container file used to generate a model response.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["container_file_citation"],
          "description": "The type of the container file citation. Always `container_file_citation`."
        },
        "container_id": {
          "type": "string",
          "description": "The ID of the container file."
        },
        "file_id": {
          "type": "string",
          "description": "The ID of the file."
        },
        "start_index": {
          "type": "integer",
          "description": "The index of the first character of the container file citation in the message."
        },
        "end_index": {
          "type": "integer",
          "description": "The index of the last character of the container file citation in the message."
        },
        "filename": {
          "type": "string",
          "description": "The filename of the container file cited."
        }
      },
      "required": [
        "type",
        "container_id",
        "file_id",
        "start_index",
        "end_index",
        "filename"
      ]
    },
    "FilePath": {
      "type": "object",
      "title": "File path",
      "description": "A path to a file.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["file_path"],
          "description": "The type of the file path. Always `file_path`."
        },
        "file_id": {
          "type": "string",
          "description": "The ID of the file."
        },
        "index": {
          "type": "integer",
          "description": "The index of the file in the list of files."
        }
      },
      "required": ["type", "file_id", "index"]
    },
    "OutputTextContent": {
      "type": "object",
      "title": "Output text",
      "description": "A text output from the model.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["output_text"],
          "description": "The type of the output text. Always `output_text`."
        },
        "text": {
          "type": "string",
          "description": "The text output from the model."
        },
        "annotations": {
          "type": "array",
          "description": "The annotations of the text output.",
          "items": {
            "anyOf": [
              {
                "$ref": "#/$defs/FileCitationBody"
              },
              {
                "$ref": "#/$defs/UrlCitationBody"
              },
              {
                "$ref": "#/$defs/ContainerFileCitationBody"
              },
              {
                "$ref": "#/$defs/FilePath"
              }
            ]
          }
        },
        "logprobs": {
          "type": "array",
          "description": "Log probability information for the output."
        }
      },
      "required": ["type", "text", "annotations"]
    },
    "RefusalContent": {
      "type": "object",
      "title": "Refusal",
      "description": "A refusal from the model.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["refusal"],
          "description": "The type of the refusal. Always `refusal`."
        },
        "refusal": {
          "type": "string",
          "description": "The refusal explanation from the model."
        }
      },
      "required": ["type", "refusal"]
    },
    "OutputMessage": {
      "type": "object",
      "title": "Output message",
      "description": "An output message from the model.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique ID of the output message."
        },
        "type": {
          "type": "string",
          "enum": ["message"],
          "description": "The type of the output message. Always `message`."
        },
        "role": {
          "type": "string",
          "enum": ["assistant"],
          "description": "The role of the output message. Always `assistant`."
        },
        "content": {
          "type": "array",
          "description": "A list of one or many output items from the model, containing different content types.",
          "items": {
            "anyOf": [
              {
                "$ref": "#/$defs/OutputTextContent"
              },
              {
                "$ref": "#/$defs/RefusalContent"
              }
            ]
          }
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the message input. One of `in_progress`, `completed`, or `incomplete`. Populated when input items are returned via API."
        }
      },
      "required": ["id", "type", "role", "content", "status"]
    },
    "FileSearchToolCall": {
      "type": "object",
      "title": "File search tool call",
      "description": "The results of a file search tool call.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique ID of the file search tool call."
        },
        "type": {
          "type": "string",
          "enum": ["file_search_call"],
          "description": "The type of the file search tool call. Always `file_search_call`."
        },
        "status": {
          "type": "string",
          "enum": [
            "in_progress",
            "searching",
            "completed",
            "incomplete",
            "failed"
          ],
          "description": "The status of the file search tool call. One of `in_progress`, `searching`, `incomplete` or `failed`,"
        },
        "queries": {
          "type": "array",
          "description": "The queries used to search for files.",
          "items": {
            "type": "string"
          }
        },
        "results": {
          "type": "array",
          "description": "The results of the file search tool call.",
          "items": {
            "type": "object",
            "properties": {
              "file_id": {
                "type": "string",
                "description": "The unique ID of the file."
              },
              "text": {
                "type": "string",
                "description": "The text that was retrieved from the file."
              },
              "filename": {
                "type": "string",
                "description": "The name of the file."
              },
              "attributes": {
                "type": "object",
                "description": "Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters, booleans, or numbers."
              },
              "score": {
                "type": "number",
                "description": "The relevance score of the file - a value between 0 and 1."
              }
            }
          }
        }
      },
      "required": ["id", "type", "status", "queries"]
    },
    "FunctionToolCall": {
      "type": "object",
      "title": "Function tool call",
      "description": "A tool call to run a function.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique ID of the function tool call."
        },
        "type": {
          "type": "string",
          "enum": ["function_call"],
          "description": "The type of the function tool call. Always `function_call`."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the function tool call generated by the model."
        },
        "name": {
          "type": "string",
          "description": "The name of the function to run."
        },
        "arguments": {
          "type": "string",
          "description": "A JSON string of the arguments to pass to the function."
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the item. One of `in_progress`, `completed`, or `incomplete`. Populated when items are returned via API."
        }
      },
      "required": ["type", "call_id", "name", "arguments"]
    },
    "WebSearchToolCall": {
      "type": "object",
      "title": "Web search tool call",
      "description": "The results of a web search tool call.",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique ID of the web search tool call."
        },
        "type": {
          "type": "string",
          "enum": ["web_search_call"],
          "description": "The type of the web search tool call. Always `web_search_call`."
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "searching", "completed", "failed"],
          "description": "The status of the web search tool call."
        },
        "action": {
          "description": "The action performed by the web search tool call.",
          "anyOf": [
            {
              "$ref": "#/$defs/WebSearchActionSearch"
            },
            {
              "$ref": "#/$defs/WebSearchActionOpenPage"
            },
            {
              "$ref": "#/$defs/WebSearchActionFind"
            }
          ]
        }
      },
      "required": ["id", "type", "status", "action"]
    },
    "ComputerToolCall": {
      "type": "object",
      "title": "Computer tool call",
      "description": "A tool call to a computer use tool.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["computer_call"],
          "description": "The type of the computer call. Always `computer_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the computer call."
        },
        "call_id": {
          "type": "string",
          "description": "An identifier used when responding to the tool call with output."
        },
        "action": {
          "anyOf": [
            {
              "$ref": "#/$defs/ClickParam"
            },
            {
              "$ref": "#/$defs/DoubleClickAction"
            },
            {
              "$ref": "#/$defs/Drag"
            },
            {
              "$ref": "#/$defs/KeyPressAction"
            },
            {
              "$ref": "#/$defs/Move"
            },
            {
              "$ref": "#/$defs/Screenshot"
            },
            {
              "$ref": "#/$defs/Scroll"
            },
            {
              "$ref": "#/$defs/Type"
            },
            {
              "$ref": "#/$defs/Wait"
            }
          ]
        },
        "pending_safety_checks": {
          "type": "array",
          "description": "The pending safety checks for the computer call.",
          "items": {
            "type": "object",
            "description": "A pending safety check for the computer call.",
            "properties": {
              "id": {
                "type": "string",
                "description": "The ID of the pending safety check."
              },
              "code": {
                "type": "string",
                "description": "The type of the pending safety check."
              },
              "message": {
                "type": "string",
                "description": "Details about the pending safety check."
              }
            },
            "required": ["id"]
          }
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the item. One of `in_progress`, `completed`, or `incomplete`. Populated when items are returned via API."
        }
      },
      "required": [
        "type",
        "id",
        "action",
        "call_id",
        "pending_safety_checks",
        "status"
      ]
    },
    "ReasoningItem": {
      "type": "object",
      "title": "Reasoning",
      "description": "A description of the chain of thought used by a reasoning model while generating a response.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["reasoning"],
          "description": "The type of the object. Always `reasoning`."
        },
        "id": {
          "type": "string",
          "description": "The unique identifier of the reasoning content."
        },
        "encrypted_content": {
          "type": "string",
          "description": "The encrypted content of the reasoning item - populated when a response is generated with `reasoning.encrypted_content` in the `include` parameter."
        },
        "summary": {
          "type": "array",
          "description": "Reasoning summary content.",
          "items": {
            "type": "object",
            "title": "Summary text",
            "description": "A summary text from the model.",
            "properties": {
              "type": {
                "type": "string",
                "enum": ["summary_text"],
                "description": "The type of the object. Always `summary_text`."
              },
              "text": {
                "type": "string",
                "description": "A summary of the reasoning output from the model so far."
              }
            },
            "required": ["type", "text"]
          }
        },
        "content": {
          "type": "array",
          "description": "Reasoning text content.",
          "items": {
            "type": "object",
            "title": "ReasoningTextContent",
            "description": "Reasoning text from the model.",
            "properties": {
              "type": {
                "type": "string",
                "enum": ["reasoning_text"],
                "description": "The type of the reasoning text. Always `reasoning_text`."
              },
              "text": {
                "type": "string",
                "description": "The reasoning text from the model."
              }
            },
            "required": ["type", "text"]
          }
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the item. One of `in_progress`, `completed`, or `incomplete`. Populated when items are returned via API."
        }
      },
      "required": ["id", "summary", "type"]
    },
    "CompactionBody": {
      "type": "object",
      "title": "Compaction item",
      "description": "A compaction item for a response.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["compaction"],
          "description": "The type of the item. Always `compaction`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the compaction item."
        },
        "encrypted_content": {
          "type": "string"
        },
        "created_by": {
          "type": "string"
        }
      },
      "required": ["type", "id", "encrypted_content"]
    },
    "ImageGenToolCall": {
      "type": "object",
      "title": "Image generation call",
      "description": "An image generation request made by the model.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["image_generation_call"],
          "description": "The type of the image generation call. Always `image_generation_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the image generation call."
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "generating", "failed"],
          "description": "The status of the image generation call."
        },
        "result": {
          "type": "string",
          "description": "The generated image encoded in base64."
        }
      },
      "required": ["type", "id", "status", "result"]
    },
    "CodeInterpreterToolCall": {
      "type": "object",
      "title": "Code interpreter tool call",
      "description": "A tool call to run code.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["code_interpreter_call"],
          "description": "The type of the code interpreter tool call. Always `code_interpreter_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the code interpreter tool call."
        },
        "status": {
          "type": "string",
          "enum": [
            "in_progress",
            "completed",
            "incomplete",
            "interpreting",
            "failed"
          ],
          "description": "The status of the code interpreter tool call. Valid values are `in_progress`, `completed`, `incomplete`, `interpreting`, and `failed`."
        },
        "container_id": {
          "type": "string",
          "description": "The ID of the container used to run the code."
        },
        "code": {
          "type": "string",
          "description": "The code to run, or null if not available."
        },
        "outputs": {
          "type": "array",
          "description": "The outputs generated by the code interpreter, such as logs or images. Can be null if no outputs are available.",
          "items": {
            "anyOf": [
              {
                "type": "object",
                "title": "Code interpreter output logs",
                "description": "The logs output from the code interpreter.",
                "properties": {
                  "type": {
                    "type": "string",
                    "enum": ["logs"],
                    "description": "The type of the output. Always `logs`."
                  },
                  "logs": {
                    "type": "string",
                    "description": "The logs output from the code interpreter."
                  }
                },
                "required": ["type", "logs"]
              },
              {
                "type": "object",
                "title": "Code interpreter output image",
                "description": "The image output from the code interpreter.",
                "properties": {
                  "type": {
                    "type": "string",
                    "enum": ["image"],
                    "description": "The type of the output. Always `image`."
                  },
                  "url": {
                    "type": "string",
                    "description": "The URL of the image output from the code interpreter."
                  }
                },
                "required": ["type", "url"]
              }
            ]
          }
        }
      },
      "required": ["type", "id", "status", "container_id", "code", "outputs"]
    },
    "LocalShellToolCall": {
      "type": "object",
      "title": "Local shell call",
      "description": "A tool call to run a command on the local shell.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["local_shell_call"],
          "description": "The type of the local shell call. Always `local_shell_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the local shell call."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the local shell tool call generated by the model."
        },
        "action": {
          "type": "object",
          "title": "Local shell exec action",
          "description": "Execute a shell command on the server.",
          "properties": {
            "type": {
              "type": "string",
              "enum": ["exec"],
              "description": "The type of the local shell action. Always `exec`."
            },
            "command": {
              "type": "array",
              "description": "The command to run.",
              "items": {
                "type": "string"
              }
            },
            "timeout_ms": {
              "type": "integer",
              "description": "Optional timeout in milliseconds for the command."
            },
            "working_directory": {
              "type": "string",
              "description": "Optional working directory to run the command in."
            },
            "env": {
              "type": "object",
              "description": "Environment variables to set for the command."
            },
            "user": {
              "type": "string",
              "description": "Optional user to run the command as."
            }
          },
          "required": ["type", "command", "env"]
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the local shell call."
        }
      },
      "required": ["type", "id", "call_id", "action", "status"]
    },
    "FunctionShellCall": {
      "type": "object",
      "title": "Shell tool call",
      "description": "A tool call that executes one or more shell commands in a managed environment.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["shell_call"],
          "description": "The type of the item. Always `shell_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the shell tool call. Populated when this item is returned via API."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the shell tool call generated by the model."
        },
        "action": {
          "type": "object",
          "title": "Shell exec action",
          "description": "Execute a shell command.",
          "properties": {
            "command": {
              "type": "array",
              "items": {
                "type": "string",
                "description": "A list of commands to run."
              }
            },
            "timeout_ms": {
              "type": "integer",
              "description": "Optional timeout in milliseconds for the commands."
            },
            "max_output_length": {
              "type": "integer",
              "description": "Optional maximum number of characters to return from each command."
            }
          },
          "required": ["command", "timeout_ms", "max_output_length"]
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed", "incomplete"],
          "description": "The status of the shell call. One of `in_progress`, `completed`, or `incomplete`."
        },
        "created_by": {
          "type": "string",
          "description": "The ID of the entity that created this tool call."
        }
      },
      "required": ["type", "id", "call_id", "action", "status"]
    },
    "FunctionShellCallOutput": {
      "type": "object",
      "title": "Shell call output",
      "description": "The output of a shell tool call.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["shell_call_output"],
          "description": "The type of the shell call output. Always `shell_call_output`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the shell call output. Populated when this item is returned via API."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the shell tool call generated by the model."
        },
        "output": {
          "type": "array",
          "description": "An array of shell call output contents",
          "items": {
            "type": "object",
            "title": "Shell call output content",
            "description": "The content of a shell call output.",
            "properties": {
              "stdout": {
                "type": "string"
              },
              "stderr": {
                "type": "string"
              },
              "outcome": {
                "description": "Represents either an exit outcome (with an exit code) or a timeout outcome for a shell call output chunk.",
                "anyOf": [
                  {
                    "type": "object",
                    "title": "Shell call timeout outcome",
                    "description": "Indicates that the shell call exceeded its configured time limit.",
                    "properties": {
                      "type": {
                        "type": "string",
                        "enum": ["timeout"],
                        "description": "The outcome type. Always `timeout`."
                      }
                    },
                    "required": ["type"]
                  },
                  {
                    "type": "object",
                    "title": "Shell call exit outcome",
                    "description": "Indicates that the shell commands finished and returned an exit code.",
                    "properties": {
                      "type": {
                        "type": "string",
                        "enum": ["exit"],
                        "description": "The outcome type. Always `exit`."
                      },
                      "exit_code": {
                        "type": "integer",
                        "description": "Exit code from the shell process."
                      }
                    },
                    "required": ["type", "exit_code"]
                  }
                ]
              },
              "created_by": {
                "type": "string"
              }
            },
            "required": ["stdout", "stderr", "outcome"]
          }
        },
        "max_output_length": {
          "type": "integer",
          "description": "The maximum length of the shell command output. This is generated by the model and should be passed back with the raw output."
        },
        "created_by": {
          "type": "string"
        }
      },
      "required": ["type", "id", "call_id", "output", "max_output_length"]
    },
    "ApplyPatchToolCall": {
      "type": "object",
      "title": "Apply patch tool call",
      "description": "A tool call that applies file diffs by creating, deleting, or updating files.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["apply_patch_call"],
          "description": "The type of the item. Always `apply_patch_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the apply patch tool call. Populated when this item is returned via API."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the apply patch tool call generated by the model."
        },
        "status": {
          "type": "string",
          "enum": ["in_progress", "completed"],
          "description": "The status of the apply patch tool call. One of `in_progress` or `completed`."
        },
        "operation": {
          "description": "One of the create_file, delete_file, or update_file operations applied via apply_patch.",
          "anyOf": [
            {
              "type": "object",
              "title": "Apply patch create file operation",
              "description": "Instruction describing how to create a file via the apply_patch tool.",
              "properties": {
                "type": {
                  "type": "string",
                  "enum": ["create_file"],
                  "description": "Create a new file with the provided diff."
                },
                "path": {
                  "type": "string",
                  "description": "Path of the file to create."
                },
                "diff": {
                  "type": "string",
                  "description": "Diff to apply."
                }
              },
              "required": ["type", "path", "diff"]
            },
            {
              "type": "object",
              "title": "Apply patch delete file operation",
              "description": "Instruction describing how to delete a file via the apply_patch tool.",
              "properties": {
                "type": {
                  "type": "string",
                  "enum": ["delete_file"],
                  "description": "Delete the specified file."
                },
                "path": {
                  "type": "string",
                  "description": "Path of the file to delete."
                }
              },
              "required": ["type", "path"]
            },
            {
              "type": "object",
              "title": "Apply patch update file operation",
              "description": "Instruction describing how to update a file via the apply_patch tool.",
              "properties": {
                "type": {
                  "type": "string",
                  "enum": ["update_file"],
                  "description": "Update an existing file with the provided diff."
                },
                "path": {
                  "type": "string",
                  "description": "Path of the file to update."
                },
                "diff": {
                  "type": "string",
                  "description": "Diff to apply."
                }
              },
              "required": ["type", "path", "diff"]
            }
          ]
        },
        "created_by": {
          "type": "string",
          "description": "The ID of the entity that created this tool call."
        }
      },
      "required": ["type", "id", "call_id", "status", "operation"]
    },
    "ApplyPatchToolCallOutput": {
      "type": "object",
      "title": "Apply patch tool call output",
      "description": "The output emitted by an apply patch tool call.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["apply_patch_call_output"],
          "description": "The type of the item. Always `apply_patch_call_output`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the apply patch tool call output. Populated when this item is returned via API."
        },
        "call_id": {
          "type": "string",
          "description": "The unique ID of the apply patch tool call generated by the model."
        },
        "status": {
          "type": "string",
          "enum": ["completed", "failed"],
          "description": "The status of the apply patch tool call output. One of `completed` or `failed`."
        },
        "output": {
          "type": "string",
          "description": "Optional textual output returned by the apply patch tool."
        },
        "created_by": {
          "type": "string",
          "description": "The ID of the entity that created this tool call output."
        }
      },
      "required": ["type", "id", "call_id", "status"]
    },
    "MCPToolCall": {
      "type": "object",
      "title": "MCP tool call",
      "description": "An invocation of a tool on an MCP server.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["mcp_call"],
          "description": "The type of the item. Always `mcp_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the tool call."
        },
        "server_label": {
          "type": "string",
          "description": "The label of the MCP server running the tool."
        },
        "name": {
          "type": "string",
          "description": "The name of the tool that was run."
        },
        "arguments": {
          "type": "string",
          "description": "A JSON string of the arguments passed to the tool."
        },
        "output": {
          "type": "string",
          "description": "The output from the tool call."
        },
        "error": {
          "type": "string",
          "description": "The error from the tool call, if any."
        },
        "status": {
          "type": "string",
          "enum": [
            "in_progress",
            "completed",
            "incomplete",
            "calling",
            "failed"
          ],
          "description": "The status of the tool call. One of `in_progress`, `completed`, `incomplete`, `calling`, or `failed`."
        },
        "approval_request_id": {
          "type": "string",
          "description": "Unique identifier for the MCP tool call approval request. Include this value in a subsequent `mcp_approval_response` input to approve or reject the corresponding tool call."
        }
      },
      "required": ["type", "id", "server_label", "name", "arguments"]
    },
    "MCPListTools": {
      "type": "object",
      "title": "MCP list tools",
      "description": "A list of tools available on an MCP server.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["mcp_list_tools"],
          "description": "The type of the item. Always `mcp_list_tools`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the list."
        },
        "server_label": {
          "type": "string",
          "description": "The label of the MCP server."
        },
        "tools": {
          "type": "array",
          "description": "The tools available on the server.",
          "items": {
            "type": "object",
            "title": "MCP list tools tool",
            "description": "A tool available on an MCP server.",
            "properties": {
              "name": {
                "type": "string",
                "description": "The name of the tool."
              },
              "description": {
                "type": "string",
                "description": "The description of the tool."
              },
              "input_schema": {
                "type": "object",
                "description": "The JSON schema describing the tool's input."
              },
              "annotations": {
                "type": "object",
                "description": "Additional annotations about the tool."
              }
            },
            "required": ["name", "input_schema"]
          }
        }
      },
      "required": ["type", "id", "server_label", "tools"]
    },
    "MCPApprovalRequest": {
      "type": "object",
      "title": "MCP approval request",
      "description": "A request for human approval of a tool invocation.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["mcp_approval_request"],
          "description": "The type of the item. Always `mcp_approval_request`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the approval request."
        },
        "server_label": {
          "type": "string",
          "description": "The label of the MCP server making the request."
        },
        "name": {
          "type": "string",
          "description": "The name of the tool to run."
        },
        "arguments": {
          "type": "string",
          "description": "A JSON string of arguments for the tool."
        }
      },
      "required": ["type", "id", "server_label", "name", "arguments"]
    },
    "CustomToolCall": {
      "type": "object",
      "title": "Custom tool call",
      "description": "A call to a custom tool created by the model.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["custom_tool_call"],
          "description": "The type of the custom tool call. Always `custom_tool_call`."
        },
        "id": {
          "type": "string",
          "description": "The unique ID of the custom tool call in the OpenAI platform."
        },
        "call_id": {
          "type": "string",
          "description": "An identifier used to map this custom tool call to a tool call output."
        },
        "name": {
          "type": "string",
          "description": "The name of the custom tool being called."
        },
        "input": {
          "type": "string",
          "description": "The input for the custom tool call generated by the model."
        }
      },
      "required": ["type", "call_id", "name", "input"]
    },
    "ToolChoiceOptions": {
      "type": "string",
      "enum": ["none", "auto", "required"],
      "title": "ToolChoiceOptions",
      "description": "Controls which (if any) tool is called by the model."
    },
    "ToolChoiceAllowed": {
      "type": "object",
      "title": "ToolChoiceAllowed",
      "description": "Constrains the tools available to the model to a pre-defined set.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["allowed_tools"],
          "description": "Allowed tool configuration type. Always `allowed_tools`."
        },
        "mode": {
          "type": "string",
          "enum": ["auto", "required"],
          "description": "Constrains the tools available to the model to a pre-defined set."
        },
        "tools": {
          "type": "array",
          "description": "A list of tool definitions that the model should be allowed to call.",
          "items": {
            "type": "object",
            "description": "A tool definition that the model should be allowed to call."
          }
        },
        "required": ["type", "mode", "tools"]
      }
    },
    "ToolChoiceTypes": {
      "type": "object",
      "title": "ToolChoiceTypes",
      "description": "Indicates that the model should use a built-in tool to generate a response.",
      "properties": {
        "type": {
          "type": "string",
          "enum": [
            "file_search",
            "web_search_preview",
            "computer_use_preview",
            "web_search_preview_2025_03_11",
            "image_generation",
            "code_interpreter"
          ],
          "description": "Types tool configuration type. Always `types`."
        }
      },
      "required": ["type"]
    },
    "ToolChoiceFunction": {
      "type": "object",
      "title": "ToolChoiceFunction",
      "description": "Use this option to force the model to call a specific function.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["function"],
          "description": "For function calling, the type is always `function`."
        },
        "name": {
          "type": "string",
          "description": "The name of the function to call."
        }
      },
      "required": ["type", "name"]
    },
    "ToolChoiceMCP": {
      "type": "object",
      "title": "ToolChoiceMCP",
      "description": "Use this option to force the model to call a specific tool on a remote MCP server.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["mcp"],
          "description": "For MCP tools, the type is always `mcp`."
        },
        "server_label": {
          "type": "string",
          "description": "The label of the MCP server to use."
        },
        "name": {
          "type": "string",
          "description": "The name of the tool to call on the server."
        }
      },
      "required": ["type", "server_label"]
    },
    "ToolChoiceCustom": {
      "type": "object",
      "title": "ToolChoiceCustom",
      "description": "Use this option to force the model to call a specific custom tool.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["custom"],
          "description": "For custom tool calling, the type is always `custom`."
        },
        "name": {
          "type": "string",
          "description": "The name of the custom tool to call."
        }
      },
      "required": ["type", "name"]
    },
    "SpecificApplyPatchParam": {
      "type": "object",
      "title": "SpecificApplyPatchParam",
      "description": "Forces the model to call the apply_patch tool when executing a tool call.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["apply_patch"],
          "description": "The tool to call. Always `apply_patch`."
        }
      },
      "required": ["type"]
    },
    "SpecificFunctionShellParam": {
      "type": "object",
      "title": "SpecificFunctionShellParam",
      "description": "Forces the model to call the shell tool when a tool call is required.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["shell"],
          "description": "The tool to call. Always `shell`."
        }
      },
      "required": ["type"]
    },
    "FunctionTool": {
      "type": "object",
      "title": "FunctionTool",
      "description": "Defines a function in your own code the model can choose to call.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["function"],
          "description": "The type of the function tool. Always `function`."
        },
        "name": {
          "type": "string",
          "description": "The name of the function to call."
        },
        "description": {
          "type": "string",
          "description": "A description of the function. Used by the model to determine whether or not to call the function."
        },
        "parameters": {
          "type": "object",
          "description": "A JSON schema object describing the parameters of the function."
        },
        "strict": {
          "type": "boolean",
          "description": "Whether to enforce strict parameter validation. Default `true`."
        }
      },
      "required": ["type", "name", "strict", "parameters"]
    },
    "FileSearchTool": {
      "type": "object",
      "title": "FileSearchTool",
      "description": "A tool that searches for relevant content from uploaded files.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["file_search"],
          "description": "The type of the file search tool. Always `file_search`."
        },
        "vector_store_ids": {
          "type": "array",
          "items": {
            "type": "string"
          },
          "description": "The IDs of the vector stores to search."
        },
        "max_num_results": {
          "type": "integer",
          "description": "The maximum number of results to return. This number should be between 1 and 50 inclusive."
        },
        "ranking_options": {
          "type": "object",
          "description": "Ranking options for search.",
          "properties": {
            "ranker": {
              "type": "string",
              "enum": ["auto", "default-2024-11-15"],
              "description": "The ranker to use for the file search."
            },
            "score_threshold": {
              "type": "number",
              "description": "The score threshold for the file search, a number between 0 and 1. Numbers closer to 1 will attempt to return only the most relevant results, but may return fewer results."
            },
            "hybrid_search": {
              "type": "object",
              "description": "Weights that control how reciprocal rank fusion balances semantic embedding matches versus sparse keyword matches when hybrid search is enabled.",
              "properties": {
                "embedding_weight": {
                  "type": "number",
                  "description": "The weight of the embedding in the reciprocal ranking fusion."
                },
                "text_weight": {
                  "type": "number",
                  "description": "The weight of the text in the reciprocal ranking fusion."
                }
              },
              "required": ["embedding_weight", "text_weight"]
            }
          }
        },
        "filters": {
          "description": "A filter to apply.",
          "anyOf": [
            {
              "$ref": "#/$defs/ComparisonFilter"
            },
            {
              "$ref": "#/$defs/CompoundFilter"
            }
          ]
        }
      },
      "required": ["type", "vector_store_ids"]
    },
    "ComputerUsePreviewTool": {
      "type": "object",
      "title": "ComputerUsePreviewTool",
      "description": "A tool that controls a virtual computer.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["computer_use_preview"],
          "description": "The type of the computer use tool. Always `computer_use_preview`."
        },
        "environment": {
          "type": "string",
          "description": "The type of computer environment to control.",
          "enum": ["windows", "mac", "linux", "ubuntu", "browser"]
        },
        "display_width": {
          "type": "integer",
          "description": "The width of the computer display."
        },
        "display_height": {
          "type": "integer",
          "description": "The height of the computer display."
        }
      },
      "required": ["type", "environment", "display_width", "display_height"]
    },
    "WebSearchTool": {
      "type": "object",
      "title": "WebSearchTool",
      "description": "Search the Internet for sources related to the prompt.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["web_search", "web_search_2025_08_26"],
          "description": "The type of the web search tool. One of `web_search` or `web_search_2025_08_26`."
        },
        "filters": {
          "type": "object",
          "description": "Filters for the search.",
          "properties": {
            "allowed_domains": {
              "type": "array",
              "description": "Allowed domains for the search. If not provided, all domains are allowed. Subdomains of the provided domains are allowed as well.",
              "items": {
                "type": "string"
              }
            }
          }
        },
        "user_location": {
          "type": "object",
          "description": "The approximate location of the user.",
          "properties": {
            "type": {
              "type": "string",
              "enum": ["approximate"],
              "description": "The type of location approximation. Always `approximate`."
            },
            "country": {
              "type": "string",
              "description": "The two-letter [ISO country code](https://en.wikipedia.org/wiki/ISO_3166-1) of the user, e.g. `US`."
            },
            "region": {
              "type": "string",
              "description": "Free text input for the region of the user, e.g. `California`."
            },
            "city": {
              "type": "string",
              "description": "Free text input for the city of the user, e.g. `San Francisco`."
            },
            "timezone": {
              "type": "string",
              "description": "The [IANA timezone](https://timeapi.io/documentation/iana-timezones) of the user, e.g. `America/Los_Angeles`."
            }
          }
        },
        "search_context_size": {
          "type": "string",
          "enum": ["low", "medium", "high"],
          "description": "High level guidance for the amount of context window space to use for the search. One of `low`, `medium`, or `high`. `medium` is the default."
        }
      },
      "required": ["type"]
    },
    "MCPToolFilter": {
      "type": "object",
      "title": "MCP tool filter",
      "description": "A filter object to specify which tools are allowed.",
      "properties": {
        "tool_names": {
          "type": "array",
          "title": "MCP allowed tools",
          "description": "List of allowed tool names.",
          "items": {
            "type": "string"
          }
        },
        "read_only": {
          "type": "boolean",
          "description": "Indicates whether or not a tool modifies data or is read-only."
        }
      }
    },
    "MCPTool": {
      "type": "object",
      "title": "MCPTool",
      "description": "Give the model access to additional tools via remote Model Context Protocol (MCP) servers.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["mcp"],
          "description": "The type of the MCP tool. Always `mcp`."
        },
        "server_label": {
          "type": "string",
          "description": "A label for this MCP server, used to identify it in tool calls."
        },
        "server_url": {
          "type": "string",
          "description": "The URL for the MCP server. One of `server_url` or `connector_id` must be provided."
        },
        "connector_id": {
          "type": "string",
          "description": "Identifier for service connectors, like those available in ChatGPT. One of `server_url` or `connector_id` must be provided.",
          "enum": [
            "connector_dropbox",
            "connector_gmail",
            "connector_googlecalendar",
            "connector_googledrive",
            "connector_microsoftteams",
            "connector_outlookcalendar",
            "connector_outlookemail",
            "connector_sharepoint"
          ]
        },
        "authorization": {
          "type": "string",
          "description": "An OAuth access token that can be used with a remote MCP server, either with a custom MCP server URL or a service connector. Your application must handle the OAuth authorization flow and provide the token here."
        },
        "server_description": {
          "type": "string",
          "description": "Optional description of the MCP server, used to provide more context."
        },
        "headers": {
          "type": "object",
          "description": "Optional HTTP headers to send to the MCP server. Use for authentication or other purposes.",
          "additionalProperties": {
            "type": "string"
          }
        },
        "allowed_tools": {
          "description": "List of allowed tool names or a filter object.",
          "anyOf": [
            {
              "type": "array",
              "title": "AllowedToolNames",
              "description": "A string array of allowed tool names",
              "items": {
                "type": "string"
              }
            },
            {
              "type": "object",
              "title": "MCP tool filter",
              "description": "A filter object to specify which tools are allowed.",
              "properties": {
                "tool_names": {
                  "type": "array",
                  "description": "List of allowed tool names.",
                  "items": {
                    "type": "string"
                  }
                },
                "read_only": {
                  "type": "boolean",
                  "description": "Indicates whether or not a tool modifies data or is read-only."
                }
              }
            }
          ]
        },
        "require_approval": {
          "description": "Specify which of the MCP server's tools require approval.",
          "anyOf": [
            {
              "type": "object",
              "title": "MCP tool approval filter",
              "description": "Specify which of the MCP server's tools require approval. Can be `always`, `never`, or a filter object associated with tools that require approval.",
              "properties": {
                "always": {
                  "$ref": "#/$defs/MCPToolFilter"
                },
                "never": {
                  "$ref": "#/$defs/MCPToolFilter"
                }
              }
            },
            {
              "type": "string",
              "title": "MCP tool approval setting",
              "description": "Specify a single approval policy for all tools. One of `always` or `never`. When set to `always`, all tools will require approval. When set to `never`, all tools will not require approval.",
              "enum": ["always", "never"]
            }
          ]
        }
      },
      "required": ["type", "server_label"]
    },
    "CodeInterpreterTool": {
      "type": "object",
      "title": "CodeInterpreterTool",
      "description": "A tool that runs Python code to help generate a response to a prompt.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["code_interpreter"],
          "description": "The type of the code interpreter tool. Always `code_interpreter`."
        },
        "container": {
          "description": "The code interpreter container. Can be a container ID or an object that specifies uploaded file IDs to make available to your code, along with an optional `memory_limit` setting.",
          "anyOf": [
            {
              "type": "string",
              "title": "Container ID",
              "description": "The container ID."
            },
            {
              "type": "object",
              "title": "CodeInterpreterToolAuto",
              "description": "Configuration for a code interpreter container. Optionally specify the IDs of the files to run the code on.",
              "properties": {
                "type": {
                  "type": "string",
                  "enum": ["auto"],
                  "description": "Always `auto`."
                },
                "file_ids": {
                  "type": "array",
                  "maxItems": 50,
                  "description": "An optional list of uploaded files to make available to your code.",
                  "items": {
                    "type": "string"
                  }
                },
                "memory_limit": {
                  "type": "string",
                  "enum": ["1g", "4g", "16g", "64g"]
                }
              },
              "required": ["type"]
            }
          ]
        }
      },
      "required": ["type", "container"]
    },
    "ImageGenTool": {
      "type": "object",
      "title": "ImageGenTool",
      "description": "A tool that generates images using the GPT image models.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["image_generation"],
          "description": "The type of the image generation tool. Always `image_generation`."
        },
        "model": {
          "type": "string",
          "description": "The image generation model to use."
        },
        "quality": {
          "type": "string",
          "enum": ["low", "medium", "high", "auto"],
          "description": "The quality of the generated image. One of `low`, `medium`, `high`, or `auto`."
        },
        "size": {
          "type": "string",
          "enum": ["1024x1024", "1024x1536", "1536x1024", "auto"],
          "description": "The size of the generated image. One of `1024x1024`, `1024x1536`, `1536x1024`, or `auto`."
        },
        "output_format": {
          "type": "string",
          "enum": ["png", "webp", "jpeg"],
          "description": "The output format of the generated image. One of `png`, `webp`, or `jpeg`."
        },
        "output_compression": {
          "type": "integer",
          "minimum": 0,
          "maximum": 100,
          "description": "Compression level for the output image."
        },
        "moderation": {
          "type": "string",
          "enum": ["auto", "low"],
          "description": "Moderation level for the generated image."
        },
        "background": {
          "type": "string",
          "enum": ["transparent", "opaque", "auto"],
          "description": "Background type for the generated image. One of `transparent`, `opaque`, or `auto`."
        },
        "input_fidelity": {
          "type": "string",
          "enum": ["high", "low"],
          "description": "Control how much effort the model will exert to match the style and features, especially facial features, of input images."
        },
        "input_image_mask": {
          "type": "object",
          "description": "Optional mask for inpainting. Contains `image_url` (string, optional) and `file_id` (string, optional).",
          "properties": {
            "image_url": {
              "type": "string",
              "description": "Base64-encoded mask image."
            },
            "file_id": {
              "type": "string",
              "description": "File ID for the mask image."
            }
          }
        },
        "partial_images": {
          "type": "integer",
          "minimum": 0,
          "maximum": 3,
          "description": "Number of partial images to generate in streaming mode, from 0 (default value) to 3."
        }
      },
      "required": ["type"]
    },
    "LocalShellToolParam": {
      "type": "object",
      "title": "LocalShellToolParam",
      "description": "A tool that allows the model to execute shell commands in a local environment.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["local_shell"],
          "description": "The type of the local shell tool. Always `local_shell`."
        }
      },
      "required": ["type"]
    },
    "FunctionShellToolParam": {
      "type": "object",
      "title": "FunctionShellToolParam",
      "description": "A tool that allows the model to execute shell commands.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["shell"],
          "description": "The type of the shell tool. Always `shell`."
        }
      },
      "required": ["type"]
    },
    "CustomToolParam": {
      "type": "object",
      "title": "CustomToolParam",
      "description": "A custom tool that processes input using a specified format.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["custom"],
          "description": "The type of the custom tool. Always `custom`."
        },
        "name": {
          "type": "string",
          "description": "The name of the custom tool, used to identify it in tool calls."
        },
        "description": {
          "type": "string",
          "description": "Optional description of the custom tool, used to provide more context."
        },
        "format": {
          "description": "The input format for the custom tool. Default is unconstrained text.",
          "anyOf": [
            {
              "type": "string",
              "enum": ["text"],
              "title": "Text format",
              "description": "Unconstrained text format. Always `text`."
            },
            {
              "type": "object",
              "title": "Grammar format",
              "description": "A grammar defined by the user.",
              "properties": {
                "type": {
                  "type": "string",
                  "enum": ["grammar"],
                  "description": "Grammar format. Always `grammar`."
                },
                "syntax": {
                  "type": "string",
                  "enum": ["lark", "regex"],
                  "description": "The syntax of the grammar definition. One of `lark` or `regex`."
                },
                "definition": {
                  "type": "string",
                  "description": "The grammar definition."
                }
              },
              "required": ["type", "syntax", "definition"]
            }
          ]
        }
      },
      "required": ["type", "name"]
    },
    "WebSearchPreviewTool": {
      "type": "object",
      "title": "WebSearchPreviewTool",
      "description": "This tool searches the web for relevant results to use in a response.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["web_search_preview", "web_search_preview_2025_03_11"],
          "description": "The type of the web search tool. One of `web_search_preview` or `web_search_preview_2025_03_11`."
        },
        "user_location": {
          "type": "object",
          "properties": {
            "type": {
              "type": "string",
              "enum": ["approximate"],
              "description": "The type of location approximation. Always `approximate`."
            },
            "country": {
              "type": "string",
              "description": "The two-letter [ISO country code](https://en.wikipedia.org/wiki/ISO_3166-1) of the user, e.g. `US`."
            },
            "region": {
              "type": "string",
              "description": "Free text input for the region of the user, e.g. `California`."
            },
            "city": {
              "type": "string",
              "description": "Free text input for the city of the user, e.g. `San Francisco`."
            },
            "timezone": {
              "type": "string",
              "description": "The [IANA timezone](https://timeapi.io/documentation/iana-timezones) of the user, e.g. `America/Los_Angeles`."
            }
          },
          "required": ["type"]
        },
        "search_context_size": {
          "type": "string",
          "enum": ["low", "medium", "high"],
          "description": "High level guidance for the amount of context window space to use for the search. One of `low`, `medium`, or `high`. `medium` is the default."
        }
      },
      "required": ["type"]
    },
    "ApplyPatchToolParam": {
      "type": "object",
      "title": "ApplyPatchToolParam",
      "description": "Allows the assistant to create, delete, or update files using unified diffs.",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["apply_patch"],
          "description": "The type of the tool. Always `apply_patch`."
        }
      },
      "required": ["type"]
    },
    "TextResponseFormatConfiguration": {
      "title": "TextResponseFormatConfiguration",
      "description": "An object specifying the format that the model must output.",
      "anyOf": [
        {
          "$ref": "#/$defs/ResponseFormatText"
        },
        {
          "$ref": "#/$defs/TextResponseFormatJsonSchema"
        },
        {
          "$ref": "#/$defs/ResponseFormatJsonObject"
        }
      ]
    }
  },
  "properties": {
    "id": {
      "type": "string",
      "description": "Unique identifier for this Response."
    },
    "created_at": {
      "type": "integer",
      "description": "Unix timestamp (in seconds) of when this Response was created."
    },
    "incomplete_details": {
      "type": "object",
      "description": "Details about why the response is incomplete.",
      "properties": {
        "reason": {
          "type": "string",
          "description": "The reason why the response is incomplete.",
          "enum": ["max_output_tokens", "content_filter"]
        }
      }
    },
    "instructions": {
      "type": "string",
      "description": "A system (or developer) message inserted into the model's context."
    },
    "metadata": {
      "type": "object",
      "description": "Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters."
    },
    "model": {
      "description": "ID of the model to use.",
      "type": "string"
    },
    "object": {
      "type": "string",
      "enum": ["response"],
      "description": "The object type of this resource - always set to `response`."
    },
    "output": {
      "type": "array",
      "description": "An array of content items generated by the model.",
      "items": {
        "anyOf": [
          {
            "$ref": "#/$defs/OutputMessage"
          },
          {
            "$ref": "#/$defs/FileSearchToolCall"
          },
          {
            "$ref": "#/$defs/FunctionToolCall"
          },
          {
            "$ref": "#/$defs/WebSearchToolCall"
          },
          {
            "$ref": "#/$defs/ComputerToolCall"
          },
          {
            "$ref": "#/$defs/ReasoningItem"
          },
          {
            "$ref": "#/$defs/CompactionBody"
          },
          {
            "$ref": "#/$defs/ImageGenToolCall"
          },
          {
            "$ref": "#/$defs/CodeInterpreterToolCall"
          },
          {
            "$ref": "#/$defs/LocalShellToolCall"
          },
          {
            "$ref": "#/$defs/FunctionShellCall"
          },
          {
            "$ref": "#/$defs/FunctionShellCallOutput"
          },
          {
            "$ref": "#/$defs/ApplyPatchToolCall"
          },
          {
            "$ref": "#/$defs/ApplyPatchToolCallOutput"
          },
          {
            "$ref": "#/$defs/MCPToolCall"
          },
          {
            "$ref": "#/$defs/MCPListTools"
          },
          {
            "$ref": "#/$defs/MCPApprovalRequest"
          },
          {
            "$ref": "#/$defs/CustomToolCall"
          }
        ]
      }
    },
    "parallel_tool_calls": {
      "type": "boolean",
      "default": true,
      "description": "Whether to allow the model to run tool calls in parallel."
    },
    "temperature": {
      "type": "number",
      "description": "What sampling temperature to use, between 0 and 2. Higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic. We generally recommend altering this or top_p but not both."
    },
    "tool_choice": {
      "anyOf": [
        {
          "$ref": "#/$defs/ToolChoiceOptions"
        },
        {
          "$ref": "#/$defs/ToolChoiceAllowed"
        },
        {
          "$ref": "#/$defs/ToolChoiceTypes"
        },
        {
          "$ref": "#/$defs/ToolChoiceFunction"
        },
        {
          "$ref": "#/$defs/ToolChoiceMCP"
        },
        {
          "$ref": "#/$defs/ToolChoiceCustom"
        },
        {
          "$ref": "#/$defs/SpecificApplyPatchParam"
        },
        {
          "$ref": "#/$defs/SpecificFunctionShellParam"
        }
      ],
      "description": "How the model should select which tool (or tools) to use when generating a response. See the tools parameter to see how to specify which tools the model can call."
    },
    "tools": {
      "type": "array",
      "items": {
        "anyOf": [
          {
            "$ref": "#/$defs/FunctionTool"
          },
          {
            "$ref": "#/$defs/FileSearchTool"
          },
          {
            "$ref": "#/$defs/ComputerUsePreviewTool"
          },
          {
            "$ref": "#/$defs/WebSearchTool"
          },
          {
            "$ref": "#/$defs/MCPTool"
          },
          {
            "$ref": "#/$defs/CodeInterpreterTool"
          },
          {
            "$ref": "#/$defs/ImageGenTool"
          },
          {
            "$ref": "#/$defs/LocalShellToolParam"
          },
          {
            "$ref": "#/$defs/FunctionShellToolParam"
          },
          {
            "$ref": "#/$defs/CustomToolParam"
          },
          {
            "$ref": "#/$defs/WebSearchPreviewTool"
          },
          {
            "$ref": "#/$defs/ApplyPatchToolParam"
          }
        ]
      },
      "description": "An array of tools the model may call while generating a response. You can specify which tool to use by setting the tool_choice parameter."
    },
    "top_p": {
      "type": "number",
      "minimum": 0,
      "maximum": 1,
      "description": "An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So 0.1 means only the tokens comprising the top 10% probability mass are considered."
    },
    "background": {
      "type": "boolean",
      "default": false,
      "description": "Whether to run the model response in the background."
    },
    "max_output_tokens": {
      "type": "integer",
      "description": "An upper bound for the number of tokens that can be generated for a response, including visible output tokens and reasoning tokens."
    },
    "max_tool_calls": {
      "type": "integer",
      "description": "The maximum number of total calls to built-in tools that can be processed in a response. This maximum number applies across all built-in tool calls, not per individual tool. Any further attempts to call a tool by the model will be ignored."
    },
    "previous_response_id": {
      "type": "string",
      "description": "The unique ID of the previous response to the model. Use this to create multi-turn conversations."
    },
    "prompt": {
      "type": "object",
      "properties": {
        "id": {
          "type": "string",
          "description": "The unique identifier of the prompt template to use."
        },
        "variables": {
          "type": "object",
          "description": "Optional map of values to substitute in for variables in your prompt. The substitution values can either be strings, or other Response input types like images or files."
        },
        "version": {
          "type": "string",
          "description": "Optional version of the prompt template."
        }
      },
      "required": ["id"],
      "description": "Reference to a prompt template and its variables."
    },
    "reasoning": {
      "type": "object",
      "properties": {
        "effort": {
          "type": "string",
          "enum": ["low", "medium", "high"],
          "description": "Constrains effort on reasoning for reasoning models."
        }
      },
      "description": "Configuration options for reasoning models."
    },
    "service_tier": {
      "type": "string",
      "enum": ["auto", "default", "flex", "scale", "priority"],
      "default": "auto",
      "description": "Specifies the processing type used for serving the request."
    },
    "status": {
      "type": "string",
      "enum": [
        "completed",
        "failed",
        "in_progress",
        "cancelled",
        "queued",
        "incomplete"
      ],
      "description": "The status of the response generation. One of `completed`, `failed`, `in_progress`, `cancelled`, `queued`, or `incomplete`."
    },
    "text": {
      "type": "object",
      "properties": {
        "format": {
          "$ref": "#/$defs/TextResponseFormatConfiguration"
        },
        "verbosity": {
          "type": "string",
          "enum": ["low", "medium", "high"],
          "description": "Constrains the verbosity of the model's response. Lower values will result in more concise responses, while higher values will result in more verbose responses."
        }
      },
      "description": "Configuration options for a text response from the model. Can be plain text or structured JSON data."
    },
    "top_logprobs": {
      "type": "integer",
      "minimum": 0,
      "maximum": 20,
      "description": "An integer between 0 and 20 specifying the number of most likely tokens to return at each token position, each with an associated log probability."
    },
    "truncation": {
      "type": "string",
      "enum": ["auto", "disabled"],
      "default": "disabled",
      "description": "The truncation strategy to use for the model response."
    },
    "usage": {
      "type": "object",
      "description": "Represents token usage details including input tokens, output tokens, a breakdown of output tokens, and the total tokens used.",
      "properties": {
        "input_tokens": {
          "type": "integer",
          "description": "The number of input tokens."
        },
        "input_tokens_details": {
          "type": "object",
          "description": "A detailed breakdown of the input tokens.",
          "properties": {
            "cached_tokens": {
              "type": "integer",
              "description": "The number of tokens that were retrieved from the cache."
            }
          },
          "required": ["cached_tokens"]
        },
        "output_tokens": {
          "type": "integer",
          "description": "The number of output tokens."
        },
        "output_tokens_details": {
          "type": "object",
          "description": "A detailed breakdown of the output tokens.",
          "properties": {
            "reasoning_tokens": {
              "type": "integer",
              "description": "The number of reasoning tokens."
            },
            "tool_output_tokens": {
              "type": "integer",
              "description": "The number of tokens that were used for tool output."
            }
          },
          "required": ["reasoning_tokens", "tool_output_tokens"]
        },
        "total_tokens": {
          "type": "integer",
          "description": "The total number of tokens used."
        }
      },
      "required": [
        "input_tokens",
        "input_tokens_details",
        "output_tokens",
        "output_tokens_details",
        "total_tokens"
      ]
    },
    "user": {
      "type": "string",
      "description": "This field is being replaced by safety_identifier and prompt_cache_key. Use prompt_cache_key instead to maintain caching optimizations. A stable identifier for your end-users. Used to boost cache hit rates by better bucketing similar requests and to help OpenAI detect and prevent abuse. "
    }
  },
  "required": [
    "id",
    "created_at",
    "model",
    "object",
    "output",
    "parallel_tool_calls",
    "temperature",
    "tool_choice",
    "tools",
    "top_p",
    "background",
    "max_output_tokens",
    "service_tier",
    "status",
    "truncation"
  ]
}
```

#### Example Requests

- cURL

```curl
curl "{{ BACKEND_HOST_URL }}/openai/v1/responses" \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${UFCLOUD_API_KEY}" \
  -d '{
        "input": "Tell me a three sentence bedtime story about a unicorn.",
        "model": "openai/gpt-oss-120b"
      }'
```

- Python SDK

```python
import os

from ufcloud import Ufcloud

client = Ufcloud(
    # This is the default and can be omitted
    api_key=os.environ.get("UFCLOUD_API_KEY"),
)

responses = client.responses.create(
    input="Tell me a three sentence bedtime story about a unicorn.",
    model="openai/gpt-oss-120b",
)

print(responses)
```

- TypeScript SDK

```javascript
import Ufcloud from "ufcloud";

const client = new Ufcloud({
  // This is the default and can be omitted
  apiKey: process.env.UFCLOUD_API_KEY,
});

const responses = await client.responses.create({
  input: "Tell me a three sentence bedtime story about a unicorn.",
  model: "openai/gpt-oss-120b",
});
console.log(responses);
```

- OpenAI Python

```python
import os

from openai import OpenAI

client = OpenAI(
    base_url="{{ BACKEND_HOST_URL }}/openai/v1",
    # This is the default and can be omitted
    api_key=os.environ.get("UFCLOUD_API_KEY"),
)

response = client.responses.create(
    input="Tell me a three sentence bedtime story about a unicorn.",
    model="openai/gpt-oss-120b",
)

print(response)
```

- OpenAI TS

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "{{ BACKEND_HOST_URL }}/openai/v1",
  // This is the default and can be omitted
  apiKey: process.env.UFCLOUD_API_KEY,
});

const response = await client.responses.create({
  input: "Tell me a three sentence bedtime story about a unicorn.",
  model: "openai/gpt-oss-120b",
});

console.log(response);
```

#### Example Response

```json
{
  "id": "resp_273c7d0120824462a9985d7d781bd193",
  "created_at": 1767670176,
  "incomplete_details": null,
  "instructions": null,
  "metadata": null,
  "model": "openai/gpt-oss-120b",
  "object": "response",
  "output": [
    {
      "id": "rs_c8095f99ba4b49d9b881687210a32b20",
      "summary": [],
      "type": "reasoning",
      "content": [
        {
          "text": "We need to respond ...",
          "type": "reasoning_text"
        }
      ],
      "encrypted_content": null,
      "status": null
    },
    {
      "id": "msg_f97384bf6e65460c9bc92d32d449a05b",
      "content": [
        {
          "annotations": [],
          "text": "Under a moonlit sky, ...",
          "type": "output_text",
          "logprobs": null
        }
      ],
      "role": "assistant",
      "status": "completed",
      "type": "message"
    }
  ],
  "input_messages": null,
  "output_messages": null,
  "parallel_tool_calls": true,
  "temperature": 1,
  "tool_choice": "auto",
  "tools": [],
  "top_p": 1,
  "background": false,
  "max_output_tokens": 130996,
  "max_tool_calls": null,
  "previous_response_id": null,
  "prompt": null,
  "reasoning": null,
  "service_tier": "auto",
  "status": "completed",
  "text": null,
  "top_logprobs": null,
  "truncation": "disabled",
  "usage": {
    "input_tokens": 76,
    "input_tokens_details": {
      "cached_tokens": 48
    },
    "output_tokens": 145,
    "output_tokens_details": {
      "reasoning_tokens": 37,
      "tool_output_tokens": 0
    },
    "total_tokens": 221
  },
  "user": null
}
```

## Embeddings

### Create embeddings

**POST {{ BACKEND_HOST_URL }}/openai/v1/embeddings**

Creates an embedding vector representing the input text.

#### Request Body

```json
{
  "title": "CreateEmbeddingRequest",
  "type": "object",
  "properties": {
    "input": {
      "description": "Single text chunk to embed.",
      "oneOf": [
        {
          "type": "string"
        },
        {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      ]
    },
    "model": {
      "description": "ID of the embedding model to use.",
      "type": "string"
    },
    "encoding_format": {
      "type": "string",
      "description": "The format to return the embeddings in. Can be either float or base64.",
      "enum": ["float", "base64"]
    },
    "user": {
      "type": "string",
      "description": "A unique identifier representing your end-user"
    },
    "truncate_prompt_tokens": {
      "type": "number",
      "description": "Number of tokens to truncate from the prompt if it exceeds model limits.",
      "minimum": -1
    }
  },
  "required": ["model", "input"]
}
```

#### Response Object

```json
{
  "title": "CreateEmbeddingResponse",
  "type": "object",
  "$defs": {
    "EmbeddingData": {
      "type": "object",
      "title": "EmbeddingData",
      "description": "Schema for a single embedding result.",
      "properties": {
        "index": {
          "type": "integer",
          "description": "Index of the input chunk."
        },
        "embedding": {
          "description": "List of embedding values or a base64 encoded string.",
          "oneOf": [
            {
              "type": "array",
              "items": {
                "type": "number"
              }
            },
            {
              "type": "string"
            }
          ]
        },
        "object": {
          "type": "string",
          "description": "The object type, which is always \"embedding\".",
          "enum": ["embedding"]
        }
      },
      "required": ["index", "embedding"]
    },
    "UsageInfo": {
      "type": "object",
      "title": "UsageInfo",
      "description": "Usage statistics for the completion request.",
      "properties": {
        "prompt_tokens": {
          "type": "integer",
          "description": "Number of tokens in the prompt."
        },
        "total_tokens": {
          "type": "integer",
          "description": "Total number of tokens used in the request (prompt + completion)."
        },
        "completion_tokens": {
          "type": "integer",
          "description": "Number of tokens in the generated completion."
        },
        "prompt_tokens_details": {
          "type": "object",
          "description": "Breakdown of tokens in the prompt.",
          "properties": {
            "cached_tokens": {
              "type": "integer",
              "description": "Number of tokens that were cached and reused."
            }
          }
        }
      },
      "required": ["prompt_tokens", "total_tokens"]
    }
  },
  "properties": {
    "id": {
      "type": "string",
      "description": "Unique identifier for the embedding response."
    },
    "model": {
      "type": "string",
      "description": "ID of the embedding model used."
    },
    "created": {
      "type": "integer",
      "description": "Timestamp of when the embeddings were created."
    },
    "data": {
      "type": "array",
      "description": "List of embedding results.",
      "items": {
        "$ref": "#/$defs/EmbeddingData"
      }
    },
    "object": {
      "type": "string",
      "description": "The object type, which is always \"list\".",
      "default": "list"
    },
    "usage": {
      "$ref": "#/$defs/UsageInfo"
    }
  },
  "required": ["id", "model", "data", "object", "usage"]
}
```

#### Example Requests

- cURL

```curl
curl "{{ BACKEND_HOST_URL }}/openai/v1/embeddings" \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${UFCLOUD_API_KEY}" \
  -d '{
        "input": "The food was delicious and the waiter...",
        "model": "BAAI/bge-base-en-v1.5",
        "encoding_format": "float",
      }'
```

- Python SDK

```python
import os

from ufcloud import Ufcloud

client = Ufcloud(
    # This is the default and can be omitted
    api_key=os.environ.get("UFCLOUD_API_KEY"),
)

embeddings_response = client.embeddings.create(
    input="The food was delicious and the waiter...",
    model="BAAI/bge-base-en-v1.5",
    encoding_format="float",
)

print(embeddings_response)
```

- TypeScript SDK

```javascript
import Ufcloud from "ufcloud";

const client = new Ufcloud({
  // This is the default and can be omitted
  apiKey: process.env.UFCLOUD_API_KEY,
});

const embeddingsResponse = await client.embeddings.create({
  input: "The food was delicious and the waiter...",
  model: "BAAI/bge-base-en-v1.5",
  encoding_format: "float",
});
console.log(embeddingsResponse);
```

- OpenAI Python

```python
import os

from openai import OpenAI

client = OpenAI(
    base_url="{{ BACKEND_HOST_URL }}/openai/v1",
    # This is the default and can be omitted
    api_key=os.environ.get("UFCLOUD_API_KEY"),
)

embeddings_response = client.embeddings.create(
    input="The food was delicious and the waiter...",
    model="BAAI/bge-base-en-v1.5",
    encoding_format="float",
)

print(embeddings_response)
```

- OpenAI TS

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "{{ BACKEND_HOST_URL }}/openai/v1",
  // This is the default and can be omitted
  apiKey: process.env.UFCLOUD_API_KEY,
});

const embeddingsResponse = await client.embeddings.create({
  input: "The food was delicious and the waiter...",
  model: "BAAI/bge-base-en-v1.5",
  model: "float",
});

console.log(embeddingsResponse);
```

#### Example Response

```json
{
  "id": "embd-4fc2a1d629594853a5e5dc990c2b21a7",
  "model": "BAAI/bge-large-en-v1.5",
  "created": 1766039116,
  "data": [
    {
      "index": 0,
      "embedding": [
        0.05032513290643692,
        0.007264506537467241,
        ...
        0.0037901774048805237,
        -0.03558555245399475,
        -0.011054683476686478
      ],
      "object": "embedding"
    }
  ],
  "object": "list",
  "usage": {
    "prompt_tokens": 3,
    "total_tokens": 3,
    "completion_tokens": 0,
    "prompt_token_details": null
  }
}

```
