
# rehype-clipboard-prep-code

**[rehype](https://github.com/rehypejs/rehype)** plugin designed to facilitate the attachment of raw code strings to a server-side parent container elements, allowing users to easily copy the entire code snippet to their clipboard.

## Primary Use Case

Imagine you have an MDX-based documentation or blog platform where you frequently share code snippets. Often, readers would want to copy the presented code for their use. With `rehype-clipboard-prep-code`, your code containers can carry the raw string version of the code, making the copy-to-clipboard action seamless.

### Example Configuration (`contentlayer.config.ts`)

The following is a sample configuration illustrating how you might set up your content layer along with the integration of `rehype-clipboard-prep-code`:

```typescript
import { defineDocumentType, makeSource } from 'contentlayer/source-files';
import rehypePrettyCode from 'rehype-pretty-code';
import remarkCodeTitles from 'remark-flexible-code-titles';
import {
  attachRawStringToCodeContainers,
  attachMetadataProperties,
} from './plugins/mdxPlugins';

export default makeSource({
  contentDirPath: 'content',
  contentDirExclude: ['drafts'],
  documentTypes: [Blog],
  mdx: {
    remarkPlugins: [
      [
        remarkCodeTitles,
        {
          titleTagName: 'CodeBlockTitle',
          titleClassName: 'custom-code-title',
          titleProperties: (language, title) => ({
            ['data-language']: language,
            title,
          }),
        },
      ],
    ],
    rehypePlugins: [
      attachRawStringToCodeContainers,
      [
        rehypePrettyCode,
        {
          theme: 'github-dark',
          },
        },
      ],
      attachMetadataProperties,
    ],
  },
});
```


- **MDX Configuration**: The MDX setup incorporates various plugins to refine the handling of markdown and HTML transformations:
  - [`remark-flexible-code-titles`](https://github.com/ipikuka/remark-flexible-code-titles) (a required plugin) enables flexible naming for code blocks.
  - [`rehypePrettyCode`](https://github.com/atomiks/rehype-pretty-code), for code styling and beautification.
  - [Content Layer](https://contentlayer.dev/) is the framework for which these plugins are integrated.


## Prerequisites

- Ensure you have `remark-flexible-code-titles` installed and configured as it is a necessary dependency for this package to function effectively.

## Installation

Follow these steps to get started:

1. Install the package via npm:
```bash
npm install rehype-clipboard-prep-code
```

2. Add and configure it in your MDX setup, as shown in the example above.

## Contributing

We welcome contributions! If you find an issue or have a feature request, feel free to open an issue or submit a pull request.

## License

MIT
