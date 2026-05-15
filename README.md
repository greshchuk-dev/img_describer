# ArtMatch

A playful web app that turns your description of a famous painting into an AI-generated image. Describe a masterpiece in your own words — without naming the painting or the artist — and let DALL·E recreate it.

## How it works

1. Think of a famous painting (e.g. the *Mona Lisa*, *Starry Night*, *The Scream*).
2. Type a description into the text area, avoiding the title and artist's name.
3. Hit **Create** — the app sends your prompt to OpenAI's image API and renders the result.

Example prompts:
- *"A woman with long brown hair and a faint smile, sitting in front of a hazy landscape."*
- *"A swirling night sky over a quiet village with a tall cypress tree."*
- *"A figure on a bridge clutching their face under an orange sky."*

## Project structure

```
.
├── index.html      # Markup and page layout
├── index.css       # Styles
├── index.js        # App logic + OpenAI image generation
├── .env            # Your OpenAI API key (not committed)
└── README.md       # You're reading it
```

## Getting started

This project uses [Vite](https://vitejs.dev/) for environment variable handling and module bundling.

### 1. Install dependencies

```bash
npm install
npm install openai
```

### 2. Add your OpenAI API key

Create a `.env` file in the project root:

```
VITE_OPENAI_API_KEY=sk-your-key-here
```

You can get a key from [platform.openai.com](https://platform.openai.com/api-keys). Make sure your account has credits available for image generation.

> **Important:** Add `.env` to your `.gitignore` so you don't commit your key.

### 3. Run the dev server

```bash
npm run dev
```

Then open the URL Vite prints in your terminal (usually `http://localhost:5173`).

## Configuration

Image generation settings live in `index.js` inside the `openai.images.generate()` call:

| Option | Current value | Notes |
|---|---|---|
| `model` | `dall-e-2` | Can be switched to `dall-e-3` for higher quality |
| `n` | `1` | Number of images to generate |
| `size` | `256x256` | Options: `256x256`, `512x512`, `1024x1024` (DALL·E 2) |
| `response_format` | `b64_json` | Returns base64 string instead of a URL |

## ⚠️ Security note

This app uses `dangerouslyAllowBrowser: true`, which exposes your OpenAI API key to anyone who opens the page. **This is fine for local experimentation, but never deploy it publicly as-is.** For production, route requests through a backend server that holds the key.

## Tech

- HTML5 + CSS3 ([normalize.css](https://necolas.github.io/normalize.css/))
- Vanilla JavaScript (ES modules)
- [Vite](https://vitejs.dev/) for dev server and env vars
- [OpenAI Node SDK](https://github.com/openai/openai-node) — DALL·E image generation

## Ideas for next steps

- Add a loading spinner while the image is being generated.
- Show the prompt below the generated image.
- Let users download the result.
- Add a gallery of past generations (stored in `localStorage`).
- Add a "guess the painting" mode where a friend has to identify what you described.

## License

MIT — feel free to use, modify, and share.
