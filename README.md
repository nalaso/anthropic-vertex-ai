# Vercel AI SDK - Anthropic Vertex Provider

[nalaso/anthropic-vertex-ai](https://github.com/nalaso/anthropic-vertex-ai) is a community provider that uses Anthropic models through Vertex AI to provide language model support for the Vercel AI SDK.

Docs - [anthropic-vertex-ai Documentation](https://sdk.vercel.ai/providers/community-providers/anthropic-vertex-ai)

![NPM Downloads](https://img.shields.io/npm/dw/anthropic-vertex-ai?style=for-the-badge&label=anthropic-vertex-ai&link=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2Fanthropic-vertex-ai)
[![NPM Downloads](https://img.shields.io/npm/dw/anthropic-vertex-ai?style=for-the-badge&label=anthropic-vertex-ai)](https://www.npmjs.com/package/anthropic-vertex-ai){:target="_blank"}
[![NPM Downloads](https://img.shields.io/npm/dw/anthropic-vertex-ai?style=for-the-badge&label=anthropic-vertex-ai)](https://www.npmjs.com/package/anthropic-vertex-ai){:target="_blank"}

## Setup

The AnthropicVertex provider is available in the `anthropic-vertex-ai` module. You can install it with:

```bash
npm install anthropic-vertex-ai
# or
pnpm add anthropic-vertex-ai
# or
yarn add anthropic-vertex-ai
# or
bun add anthropic-vertex-ai
```

## Provider Instance

You can import the default provider instance `anthropicVertex` from `anthropic-vertex-ai`:

```ts
import { anthropicVertex } from 'anthropic-vertex-ai';
```

If you need a customized setup, you can import `createAnthropicVertex` from `anthropic-vertex-ai` and create a provider instance with your settings:

```ts
import { createAnthropicVertex } from 'anthropic-vertex-ai';

const anthropicVertex = createAnthropicVertex({
  region: 'us-central1',
  projectId: 'your-project-id',
  // other options
});
```

You can use the following optional settings to customize the AnthropicVertex provider instance:

- **region** _string_

  Your Google Vertex region. Defaults to the `GOOGLE_VERTEX_REGION` environment variable.

- **projectId** _string_

  Your Google Vertex project ID. Defaults to the `GOOGLE_VERTEX_PROJECT_ID` environment variable.

- **googleAuth** _GoogleAuth_

  Optional. The Authentication options provided by google-auth-library.

- **baseURL** _string_

  Use a different URL prefix for API calls, e.g., to use proxy servers.
  The default prefix is `https://{region}-aiplatform.googleapis.com/v1`.

- **headers** _Record&lt;string,string&gt;_

  Custom headers to include in the requests.

- **fetch** _(input: RequestInfo, init?: RequestInit) => Promise&lt;Response&gt;_

  Custom fetch implementation. You can use it as a middleware to intercept requests,
  or to provide a custom fetch implementation for e.g., testing.

## Language Models

You can create models that call the Anthropic API through Vertex AI using the provider instance.
The first argument is the model ID, e.g., `claude-3-sonnet@20240229`:

```ts
const model = anthropicVertex('claude-3-sonnet@20240229');
```

### Example: Generate Text

You can use AnthropicVertex language models to generate text with the `generateText` function:

```ts
import { anthropicVertex } from 'anthropic-vertex-ai';
import { generateText } from 'ai';

const { text } = await generateText({
  model: anthropicVertex('claude-3-sonnet@20240229'),
  prompt: 'Write a vegetarian lasagna recipe for 4 people.',
});
```

AnthropicVertex language models can also be used in the `streamText`, `generateObject`, and `streamObject` functions
(see [AI SDK Core](/docs/ai-sdk-core) for more information).

### Model Capabilities

| Model                        | Image Input         | Object Generation   | Tool Usage          | Tool Streaming      |
| ---------------------------- | ------------------- | ------------------- | ------------------- | ------------------- |
| `claude-3-5-sonnet@20240620` | :heavy_check_mark:  | :heavy_check_mark:  | :heavy_check_mark:  | :heavy_check_mark:  |
| `claude-3-opus@20240229`     | :heavy_check_mark:  | :heavy_check_mark:  | :heavy_check_mark:  | :heavy_check_mark:  |
| `claude-3-sonnet@20240229`   | :heavy_check_mark:  | :heavy_check_mark:  | :heavy_check_mark:  | :heavy_check_mark:  |
| `claude-3-haiku@20240307`    | :heavy_check_mark:  | :heavy_check_mark:  | :heavy_check_mark:  | :heavy_check_mark:  |

## Environment Variables

To use the AnthropicVertex provider, you need to set up the following environment variables:

- `GOOGLE_VERTEX_REGION`: Your Google Vertex region (e.g., 'us-central1')
- `GOOGLE_VERTEX_PROJECT_ID`: Your Google Cloud project ID

Make sure to set these variables in your environment or in a `.env` file in your project root.

## Authentication

The AnthropicVertex provider uses Google Cloud authentication. Make sure you have set up your Google Cloud credentials properly. You can either use a service account key file or default application credentials.

For more information on setting up authentication, refer to the [Google Cloud Authentication guide](https://cloud.google.com/docs/authentication).
