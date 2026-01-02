---
description: Comprehensive reference documentation for the UF Cloud API, including endpoints, parameters, and examples.
title: API Reference - UFCloudDocs
---

# UF Cloud API Reference

## Chat

### Create chat completion test

**POST /openai/v1/chat/completions**

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

```shell
curl "http://localhost:8000/openai/v1/chat/completions" \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${UF_API_KEY}" \
  -d '{
        "messages": [
          {
            "role": "user",
            "content": ""
          }
        ],
        "model": "",
        "temperature": 1,
        "max_tokens": 1024,
        "top_p": 1,
        "stream": false
      }'
```

- Python SDK

```python
import openai

client = openai.OpenAI(
    api_key="your-api-key",
    base_url="https://api.ufcloud.io/v1"
)

response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

- TypeScript SDK

```python
import openai

client = openai.OpenAI(
    api_key="your-api-key",
    base_url="https://api.ufcloud.io/v1"
)

response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "Hello!"}]
)

```

- OpenAI Python

```python
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "http://localhost:8000/openai/v1",
  apiKey: "UF_API_KEY"
});

const chatCompletion = await client.chat.completions.create({
  "messages": [
    {
      "role": "user",
      "content": ""
    }
  ],
  "model": "",
  "temperature": 1,
  "max_tokens": 1024,
  "top_p": 1,
  "stream": false
});

console.log(chatCompletion.choices[0].message.content);

```

- OpenAI TS

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "http://localhost:8000/openai/v1",
  apiKey: "UF_API_KEY",
});

const chatCompletion = await client.chat.completions.create({
  messages: [
    {
      role: "user",
      content: "",
    },
  ],
  model: "",
  temperature: 1,
  max_tokens: 1024,
  top_p: 1,
  stream: false,
});

console.log(chatCompletion.choices[0].message.content);
```

#### Example Response

```json
{
  "id": "chatcmpl-123",
  "object": "chat.completion",
  "created": 1677652288,
  "model": "gpt-4",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Hello! How can I help you?"
      },
      "finish_reason": "stop"
    }
  ]
}
```

### Create chat completion2

**POST** `/openai/v1/chat/completions`

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

```curl
curl https://api.ufcloud.io/v1/chat/completions \
  -H "Authorization: Bearer $UFCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4",
    "messages": [
      {"role": "user", "content": "Hello!"}
    ]
  }'
```

```python
import openai

client = openai.OpenAI(
    api_key="your-api-key",
    base_url="https://api.ufcloud.io/v1"
)

response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

#### Example Response

```json
{
  "id": "chatcmpl-123",
  "object": "chat.completion",
  "created": 1677652288,
  "model": "gpt-4",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Hello! How can I help you?"
      },
      "finish_reason": "stop"
    }
  ]
}
```

## Chat1

### Create chat completion

**POST** `/openai/v1/chat/completions`

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

```curl
curl https://api.ufcloud.io/v1/chat/completions \
  -H "Authorization: Bearer $UFCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4",
    "messages": [
      {"role": "user", "content": "Hello!"}
    ]
  }'
```

```python
import openai

client = openai.OpenAI(
    api_key="your-api-key",
    base_url="https://api.ufcloud.io/v1"
)

response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

#### Example Response

```json
{
  "id": "chatcmpl-123",
  "object": "chat.completion",
  "created": 1677652288,
  "model": "gpt-4",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Hello! How can I help you?"
      },
      "finish_reason": "stop"
    }
  ]
}
```

### Create chat completion2

**POST** `/openai/v1/chat/completions`

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

```curl
curl https://api.ufcloud.io/v1/chat/completions \
  -H "Authorization: Bearer $UFCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4",
    "messages": [
      {"role": "user", "content": "Hello!"}
    ]
  }'
```

```python
import openai

client = openai.OpenAI(
    api_key="your-api-key",
    base_url="https://api.ufcloud.io/v1"
)

response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

#### Example Response

```json
{
  "id": "chatcmpl-123",
  "object": "chat.completion",
  "created": 1677652288,
  "model": "gpt-4",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Hello! How can I help you?"
      },
      "finish_reason": "stop"
    }
  ]
}
```
