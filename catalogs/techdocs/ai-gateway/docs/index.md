
## Get start using python sdk to call models via AI gateway

### Purpose

This guide helps developers integrate and call various AI models through the Portkey AI Gateway using the Python SDK.

### Core Capabilities

Covers basic calls, custom configurations, request parameter specifications, and advanced features such as caching, retries, fallbacks, load balancing, and conditional routing.

### Target Audience

Python developers looking to integrate AI models into their applications via the Portkey AI Gateway.

## Prerequisites

### Obtain Essential Configuration Information

- Request an API key from the AI Gateway maintenance team.
- Confirm available providers (e.g., @azure-openai-provider, @openai-virtual-key) and supported models (e.g., gpt-4o-mini, claude-3.5-sonnet-20240620) with the maintenance team.


### Environment Requirements
- Supported Python versions: 3.8+ (inferred from standard SDK compatibility; not explicitly specified in the original documentation).
- Required tool: Portkey Python SDK (installation instructions provided in subsequent steps).

### get API key form AI gateway maintain team

You will receive the following:
- API key
- List of available providers and compatible models

## Python integration
The official Portkey Python SDK simplifies deploying AI applications to production. It enables seamless integration of Portkey into any Python-based project.

### Install the Portkey SDK from PyPI:

```
pip install portkey-ai
```

## Examples
### example: quick start 
- Leverages default configurations associated with your API key in the control plane.
  
For more details, refer to the official documentation: https://portkey.ai/docs/api-reference/sdk/python

```python

from portkey_ai import Portkey

client = Portkey(
  api_key="u6**************Vz", ## which is configured in control plane
  provider="@azure-openai-provider" ## which is configured in control plane
)

response = client.chat.completions.create(
  messages=[{"role": "user", "content": "Hello, world!"}],
  model="gpt-4o-mini"  ## Example provider/model
)

print(response)

```


### example: custom header


- Supported custom headers include: trace_id, metadata (supports dynamic data), and base_url (for self-hosted gateways).


```python

from portkey_ai import Portkey

client = Portkey(
  api_key="u6**************Vz", ## which is configured in control plane
  provider="@azure-openai-provider"， ## which is configured in control plane
  trace_id = "TRACE_ID",
  metadata = {"_user": "wenpeng.lei", "anyOtherKey": "anyOtherValue" }, ## can be customized base on requirement
  base_url = "SELF_HOSTED_GATEWAY_URL" ## Self-Hosted Gateway URL
)

response = client.chat.completions.create(
  messages=[{"role": "user", "content": "Hello, world!"}],
  model="gpt-4o-mini"  ## Example provider/model
)

print(response)

```

Or configure headers at runtime:
```python

from portkey_ai import Portkey

client = Portkey(
  api_key="u6**************Vz", ## which is configured in control plane
  provider="@azure-openai-provider"， ## which is configured in control plane 
)

response = client.with_options({
  trace_id = "TRACE_ID",
  metadata = {"_user": "wenpeng.lei", "anyOtherKey": "anyOtherValue" }, ## can be customized base on requirement
  base_url = "SELF_HOSTED_GATEWAY_URL" ## Self-Hosted Gateway URL
}).chat.completions.create(
  messages=[{"role": "user", "content": "Hello, world!"}],
  model="gpt-4o-mini"  ## Example provider/model
)

print(response)

```

For a complete list of supported custom headers, visit: https://portkey.ai/docs/api-reference/inference-api/headers#list-of-all-headers

### example: custom config support for single request

Configurations are compatible with all integration methods:

- Via the config parameter in the Portkey SDK client (directly or through frameworks)
- Via config headers in the OpenAI SDK
- Via the x-portkey-config header in REST API calls

The following examples demonstrate configuration via the Portkey SDK client's config parameter.


#### using pre-defined config from control panel 

 (Contact the AI Gateway maintenance team to obtain the config ID.)

A request-specific configuration overrides the default config linked to your API key. The default config is only applied if no other config is specified in the request.

```python
from portkey_ai import Portkey

client = Portkey(
  api_key="u6**************Vz", ## which is configured in control plane
  provider="@azure-openai-provider"， ## which is configured in control plane
  config="pc-***" ## Supports a string config id or a config object. if no config provide, will use the default config attached to the API key
)

response = client.chat.completions.create(
  messages=[{"role": "user", "content": "Hello, world!"}],
  model="gpt-4o-mini"  ## Example provider/model
)

print(response)

```

#### using custom config object - cache and retry

```python
from portkey_ai import Portkey

client = Portkey(
  api_key="u6**************Vz", ## which is configured in control plane
  provider="@azure-openai-provider"， ## which is configured in control plane
  config={
    "cache": { ## Optional
      "mode": "semantic",
      "max_age": 10000
    },
    "retry": { ## Optional
      "attempts": 5,
      "on_status_codes": []
    }
  }, ## Simple config with cache and retry
)

response = client.chat.completions.create(
    messages=[{"role": "user", "content": "Hello, world!"}],
    model="gpt-4o-mini"  ## Example provider/model
)

print(response)

```

For more details:
- `cache`: https://portkey.ai/docs/product/ai-gateway/cache-simple-and-semantic
- `retry`: https://portkey.ai/docs/api-reference/inference-api/config-object#retry-object-details

#### using custom config object - fallback

```python
from portkey_ai import Portkey

client = Portkey(
  api_key="u6**************Vz", ## which is configured in control plane
  provider="@azure-openai-provider"， ## which is configured in control plane
  config={
    "strategy": {
        "mode": "fallback"
    },
    "targets": [
      {
        "provider":"@openai-virtual-key",
        "override_params": {
            "model": "gpt-4o"
        }
      },
      {
        "provider":"@anthropic-virtual-key",
        "override_params": {
            "model": "claude-3.5-sonnet-20240620"
        }
      }
    ]
  }, ## Simple config with fallback
)

response = client.chat.completions.create(
  messages=[{"role": "user", "content": "Hello, world!"}],
  model="gpt-4o-mini"  ## Example provider/model
)

print(response)

```
For more details:
- `fallback`: https://portkey.ai/docs/product/ai-gateway/fallbacks

#### using custom config object - load balance

This example distributes 75% of requests to an OpenAI account and 25% to an Azure OpenAI account.

