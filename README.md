# APIVerve Text Processing Action

> Translate text, summarize content, and paraphrase documents

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Text_Processing-blue?logo=github)](https://github.com/apiverve/action-text-processing)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**[Browse All APIs](https://apiverve.com/marketplace?utm_source=github&utm_medium=action&utm_campaign=text-processing)** | **[Get Free API Key](https://dashboard.apiverve.com/signup?utm_source=github&utm_medium=action&utm_campaign=text-processing)** | **[Documentation](https://docs.apiverve.com?utm_source=github&utm_medium=action&utm_campaign=text-processing)**

---

## What does this action do?

This action provides access to APIVerve's Text Processing APIs directly in your GitHub workflows:

- Translate text between languages
- Summarize long documents
- Paraphrase content
- Extract keywords from text

### Available APIs

| API | Description |
|-----|-------------|
| `translator` | Translator translates written text into target languages using standard language codes. Submit any string with a target language code to receive the translated text and the confirmed or auto-detected source language. |
| `textsummarizer` | Text Summarizer condenses raw text into concise summaries of a specified sentence count. Pass up to 5,000 characters to extract key points into readable summaries, with paid plans adding word counts and reduction metrics. |
| `paraphrase` | paraphrase API |
| `keywordextractor` | Keyword Extractor scans raw text or live webpage URLs to extract key terms and their frequencies. It returns up to 50 unique keywords, occurrence counts, total keyword volume, and the top five terms with their percentage share. |
| `languagedetector` | Language Detector identifies the language of any submitted text string. It returns the primary language, its ISO 639-1 code, and candidate matches ranked by confidence scores. |

---

## Quick Start

```yaml
- name: Text Processing
  uses: apiverve/action-text-processing@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: translator
    params: '{"text": "Hello world", "target": "es"}'
```

---

## Setup

### 1. Get Your API Key

Sign up for a free account at [dashboard.apiverve.com/signup](https://dashboard.apiverve.com/signup?utm_source=github&utm_medium=action&utm_campaign=text-processing) and create an API key.

### 2. Add Secret to Repository

Go to your repository **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

- Name: `APIVERVE_KEY`
- Value: Your API key from the dashboard

### 3. Use in Workflow

```yaml
- name: Text Processing
  uses: apiverve/action-text-processing@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: translator
    params: '{"your": "parameters"}'
```

---

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `api_key` | Your APIVerve API key (or set `APIVERVE_API_KEY` env var) | Yes* | - |
| `api` | API to use: `translator`, `textsummarizer`, `paraphrase`, `keywordextractor`, `languagedetector` | No | `translator` |
| `params` | JSON parameters for the API | No | `{}` |
| `output_file` | Path to save binary output (images, PDFs) | No | - |
| `format` | Response format: `json`, `yaml`, or `xml` | No | `json` |
| `fail_on_error` | Fail workflow if API returns error | No | `true` |
*\*API key is required but can be provided via input OR `APIVERVE_API_KEY` / `APIVERVE_KEY` environment variable.*

## Outputs

| Output | Description |
|--------|-------------|
| `result` | Full API response as JSON |
| `data` | The `data` field from response as JSON |
| `status` | API status (`ok` or `error`) |
| `file` | Path to downloaded file (if `output_file` was used) |
---

## Examples

### Translation

Translate text to another language

```yaml
- name: Translation
  id: text-processing-0
  uses: apiverve/action-text-processing@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: translator
    params: '{"text": "Hello world", "target": "es"}'

- name: Use result
  run: echo "Result: ${{ steps.text-processing-0.outputs.data }}"
```

### Summarization

Summarize long text

```yaml
- name: Summarization
  id: text-processing-1
  uses: apiverve/action-text-processing@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: textsummarizer
    params: '{"text": "Your long text here..."}'

- name: Use result
  run: echo "Result: ${{ steps.text-processing-1.outputs.data }}"
```


---

## Full Workflow Example

```yaml
name: Text Processing Workflow

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  text-processing:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run Text Processing
        id: result
        uses: apiverve/action-text-processing@v1
        with:
          api_key: ${{ secrets.APIVERVE_KEY }}
          api: translator
          params: '{"text": "Hello world", "target": "es"}'

      - name: Show result
        run: |
          echo "Status: ${{ steps.result.outputs.status }}"
          echo "Data: ${{ steps.result.outputs.data }}"
```

---

## Related Actions

Looking for more APIVerve actions?

- [apiverve/action](https://github.com/apiverve/action) - Generic action for all 350+ APIs
- [apiverve/action-release-assets](https://github.com/apiverve/action-release-assets) - Generate QR codes, barcodes, and badges for your GitHub releases
- [apiverve/action-visual-testing](https://github.com/apiverve/action-visual-testing) - Capture screenshots and generate PDFs for visual regression testing and documentation
- [apiverve/action-dns-monitor](https://github.com/apiverve/action-dns-monitor) - Verify DNS configuration, check propagation, and validate DNSSEC after deployments

**[Browse all APIVerve Actions →](https://github.com/marketplace?query=apiverve)**

---

## Pricing

- **Free tier** - Get started with generous free limits
- **Pro plans** - Higher rate limits and priority support for production use

Check out [pricing details](https://apiverve.com/pricing?utm_source=github&utm_medium=action&utm_campaign=text-processing).

---

## Resources

- **API Documentation**: [docs.apiverve.com](https://docs.apiverve.com?utm_source=github&utm_medium=action&utm_campaign=text-processing)
- **API Marketplace**: [apiverve.com/marketplace](https://apiverve.com/marketplace?utm_source=github&utm_medium=action&utm_campaign=text-processing)
- **Issues & Support**: [GitHub Issues](https://github.com/apiverve/action-text-processing/issues)
- **Email**: support@apiverve.com

---

## License

MIT - see [LICENSE](LICENSE)

---

Built by [APIVerve](https://apiverve.com?utm_source=github&utm_medium=action&utm_campaign=text-processing) - 350+ APIs for developers
