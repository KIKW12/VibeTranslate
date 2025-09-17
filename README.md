# Vibe Translate 🌈

A vibrant translation package powered by AI - translate text with good vibes!

## Features

- 🌍 Translate text between multiple languages
- 🔍 Automatic language detection
- 📦 Batch translation support
- ⚡ Multiple OpenAI model support
- 🛠️ Customizable options (temperature, model, etc.)
- 📝 TypeScript-friendly with detailed return types

## Installation

```bash
npm install vibe-translate
```

## Setup

1. Get your OpenAI API key from [OpenAI Platform](https://platform.openai.com/api-keys)
2. Set up your environment variables:

```bash
# .env file
OPENAI_API_KEY=your_openai_api_key_here
```

## Quick Start

```javascript
import AITranslator from 'vibe-translate';

const translator = new AITranslator(process.env.OPENAI_API_KEY);

// Translate text
const result = await translator.translate(
  'Hello, world!', 
  'Spanish'
);

console.log(result.translatedText); // "¡Hola, mundo!"
```

## API Reference

### Constructor

```javascript
new AITranslator(apiKey, options)
```

**Parameters:**
- `apiKey` (string): Your OpenAI API key
- `options` (object, optional):
  - `model` (string): Default model to use (default: 'gpt-3.5-turbo')
  - `temperature` (number): Default temperature (default: 0.3)

### Methods

#### `translate(text, targetLanguage, sourceLanguage, options)`

Translate text from one language to another.

**Parameters:**
- `text` (string): Text to translate
- `targetLanguage` (string): Target language (e.g., 'Spanish', 'French', 'German')
- `sourceLanguage` (string, optional): Source language (auto-detected if not provided)
- `options` (object, optional): Override default options

**Returns:** Promise resolving to translation result object

#### `translateBatch(texts, targetLanguage, sourceLanguage, options)`

Translate multiple texts at once.

**Parameters:**
- `texts` (Array<string>): Array of texts to translate
- `targetLanguage` (string): Target language
- `sourceLanguage` (string, optional): Source language
- `options` (object, optional): Override default options

**Returns:** Promise resolving to array of translation results

#### `detectLanguage(text, options)`

Detect the language of a given text.

**Parameters:**
- `text` (string): Text to analyze
- `options` (object, optional): Override default options

**Returns:** Promise resolving to language detection result

#### `getAvailableModels()`

Get list of available OpenAI models for translation.

**Returns:** Array of model names

## Usage Examples

### Basic Translation

```javascript
const result = await translator.translate(
  'How are you?', 
  'French'
);

console.log(result);
// {
//   success: true,
//   originalText: 'How are you?',
//   translatedText: 'Comment allez-vous?',
//   sourceLanguage: 'auto-detected',
//   targetLanguage: 'French',
//   model: 'gpt-3.5-turbo',
//   usage: { ... }
// }
```

### Language Detection

```javascript
const detection = await translator.detectLanguage('Bonjour le monde');

console.log(detection);
// {
//   success: true,
//   text: 'Bonjour le monde',
//   detectedLanguage: 'French',
//   confidence: 'high',
//   usage: { ... }
// }
```

### Batch Translation

```javascript
const texts = ['Hello', 'Goodbye', 'Thank you'];
const results = await translator.translateBatch(texts, 'Spanish');

results.forEach(result => {
  console.log(`${result.originalText} → ${result.translatedText}`);
});
// Hello → Hola
// Goodbye → Adiós  
// Thank you → Gracias
```

### Custom Options

```javascript
const result = await translator.translate(
  'Hello world',
  'Japanese',
  'English',
  {
    model: 'gpt-4',
    temperature: 0.1
  }
);
```

## Supported Languages

This package supports translation between any languages that OpenAI's models understand, including but not limited to:

- English, Spanish, French, German, Italian, Portuguese
- Chinese (Simplified & Traditional), Japanese, Korean
- Arabic, Russian, Hindi, Bengali
- And many more...

## Error Handling

All methods return objects with a `success` field. Check this field to handle errors:

```javascript
const result = await translator.translate('Hello', 'Spanish');

if (result.success) {
  console.log(result.translatedText);
} else {
  console.error('Translation failed:', result.error);
}
```

## Rate Limits & Costs

This package uses OpenAI's API, which has rate limits and costs associated with usage. Please refer to [OpenAI's pricing page](https://openai.com/pricing) for current rates.

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