```python
from portkey_ai import Portkey

client = Portkey(
  api_key="u6**************Vz", ## which is configured in control plane
  provider="@azure-openai-provider"， ## which is configured in control plane
  config={
    "strategy": {
        "mode": "loadbalance"
    },
    "targets": [
      {
        "provider":"@openai-virtual-key",
        "weight": 0.75
      },
      {
        "provider":"@azure-virtual-key",
        "weight": 0.25
      }
    ]
  }, ## Simple config with load balance
)

response = client.chat.completions.create(
  messages=[{"role": "user", "content": "Hello, world!"}],
  model="gpt-4o-mini"  ## Example provider/model
)

print(response)

```
For more details:

- `load balance`: https://portkey.ai/docs/product/ai-gateway/load-balancing

#### using custom config object - conditional routing

Route requests to different providers based on custom conditions, such as:

 - If this user is on the `paid plan`, route their request to a `custom fine-tuned model`
 - If the model parameter is set to `fastest`, route to `gpt-4o-mini`, if `smartest`, route to `openai o1`
 - If this user is an `EU resident`, call an `EU hosted model`
 - If the `temperature` parameter is above `0.7`, route to a more creative model
 - If the request is coming from `testing environment` with a `llm-pass-through` flag, route it to the `cheapest model`
 - ..and more!

Routing logic can be based on:
- `Metadata` - Custom key-value pairs you pass with your requests
- `Request Parameters` - Any parameter that you send in your original LLM request (like model, temperature, max_tokens)
- `Request URL Path` - Match against `url.pathname` (for example, route `/embeddings` requests)

**Note**: Only two-segment keys are supported (e.g., metadata.user_plan, params.model). Nested paths like metadata.features.new_model_enabled are not allowed.


**List of Condition Query Operators**

| Operator | Description              |
| -------- | ------------------------ |
| $eq      | Equals                   |
| $ne      | Not equals               |
| $in      | In array                 |
| $nin     | Not in array             |
| $regex   | Match the regex          |
| $gt      | Greater than             |
| $gte     | Greater than or equal to |
| $lt      | Less than                |
| $lte     | Less than or equal to    |


##### Model Parameter Based Routing
```python
from portkey_ai import Portkey

client = Portkey(
  api_key="u6**************Vz", ## which is configured in control plane
  provider="@azure-openai-provider"， ## which is configured in control plane
  config={
    "strategy": {
      "mode": "conditional",
      "conditions": [
        {
          "query": {
            "params.model": {
              "$eq": "fastest"
            }
          },
          "then": "fastest-model-target"
        },
        {
          "query": {
            "params.model": {
              "$eq": "smartest"
            }
          },
          "then": "smartest-model-target"
        }
      ],
      "default": "fastest-model-target"
    },
    "targets": [
      {
        "name": "smartest-model-target",
        "provider":"@anthropic-vk",
        "override_params": {
          "model": "claude-3.5-sonnet"
        }
      },
      {
        "name": "fastest-model-target",
        "provider":"@oai-vk",
        "override_params": {
          "model": "gpt-4o-mini"
        }
      }
    ]
  }, ## Simple config with param based routing
)

## Option 1
## This will use the "smartest" model (claude-3.5-sonnet)
completion = client.chat.completions.create(
  model="smartest",  ## This value matches our conditional routing condition
  messages=[
    {"role": "developer", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Explain quantum computing to a 5-year-old"}
  ]
)

## Option 2
## This will use the "fastest" model (gpt-4o-mini)
completion = client.chat.completions.create(
  model="fastest",  ## This value matches our conditional routing condition
  messages=[
    {"role": "developer", "content": "You are a helpful assistant."},
    {"role": "user", "content": "What's 2+2?"}
  ]
)

```

##### Metadata Parameter Based Routing
```python
from portkey_ai import Portkey

client = Portkey(
  api_key="u6**************Vz", ## which is configured in control plane
  provider="@azure-openai-provider"， ## which is configured in control plane
  config={
    "strategy": {
      "mode": "conditional",
      "conditions": [
        {
          "query": { "metadata.data_sensitivity": { "$eq": "high" } },
          "then": "on-premises-model"
        },
        {
          "query": { "metadata.data_sensitivity": { "$in": ["medium", "low"] } },
          "then": "cloud-model"
        }
      ],
      "default": "public-model"
    },
    "targets": [
      {
        "name": "public-model", "provider":"@openai-vk" },
      {
        "name": "on-premises-model", "provider":"@private-vk" },
      {
        "name": "cloud-model", "provider":"@azure-vk" }
    ]
  }, ## Simple config with metadata based routing
)

## Option 1
## This will use the "on-premises-model" model (@private-vk)
response = portkey.with_options(
  metadata = {
    "data_sensitivity": "high",
  }
).chat.completions.create(
  messages = [{ "role": 'user', "content": 'What is 1729' }]
)

## Option 2
## This will use the "cloud-model" model (@azure-vk)
response = portkey.with_options(
  metadata = {
    "data_sensitivity": "medium", ## or "low"
  }
).chat.completions.create(
  messages = [{ "role": 'user', "content": 'What is 1729' }]
)

## Option 3
## This will use the "public-model" model (@openai-vk)
response = portkey.with_options(
  metadata = {
    "data_sensitivity": "NA", ## or any other string 
  }
).chat.completions.create(
  messages = [{ "role": 'user', "content": 'What is 1729' }]
)

```


##### example for combined conditions
```python
from portkey_ai import Portkey

client = Portkey(
  api_key="u6**************Vz", ## which is configured in control plane
  provider="@azure-openai-provider"， ## which is configured in control plane
  config={
    "strategy": {
      "mode": "conditional",
      "conditions": [
        {
          "query": {
            "$and": [
              { "metadata.user_tier": { "$eq": "enterprise" } },
              { "params.temperature": { "$gte": 0.7 } }
            ]
          },
          "then": "creative-premium-target"
        }
      ],
      "default": "standard-target"
    },
    "targets": [
      {
        "name": "creative-premium-target",
        "provider":"@anthropic-vk",
        "override_params": { "model": "claude-3-opus" }
      },
      {
        "name": "standard-target",
        "provider":"@openai-vk",
        "override_params": { "model": "gpt-3.5-turbo" }
      }
    ]
  }
)

## Option 1
## This will use the "creative-premium-target" model (claude-3-opus)
response = portkey.with_options(
  metadata = {
    "user_tier": "enterprise",
  }
).chat.completions.create(
  messages = [{ "role": 'user', "content": 'What is 1729' }]
  temperature=0.8
)


## Option 2
## This will use the "standard-target" model (gpt-3.5-turbo)
response = portkey.with_options(
  metadata = {
    "user_tier": "enterprise",
  }
).chat.completions.create(
  messages = [{ "role": 'user', "content": 'What is 1729' }]
  temperature=0.6
)

```

