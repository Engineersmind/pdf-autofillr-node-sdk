[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![npm](https://img.shields.io/npm/v/pdf-autofillr)](https://www.npmjs.com/package/pdf-autofillr)
[![Platform](https://img.shields.io/badge/platform-pdffillr.ai-blue)](https://pdffillr.ai)

<div align="center">

# pdf-autofillr — Node.js SDK

**TypeScript/Node.js SDK for AI-powered PDF form filling — extract fields, map data, and fill any PDF form automatically.**

[**Quick Start**](#quick-start) · [**Python SDK**](https://github.com/EngineersMind/pdf-autofillr-python-sdk) · [**Live Platform**](https://pdffillr.ai) · [**CLI**](https://github.com/EngineersMind/pdf-autofillr-cli)

</div>

---

> **Status:** This SDK is under active development. For production use today, see the [Python SDK](https://github.com/EngineersMind/pdf-autofillr-python-sdk) or the [live platform at pdffillr.ai](https://pdffillr.ai).

## What it does

`pdf-autofillr` extracts form fields from any PDF, maps your data to those fields using an LLM of your choice, and returns a filled PDF — programmatically, at scale.

```
Blank PDF + your data
        │
        ▼
  embed (once per template)  ← extract fields → LLM map → bake metadata
        │
        ▼
  fill (per submission)      ← inject data → return filled PDF
```

## Installation

```bash
npm install pdf-autofillr
# or
yarn add pdf-autofillr
```

## Quick Start

```typescript
import { PDFAutofillr } from "pdf-autofillr";
import { readFileSync, writeFileSync } from "node:fs";

async function main() {
  const client = new PDFAutofillr({ apiKey: process.env.PDF_AUTOFILLR_API_KEY });

  // Step 1: Embed metadata into a template (once per PDF)
  const embedded = await client.embed({
    pdf: readFileSync("form.pdf"),
    schemaKeys: ["first_name", "last_name", "date_of_birth"],
  });

  // Step 2: Fill the template with data
  const filled = await client.fill({
    pdf: embedded.pdf,
    data: { first_name: "Jane", last_name: "Doe", date_of_birth: "1990-01-15" },
  });

  writeFileSync("filled_form.pdf", filled.pdf);
}

main();
```

> Requires Node.js 18+ (ESM or CJS with async/await support).

## Supported LLMs

Works with any LLM via the platform:

| Provider | Models |
|----------|--------|
| OpenAI | `gpt-4o`, `gpt-4o-mini` |
| Anthropic | `claude-3-5-haiku-latest`, `claude-3-5-sonnet-latest` |
| Google | `gemini-1.5-flash`, `gemini-1.5-pro` |
| Ollama (local) | `llama3.1`, `mistral` |

## Related

| Package | Language | Description |
|---------|----------|-------------|
| [pdf-autofillr-python-sdk](https://github.com/EngineersMind/pdf-autofillr-python-sdk) | Python | Full-featured Python SDK (stable) |
| [pdf-autofillr-cli](https://github.com/EngineersMind/pdf-autofillr-cli) | CLI | Fill PDFs from your terminal |
| [pdf-autofillr-plugins](https://github.com/EngineersMind/pdf-autofillr-plugins) | Any | Custom extractors and LLM adapters |
| [autofiller-community](https://github.com/EngineersMind/autofiller-community) | Open-source | Community models and domain packs |

## Contributing

Contributions are welcome! Open an [issue](https://github.com/EngineersMind/pdf-autofillr-node-sdk/issues) or submit a pull request.

## License

MIT — see [LICENSE](LICENSE)