For more details on intelligent routing: https://portkey.ai/docs/product/ai-gateway/conditional-routing

## Specification for /chat/completions

```yaml 
paths:
  path: /chat/completions
  method: post
  servers:
    - url: https://api.portkey.ai/v1
      description: Portkey API Public Endpoint
    - url: SELF_HOSTED_GATEWAY_URL
      description: Self-Hosted Gateway URL
  request:
    security:
      - title: Portkey Key & Virtual Key
        parameters:
          query: {}
          header:
            x-portkey-api-key:
              type: apiKey
            x-portkey-virtual-key:
              type: apiKey
          cookie: {}
      - title: Portkey Key & Provider Auth & Provider Name
        parameters:
          query: {}
          header:
            x-portkey-api-key:
              type: apiKey
            Authorization:
              type: http
              scheme: bearer
            x-portkey-provider:
              type: apiKey
          cookie: {}
      - title: Portkey Key & Config
        parameters:
          query: {}
          header:
            x-portkey-api-key:
              type: apiKey
            x-portkey-config:
              type: apiKey
          cookie: {}
      - title: Portkey Key & Provider Auth & Provider Name & Custom Host
        parameters:
          query: {}
          header:
            x-portkey-api-key:
              type: apiKey
            Authorization:
              type: http
              scheme: bearer
            x-portkey-provider:
              type: apiKey
            x-portkey-custom-host:
              type: apiKey
          cookie: {}
    parameters:
      path: {}
      query: {}
      header:
        x-portkey-trace-id:
          schema:
            - type: string
              required: false
              description: >-
                An ID you can pass to refer to one or more requests later on. If
                not provided, Portkey generates a trace ID automatically for
                each request.
                [Docs](https://portkey.ai/docs/product/observability/traces)
        x-portkey-span-id:
          schema:
            - type: string
              required: false
              description: An ID you can pass to refer to a span under a trace.
        x-portkey-parent-span-id:
          schema:
            - type: string
              required: false
              description: Link a child span to a parent span
        x-portkey-span-name:
          schema:
            - type: string
              required: false
              description: Name for the Span ID
        x-portkey-metadata:
          schema:
            - type: object
              properties: {}
              required: false
              description: Pass any arbitrary metadata along with your request
        x-portkey-cache-namespace:
          schema:
            - type: string
              description: >-
                Partition your Portkey cache store based on custom strings,
                ignoring metadata and other headers
        x-portkey-cache-force-refresh:
          schema:
            - type: boolean
              description: >-
                Forces a cache refresh for your request by making a new API call
                and storing the updated value
      cookie: {}
    body:
      application/json:
        schemaArray:
          - type: object
            properties:
              messages:
                allOf:
                  - description: >-
                      A list of messages comprising the conversation so far.
                      [Example Python
                      code](https://cookbook.openai.com/examples/how_to_format_inputs_to_chatgpt_models).
                    type: array
                    minItems: 1
                    items:
                      $ref: '#/components/schemas/ChatCompletionRequestMessage'
              model:
                allOf:
                  - description: >-
                      ID of the model to use. See the [model endpoint
                      compatibility](https://platform.openai.com/docs/models/model-endpoint-compatibility)
                      table for details on which models work with the Chat API.
                    example: gpt-4-turbo
                    anyOf:
                      - type: string
                      - type: string
                        enum:
                          - gpt-4o
                          - gpt-4o-2024-05-13
                          - gpt-4-turbo
                          - gpt-4-turbo-2024-04-09
                          - gpt-4-0125-preview
                          - gpt-4-turbo-preview
                          - gpt-4-1106-preview
                          - gpt-4-vision-preview
                          - gpt-4
                          - gpt-4-0314
                          - gpt-4-0613
                          - gpt-4-32k
                          - gpt-4-32k-0314
                          - gpt-4-32k-0613
                          - gpt-3.5-turbo
                          - gpt-3.5-turbo-16k
                          - gpt-3.5-turbo-0301
                          - gpt-3.5-turbo-0613
                          - gpt-3.5-turbo-1106
                          - gpt-3.5-turbo-0125
                          - gpt-3.5-turbo-16k-0613
                    x-oaiTypeLabel: string
              frequency_penalty:
                allOf:
                  - type: number
                    default: 0
                    minimum: -2
                    maximum: 2
                    nullable: true
                    description: >
                      Number between -2.0 and 2.0. Positive values penalize new
                      tokens based on their existing frequency in the text so
                      far, decreasing the model's likelihood to repeat the same
                      line verbatim.


                      [See more information about frequency and presence
                      penalties.](https://platform.openai.com/docs/guides/text-generation/parameter-details)
              logit_bias:
                allOf:
                  - type: object
                    x-oaiTypeLabel: map
                    default: null
                    nullable: true
                    additionalProperties:
                      type: integer
                    description: >
                      Modify the likelihood of specified tokens appearing in the
                      completion.


                      Accepts a JSON object that maps tokens (specified by their
                      token ID in the tokenizer) to an associated bias value
                      from -100 to 100. Mathematically, the bias is added to the
                      logits generated by the model prior to sampling. The exact
                      effect will vary per model, but values between -1 and 1
                      should decrease or increase likelihood of selection;
                      values like -100 or 100 should result in a ban or
                      exclusive selection of the relevant token.
              logprobs:
                allOf:
                  - description: >-
                      Whether to return log probabilities of the output tokens
                      or not. If true, returns the log probabilities of each
                      output token returned in the `content` of `message`.
                    type: boolean
                    default: false
                    nullable: true
              top_logprobs:
                allOf:
                  - description: >-
                      An integer between 0 and 20 specifying the number of most
                      likely tokens to return at each token position, each with
                      an associated log probability. `logprobs` must be set to
                      `true` if this parameter is used.
                    type: integer
                    minimum: 0
                    maximum: 20
                    nullable: true
              max_tokens:
                allOf:
                  - description: >
                      The maximum number of
                      [tokens](https://platform.openai.com/tokenizer?view=bpe)
                      that can be generated in the chat completion.


                      The total length of input tokens and generated tokens is
                      limited by the model's context length. [Example Python
                      code](https://cookbook.openai.com/examples/how_to_count_tokens_with_tiktoken)
                      for counting tokens.
                    type: integer
                    nullable: true
              'n':
                allOf:
                  - type: integer
                    minimum: 1
                    maximum: 128
                    default: 1
                    example: 1
                    nullable: true
                    description: >-
                      How many chat completion choices to generate for each
                      input message. Note that you will be charged based on the
                      number of generated tokens across all of the choices. Keep
                      `n` as `1` to minimize costs.
              presence_penalty:
                allOf:
                  - type: number
                    default: 0
                    minimum: -2
                    maximum: 2
                    nullable: true
                    description: >
                      Number between -2.0 and 2.0. Positive values penalize new
                      tokens based on whether they appear in the text so far,
                      increasing the model's likelihood to talk about new
                      topics.


                      [See more information about frequency and presence
                      penalties.](https://platform.openai.com/docs/guides/text-generation/parameter-details)
              response_format:
                allOf:
                  - type: object
                    description: >
                      An object specifying the format that the model must
                      output.


                      Setting to `{ "type": "json_schema", "json_schema": {...}
                      }`enables Structured Outputs which ensures the model will
                      match your

                      supplied JSON schema. Works across all the providers that
                      support this functionality. [OpenAI & Azure
                      OpenAI](/integrations/llms/openai/structured-outputs),
                      [Gemini & Vertex
                      AI](/integrations/llms/vertex-ai/controlled-generations).


                      Setting to `{ "type": "json_object" }` enables the older
                      JSON mode, which ensures the message the model generates
                      is valid JSON.


                      Using `json_schema` is preferred for models that support
                      it.
                    oneOf:
                      - $ref: '#/components/schemas/ResponseFormatText'
                      - $ref: '#/components/schemas/ResponseFormatJsonSchema'
                      - $ref: '#/components/schemas/ResponseFormatJsonObject'
              seed:
                allOf:
                  - type: integer
                    minimum: -9223372036854776000
                    maximum: 9223372036854776000
                    nullable: true
                    description: >
                      This feature is in Beta.

                      If specified, our system will make a best effort to sample
                      deterministically, such that repeated requests with the
                      same `seed` and parameters should return the same result.

                      Determinism is not guaranteed, and you should refer to the
                      `system_fingerprint` response parameter to monitor changes
                      in the backend.
                    x-code-samples:
                      beta: true
              stop:
                allOf:
                  - description: >
                      Up to 4 sequences where the API will stop generating
                      further tokens.
                    default: null
                    oneOf:
                      - type: string
                        nullable: true
                      - type: array
                        minItems: 1
                        maxItems: 4
                        items:
                          type: string
              stream:
                allOf:
                  - description: >
                      If set, partial message deltas will be sent, like in
                      ChatGPT. Tokens will be sent as data-only [server-sent
                      events](https://developer.mozilla.org/en-UShttps://platform.openai.com/docs/Web/API/Server-sent_events/Using_server-sent_events#Event_stream_format)
                      as they become available, with the stream terminated by a
                      `data: [DONE]` message. [Example Python
                      code](https://cookbook.openai.com/examples/how_to_stream_completions).
                    type: boolean
                    nullable: true
                    default: false
              stream_options:
                allOf:
                  - $ref: '#/components/schemas/ChatCompletionStreamOptions'
              thinking:
                allOf:
                  - type: object
                    nullable: true
                    description: >
                      View the thinking/reasoning tokens as part of your
                      response. Thinking models produce a long internal chain of
                      thought before generating a response. Supported only for
                      specific Claude models on Anthropic, Google Vertex AI, and
                      AWS Bedrock.  Requires setting `strict_openai_compliance =
                      false` in your API call.
                    properties:
                      type:
                        type: string
                        enum:
                          - enabled
                          - disabled
                        description: Enables or disables the thinking mode capability.
                        default: disabled
                      budget_tokens:
                        type: integer
                        description: >
                          The maximum number of tokens to allocate for the
                          thinking process.

                          A higher token budget allows for more thorough
                          reasoning but may increase overall response time.
                        minimum: 1
                        example: 2030
                    required:
                      - type
                    example:
                      type: enabled
                      budget_tokens: 2030
              temperature:
                allOf:
                  - type: number
                    minimum: 0
                    maximum: 2
                    default: 1
                    example: 1
                    nullable: true
                    description: >
                      What sampling temperature to use, between 0 and 2. Higher
                      values like 0.8 will make the output more random, while
                      lower values like 0.2 will make it more focused and
                      deterministic.


                      We generally recommend altering this or `top_p` but not
                      both.
              top_p:
                allOf:
                  - type: number
                    minimum: 0
                    maximum: 1
                    default: 1
                    example: 1
                    nullable: true
                    description: >
                      An alternative to sampling with temperature, called
                      nucleus sampling, where the model considers the results of
                      the tokens with top_p probability mass. So 0.1 means only
                      the tokens comprising the top 10% probability mass are
                      considered.


                      We generally recommend altering this or `temperature` but
                      not both.
              tools:
                allOf:
                  - type: array
                    description: >
                      A list of tools the model may call. Currently, only
                      functions are supported as a tool. Use this to provide a
                      list of functions the model may generate JSON inputs for.
                      A max of 128 functions are supported.
                    items:
                      $ref: '#/components/schemas/ChatCompletionTool'
              tool_choice:
                allOf:
                  - $ref: '#/components/schemas/ChatCompletionToolChoiceOption'
              parallel_tool_calls:
                allOf:
                  - $ref: '#/components/schemas/ParallelToolCalls'
              user:
                allOf:
                  - type: string
                    example: user-1234
                    description: >
                      A unique identifier representing your end-user, which can
                      help OpenAI to monitor and detect abuse. [Learn
                      more](https://platform.openai.com/docs/guides/safety-best-practices/end-user-ids).
              function_call:
                allOf:
                  - deprecated: true
                    description: >
                      Deprecated in favor of `tool_choice`.


                      Controls which (if any) function is called by the model.

                      `none` means the model will not call a function and
                      instead generates a message.

                      `auto` means the model can pick between generating a
                      message or calling a function.

                      Specifying a particular function via `{"name":
                      "my_function"}` forces the model to call that function.


                      `none` is the default when no functions are present.
                      `auto` is the default if functions are present.
                    oneOf:
                      - type: string
                        description: >
                          `none` means the model will not call a function and
                          instead generates a message. `auto` means the model
                          can pick between generating a message or calling a
                          function.
                        enum:
                          - none
                          - auto
                      - $ref: '#/components/schemas/ChatCompletionFunctionCallOption'
                    x-oaiExpandable: true
              functions:
                allOf:
                  - deprecated: true
                    description: >
                      Deprecated in favor of `tools`.


                      A list of functions the model may generate JSON inputs
                      for.
                    type: array
                    minItems: 1
                    maxItems: 128
                    items:
                      $ref: '#/components/schemas/ChatCompletionFunctions'
            required: true
            refIdentifier: '#/components/schemas/CreateChatCompletionRequest'
            requiredProperties:
              - model
              - messages
        examples:
          example:
            value:
              messages:
                - content: <string>
                  role: system
                  name: <string>
              model: gpt-4-turbo
              frequency_penalty: 0
              logit_bias: null
              logprobs: false
              top_logprobs: 10
              max_tokens: 123
              'n': 1
              presence_penalty: 0
              response_format:
                type: text
              seed: 0
              stop: <string>
              stream: false
              stream_options: null
              thinking:
                type: enabled
                budget_tokens: 2030
              temperature: 1
              top_p: 1
              tools:
                - type: function
                  function:
                    description: <string>
                    name: <string>
                    parameters: {}
                    strict: false
              tool_choice: none
              parallel_tool_calls: true
              user: user-1234
              function_call: none
              functions:
                - description: <string>
                  name: <string>
                  parameters: {}
    codeSamples:
      - label: Default
        lang: cURL
        source: |
          curl https://api.portkey.ai/v1/chat/completions \
            -H "Content-Type: application/json" \
            -H "x-portkey-api-key: $PORTKEY_API_KEY" \
            -H "x-portkey-virtual-key: $PORTKEY_PROVIDER_VIRTUAL_KEY" \
            -d '{
              "model": "gpt-4o",
              "messages": [
                {
                  "role": "system",
                  "content": "You are a helpful assistant."
                },
                {
                  "role": "user",
                  "content": "Hello!"
                }
              ]
            }'
      - label: Self-Hosted
        lang: cURL
        source: |
          curl SELF_HOSTED_GATEWAY_URL/chat/completions \
            -H "Content-Type: application/json" \
            -H "x-portkey-api-key: $PORTKEY_API_KEY" \
            -H "x-portkey-virtual-key: $PORTKEY_PROVIDER_VIRTUAL_KEY" \
            -d '{
              "model": "gpt-4o",
              "messages": [
                {
                  "role": "system",
                  "content": "You are a helpful assistant."
                },
                {
                  "role": "user",
                  "content": "Hello!"
                }
              ]
            }'
      - label: Default
        lang: python
        source: |
          from portkey_ai import Portkey

          portkey = Portkey(
            api_key = "PORTKEY_API_KEY",
            virtual_key = "PROVIDER_VIRTUAL_KEY"
          )

          response = portkey.chat.completions.create(
            model="gpt-4o",
            messages=[
              {"role": "system", "content": "You are a helpful assistant."},
              {"role": "user", "content": "Hello!"}
            ]
          )

          print(response.choices[0].message)
      - label: Self-Hosted
        lang: python
        source: |
          from portkey_ai import Portkey

          portkey = Portkey(
            api_key = "PORTKEY_API_KEY",
            base_url = "SELF_HOSTED_GATEWAY_URL",
            virtual_key = "PROVIDER_VIRTUAL_KEY"
          )

          response = portkey.chat.completions.create(
            model="gpt-4o",
            messages=[
              {"role": "system", "content": "You are a helpful assistant."},
              {"role": "user", "content": "Hello!"}
            ]
          )

          print(response.choices[0].message)
      - label: Default
        lang: javascript
        source: |
          import Portkey from 'portkey-ai';

          const portkey = new Portkey({
            apiKey: 'PORTKEY_API_KEY',
            virtualKey: 'PROVIDER_VIRTUAL_KEY'
          });

          async function main() {
            const response = await portkey.chat.completions.create({
              messages: [{ role: "system", content: "You are a helpful assistant." }],
              model: "gpt-4o",
            });

            console.log(response.choices[0]);
          }

          main();
      - label: Self-Hosted
        lang: javascript
        source: |
          import Portkey from 'portkey-ai';

          const portkey = new Portkey({
            apiKey: 'PORTKEY_API_KEY',
            virtualKey: 'PROVIDER_VIRTUAL_KEY',
            baseUrl: 'SELF_HOSTED_GATEWAY_URL'
          });

          async function main() {
            const response = await portkey.chat.completions.create({
              messages: [{ role: "system", content: "You are a helpful assistant." }],
              model: "gpt-4o",
            });

            console.log(response.choices[0]);
          }

          main();
  response:
    '200':
      application/json:
        schemaArray:
          - type: object
            properties:
              id:
                allOf:
                  - type: string
                    description: A unique identifier for the chat completion.
              choices:
                allOf:
                  - type: array
                    description: >-
                      A list of chat completion choices. Can be more than one if
                      `n` is greater than 1.
                    items:
                      type: object
                      required:
                        - finish_reason
                        - index
                        - message
                        - logprobs
                      properties:
                        finish_reason:
                          type: string
                          description: >
                            The reason the model stopped generating tokens. This
                            will be `stop` if the model hit a natural stop point
                            or a provided stop sequence,

                            `length` if the maximum number of tokens specified
                            in the request was reached,

                            `content_filter` if content was omitted due to a
                            flag from our content filters,

                            `tool_calls` if the model called a tool, or
                            `function_call` (deprecated) if the model called a
                            function.
                          enum:
                            - stop
                            - length
                            - tool_calls
                            - content_filter
                            - function_call
                        index:
                          type: integer
                          description: The index of the choice in the list of choices.
                        message:
                          $ref: '#/components/schemas/ChatCompletionResponseMessage'
                        logprobs:
                          description: Log probability information for the choice.
                          type: object
                          nullable: true
                          properties:
                            content:
                              description: >-
                                A list of message content tokens with log
                                probability information.
                              type: array
                              items:
                                $ref: >-
                                  #/components/schemas/ChatCompletionTokenLogprob
                              nullable: true
                          required:
                            - content
              created:
                allOf:
                  - type: integer
                    description: >-
                      The Unix timestamp (in seconds) of when the chat
                      completion was created.
              model:
                allOf:
                  - type: string
                    description: The model used for the chat completion.
              system_fingerprint:
                allOf:
                  - type: string
                    description: >
                      This fingerprint represents the backend configuration that
                      the model runs with.


                      Can be used in conjunction with the `seed` request
                      parameter to understand when backend changes have been
                      made that might impact determinism.
              object:
                allOf:
                  - type: string
                    description: The object type, which is always `chat.completion`.
                    enum:
                      - chat.completion
              usage:
                allOf:
                  - $ref: '#/components/schemas/CompletionUsage'
            description: >-
              Represents a chat completion response returned by model, based on
              the provided input.
            refIdentifier: '#/components/schemas/CreateChatCompletionResponse'
            requiredProperties:
              - choices
              - created
              - id
              - model
              - object
        examples:
          example:
            value:
              id: <string>
              choices:
                - finish_reason: stop
                  index: 123
                  message:
                    content: <string>
                    tool_calls:
                      - id: <string>
                        type: function
                        function:
                          name: <string>
                          arguments: <string>
                    role: assistant
                    function_call:
                      arguments: <string>
                      name: <string>
                    content_blocks:
                      - type: text
                        text: <string>
                  logprobs:
                    content:
                      - token: <string>
                        logprob: 123
                        bytes:
                          - 123
                        top_logprobs:
                          - token: <string>
                            logprob: 123
                            bytes:
                              - 123
              created: 123
              model: <string>
              system_fingerprint: <string>
              object: chat.completion
              usage:
                completion_tokens: 123
                prompt_tokens: 123
                total_tokens: 123
        description: OK
  deprecated: false
  type: path
components:
  schemas:
    ChatCompletionRequestMessageContentPart:
      oneOf:
        - $ref: '#/components/schemas/ChatCompletionRequestMessageContentPartText'
        - $ref: '#/components/schemas/ChatCompletionRequestMessageContentPartImage'
      x-oaiExpandable: true
    ChatCompletionRequestMessageContentPartImage:
      type: object
      title: Image content part
      properties:
        type:
          type: string
          enum:
            - image_url
          description: The type of the content part.
        image_url:
          type: object
          properties:
            url:
              type: string
              description: Either a URL of the image or the base64 encoded image data.
              format: uri
            detail:
              type: string
              description: >-
                Specifies the detail level of the image. Learn more in the
                [Vision
                guide](https://platform.openai.com/docs/guides/vision/low-or-high-fidelity-image-understanding).
              enum:
                - auto
                - low
                - high
              default: auto
          required:
            - url
      required:
        - type
        - image_url
    ChatCompletionRequestMessageContentPartText:
      type: object
      title: Text content part
      properties:
        type:
          type: string
          enum:
            - text
          description: The type of the content part.
        text:
          type: string
          description: The text content.
      required:
        - type
        - text
    ChatCompletionMessageContentPartThinking:
      type: object
      title: Thinking content part
      properties:
        type:
          type: string
          enum:
            - thinking
          description: The type of the content part.
        thinking:
          type: string
          description: The thinking content.
      required:
        - type
        - thinking
    ChatCompletionMessageContentPartRedactedThinking:
      type: object
      title: Redacted thinking content part
      properties:
        type:
          type: string
          enum:
            - redacted_thinking
          description: The type of the content part.
        data:
          type: string
          description: The redacted thinking content.
      required:
        - type
        - data
    ChatCompletionRequestMessage:
      oneOf:
        - $ref: '#/components/schemas/ChatCompletionRequestSystemMessage'
        - $ref: '#/components/schemas/ChatCompletionRequestDeveloperMessage'
        - $ref: '#/components/schemas/ChatCompletionRequestUserMessage'
        - $ref: '#/components/schemas/ChatCompletionRequestAssistantMessage'
        - $ref: '#/components/schemas/ChatCompletionRequestToolMessage'
        - $ref: '#/components/schemas/ChatCompletionRequestFunctionMessage'
      x-oaiExpandable: true
    ChatCompletionRequestSystemMessage:
      type: object
      title: System message
      properties:
        content:
          description: The contents of the system message.
          type: string
        role:
          type: string
          enum:
            - system
          description: The role of the messages author, in this case `system`.
        name:
          type: string
          description: >-
            An optional name for the participant. Provides the model information
            to differentiate between participants of the same role.
      required:
        - content
        - role
    ChatCompletionRequestDeveloperMessage:
      type: object
      title: Developer message
      description: >-
        New role by OpenAI for select models. Must be explicitly used for models
        that support it. When used with incompatible models or providers,
        Portkey automatically converts it to a system role.
      properties:
        content:
          description: The contents of the Developer message.
          type: string
        role:
          type: string
          enum:
            - developer
          description: The role of the messages author, in this case `Developer`.
        name:
          type: string
          description: >-
            An optional name for the participant. Provides the model information
            to differentiate between participants of the same role.
      required:
        - content
        - role
    ChatCompletionRequestUserMessage:
      type: object
      title: User message
      properties:
        content:
          description: |
            The contents of the user message.
          oneOf:
            - type: string
              description: The text contents of the message.
              title: Text content
            - type: array
              description: >-
                An array of content parts with a defined type, each can be of
                type `text` or `image_url` when passing in images. You can pass
                multiple images by adding multiple `image_url` content parts.
                Image input is only supported when using the
                `gpt-4-visual-preview` model.
              title: Array of content parts
              items:
                $ref: '#/components/schemas/ChatCompletionRequestMessageContentPart'
              minItems: 1
          x-oaiExpandable: true
        role:
          type: string
          enum:
            - user
          description: The role of the messages author, in this case `user`.
        name:
          type: string
          description: >-
            An optional name for the participant. Provides the model information
            to differentiate between participants of the same role.
      required:
        - content
        - role
    ChatCompletionRequestAssistantMessage:
      type: object
      title: Assistant message
      properties:
        content:
          nullable: true
          type: string
          description: >
            The contents of the assistant message. Required unless `tool_calls`
            or `function_call` is specified.
        role:
          type: string
          enum:
            - assistant
          description: The role of the messages author, in this case `assistant`.
        name:
          type: string
          description: >-
            An optional name for the participant. Provides the model information
            to differentiate between participants of the same role.
        tool_calls:
          $ref: '#/components/schemas/ChatCompletionMessageToolCalls'
        function_call:
          type: object
          deprecated: true
          description: >-
            Deprecated and replaced by `tool_calls`. The name and arguments of a
            function that should be called, as generated by the model.
          nullable: true
          properties:
            arguments:
              type: string
              description: >-
                The arguments to call the function with, as generated by the
                model in JSON format. Note that the model does not always
                generate valid JSON, and may hallucinate parameters not defined
                by your function schema. Validate the arguments in your code
                before calling your function.
            name:
              type: string
              description: The name of the function to call.
          required:
            - arguments
            - name
      required:
        - role
    ChatCompletionRequestToolMessage:
      type: object
      title: Tool message
      properties:
        role:
          type: string
          enum:
            - tool
          description: The role of the messages author, in this case `tool`.
        content:
          type: string
          description: The contents of the tool message.
        tool_call_id:
          type: string
          description: Tool call that this message is responding to.
      required:
        - role
        - content
        - tool_call_id
    ChatCompletionRequestFunctionMessage:
      type: object
      title: Function message
      deprecated: true
      properties:
        role:
          type: string
          enum:
            - function
          description: The role of the messages author, in this case `function`.
        content:
          nullable: true
          type: string
          description: The contents of the function message.
        name:
          type: string
          description: The name of the function to call.
      required:
        - role
        - content
        - name
    FunctionParameters:
      type: object
      description: >-
        The parameters the functions accepts, described as a JSON Schema object.
        See the
        [guide](https://platform.openai.com/docs/guides/function-calling) for
        examples, and the [JSON Schema
        reference](https://json-schema.org/understanding-json-schema/) for
        documentation about the format. 


        Omitting `parameters` defines a function with an empty parameter list.
      additionalProperties: true
    ChatCompletionFunctions:
      type: object
      deprecated: true
      properties:
        description:
          type: string
          description: >-
            A description of what the function does, used by the model to choose
            when and how to call the function.
        name:
          type: string
          description: >-
            The name of the function to be called. Must be a-z, A-Z, 0-9, or
            contain underscores and dashes, with a maximum length of 64.
        parameters:
          $ref: '#/components/schemas/FunctionParameters'
      required:
        - name
    ChatCompletionFunctionCallOption:
      type: object
      description: >
        Specifying a particular function via `{"name": "my_function"}` forces
        the model to call that function.
      properties:
        name:
          type: string
          description: The name of the function to call.
      required:
        - name
    ChatCompletionTool:
      type: object
      properties:
        type:
          type: string
          enum:
            - function
          description: The type of the tool. Currently, only `function` is supported.
        function:
          $ref: '#/components/schemas/FunctionObject'
      required:
        - type
        - function
    ChatCompletionToolChoiceOption:
      description: >
        Controls which (if any) tool is called by the model.

        `none` means the model will not call any tool and instead generates a
        message.

        `auto` means the model can pick between generating a message or calling
        one or more tools.

        `required` means the model must call one or more tools.

        Specifying a particular tool via `{"type": "function", "function":
        {"name": "my_function"}}` forces the model to call that tool.


        `none` is the default when no tools are present. `auto` is the default
        if tools are present.
      oneOf:
        - type: string
          description: >
            `none` means the model will not call any tool and instead generates
            a message. `auto` means the model can pick between generating a
            message or calling one or more tools. `required` means the model
            must call one or more tools.
          enum:
            - none
            - auto
            - required
        - $ref: '#/components/schemas/ChatCompletionNamedToolChoice'
      x-oaiExpandable: true
    ChatCompletionNamedToolChoice:
      type: object
      description: >-
        Specifies a tool the model should use. Use to force the model to call a
        specific function.
      properties:
        type:
          type: string
          enum:
            - function
          description: The type of the tool. Currently, only `function` is supported.
        function:
          type: object
          properties:
            name:
              type: string
              description: The name of the function to call.
          required:
            - name
      required:
        - type
        - function
    ParallelToolCalls:
      description: >-
        Whether to enable [parallel function
        calling](https://platform.openai.com/docs/guides/function-calling/parallel-function-calling)
        during tool use.
      type: boolean
      default: true
    ChatCompletionMessageToolCalls:
      type: array
      description: The tool calls generated by the model, such as function calls.
      items:
        $ref: '#/components/schemas/ChatCompletionMessageToolCall'
    ChatCompletionMessageToolCall:
      type: object
      properties:
        id:
          type: string
          description: The ID of the tool call.
        type:
          type: string
          enum:
            - function
          description: The type of the tool. Currently, only `function` is supported.
        function:
          type: object
          description: The function that the model called.
          properties:
            name:
              type: string
              description: The name of the function to call.
            arguments:
              type: string
              description: >-
                The arguments to call the function with, as generated by the
                model in JSON format. Note that the model does not always
                generate valid JSON, and may hallucinate parameters not defined
                by your function schema. Validate the arguments in your code
                before calling your function.
          required:
            - name
            - arguments
      required:
        - id
        - type
        - function
    ChatCompletionStreamOptions:
      description: >
        Options for streaming response. Only set this when you set `stream:
        true`.
      type: object
      nullable: true
      default: null
      properties:
        include_usage:
          type: boolean
          description: >
            If set, an additional chunk will be streamed before the `data:
            [DONE]` message. The `usage` field on this chunk shows the token
            usage statistics for the entire request, and the `choices` field
            will always be an empty array. All other chunks will also include a
            `usage` field, but with a null value.
    ChatCompletionMessageContentBlock:
      type: object
      description: A block of content in a chat completion message.
      oneOf:
        - $ref: '#/components/schemas/ChatCompletionRequestMessageContentPartText'
        - $ref: '#/components/schemas/ChatCompletionMessageContentPartThinking'
        - $ref: >-
            #/components/schemas/ChatCompletionMessageContentPartRedactedThinking
    ChatCompletionResponseMessage:
      type: object
      description: A chat completion message generated by the model.
      properties:
        content:
          type: string
          description: The contents of the message.
          nullable: true
        tool_calls:
          $ref: '#/components/schemas/ChatCompletionMessageToolCalls'
        role:
          type: string
          enum:
            - assistant
          description: The role of the author of this message.
        function_call:
          type: object
          deprecated: true
          description: >-
            Deprecated and replaced by `tool_calls`. The name and arguments of a
            function that should be called, as generated by the model.
          properties:
            arguments:
              type: string
              description: >-
                The arguments to call the function with, as generated by the
                model in JSON format. Note that the model does not always
                generate valid JSON, and may hallucinate parameters not defined
                by your function schema. Validate the arguments in your code
                before calling your function.
            name:
              type: string
              description: The name of the function to call.
          required:
            - name
            - arguments
        content_blocks:
          nullable: true
          type: array
          description: >-
            The content blocks of the message. This is only present for certain
            providers with strict-open-ai-compliance flag set to false
          items:
            type: object
            $ref: '#/components/schemas/ChatCompletionMessageContentBlock'
      required:
        - role
        - content
    ChatCompletionTokenLogprob:
      type: object
      properties:
        token:
          description: The token.
          type: string
        logprob:
          description: >-
            The log probability of this token, if it is within the top 20 most
            likely tokens. Otherwise, the value `-9999.0` is used to signify
            that the token is very unlikely.
          type: number
        bytes:
          description: >-
            A list of integers representing the UTF-8 bytes representation of
            the token. Useful in instances where characters are represented by
            multiple tokens and their byte representations must be combined to
            generate the correct text representation. Can be `null` if there is
            no bytes representation for the token.
          type: array
          items:
            type: integer
          nullable: true
        top_logprobs:
          description: >-
            List of the most likely tokens and their log probability, at this
            token position. In rare cases, there may be fewer than the number of
            requested `top_logprobs` returned.
          type: array
          items:
            type: object
            properties:
              token:
                description: The token.
                type: string
              logprob:
                description: >-
                  The log probability of this token, if it is within the top 20
                  most likely tokens. Otherwise, the value `-9999.0` is used to
                  signify that the token is very unlikely.
                type: number
              bytes:
                description: >-
                  A list of integers representing the UTF-8 bytes representation
                  of the token. Useful in instances where characters are
                  represented by multiple tokens and their byte representations
                  must be combined to generate the correct text representation.
                  Can be `null` if there is no bytes representation for the
                  token.
                type: array
                items:
                  type: integer
                nullable: true
            required:
              - token
              - logprob
              - bytes
      required:
        - token
        - logprob
        - bytes
        - top_logprobs
    FunctionObject:
      type: object
      properties:
        description:
          type: string
          description: >-
            A description of what the function does, used by the model to choose
            when and how to call the function.
        name:
          type: string
          description: >-
            The name of the function to be called. Must be a-z, A-Z, 0-9, or
            contain underscores and dashes, with a maximum length of 64.
        parameters:
          $ref: '#/components/schemas/FunctionParameters'
        strict:
          type: boolean
          nullable: true
          default: false
          description: >-
            Whether to enable strict schema adherence when generating the
            function call. If set to true, the model will follow the exact
            schema defined in the `parameters` field. Only a subset of JSON
            Schema is supported when `strict` is `true`. Learn more about
            Structured Outputs in the [function calling
            guide](docs/guides/function-calling).
      required:
        - name
    CompletionUsage:
      type: object
      description: Usage statistics for the completion request.
      properties:
        completion_tokens:
          type: integer
          description: Number of tokens in the generated completion.
        prompt_tokens:
          type: integer
          description: Number of tokens in the prompt.
        total_tokens:
          type: integer
          description: Total number of tokens used in the request (prompt + completion).
      required:
        - prompt_tokens
        - completion_tokens
        - total_tokens
    ResponseFormatJsonObject:
      type: object
      title: JSON object
      description: >
        JSON object response format. An older method of generating JSON
        responses.

        Using `json_schema` is recommended for models that support it. Note that
        the

        model will not generate JSON without a system or user message
        instructing it

        to do so.
      properties:
        type:
          type: string
          description: The type of response format being defined. Always `json_object`.
          enum:
            - json_object
          x-stainless-const: true
      required:
        - type
    ResponseFormatJsonSchema:
      type: object
      title: JSON schema
      description: |
        JSON Schema response format. Used to generate structured JSON responses.
        Learn more about [Structured Outputs](/docs/guides/structured-outputs).
      properties:
        type:
          type: string
          description: The type of response format being defined. Always `json_schema`.
          enum:
            - json_schema
          x-stainless-const: true
        json_schema:
          type: object
          title: JSON schema
          description: |
            Structured Outputs configuration options, including a JSON Schema.
          properties:
            description:
              type: string
              description: >
                A description of what the response format is for, used by the
                model to

                determine how to respond in the format.
            name:
              type: string
              description: >
                The name of the response format. Must be a-z, A-Z, 0-9, or
                contain

                underscores and dashes, with a maximum length of 64.
            schema:
              $ref: '#/components/schemas/ResponseFormatJsonSchemaSchema'
            strict:
              type: boolean
              nullable: true
              default: false
              description: >
                Whether to enable strict schema adherence when generating the
                output.

                If set to true, the model will always follow the exact schema
                defined

                in the `schema` field. Only a subset of JSON Schema is supported
                when

                `strict` is `true`. To learn more, read the [Structured Outputs

                guide](/docs/guides/structured-outputs).
          required:
            - name
      required:
        - type
        - json_schema
    ResponseFormatJsonSchemaSchema:
      type: object
      title: JSON schema
      description: |
        The schema for the response format, described as a JSON Schema object.
        Learn how to build JSON schemas [here](https://json-schema.org/).
      additionalProperties: true
    ResponseFormatText:
      type: object
      title: Text
      description: |
        Default response format. Used to generate text responses.
      properties:
        type:
          type: string
          description: The type of response format being defined. Always `text`.
          enum:
            - text
          x-stainless-const: true
      required:
        - type

```
