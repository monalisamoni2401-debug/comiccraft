# ComicCraft - AI Comic Story Creator

ComicCraft is a FastAPI web application that turns a user story prompt into a five-panel comic.

## Features

- Gemini-powered 5-panel outline
- Gemini-powered narration and dialogue
- Stable Diffusion support
- Mock image mode for CPU/no-GPU testing
- Responsive Jinja2 frontend
- PDF export
- JSON API
- Error handling and environment-based secrets

## Project Structure

```text
ComicCraft/
├── app/
├── templates/
├── static/
├── .env.example
├── requirements.txt
├── run.py
└── README.md
```

## Windows Setup

```powershell
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
copy .env.example .env
```

Edit `.env` and add your Gemini API key.

For first testing, keep:

```env
MOCK_IMAGE_MODE=true
```

Run:

```powershell
python run.py
```

Open:

http://127.0.0.1:8000

Swagger:

http://127.0.0.1:8000/docs

## Gemini

Set:

```env
GEMINI_API_KEY=your_key_here
```

The application uses configurable model names:

```env
GEMINI_OUTLINE_MODEL=gemini-2.5-flash
GEMINI_STORY_MODEL=gemini-2.5-pro
```

If your Google account/project supports different current model IDs, update these values.

## Stable Diffusion

Set:

```env
MOCK_IMAGE_MODE=false
SD_MODEL_ID=runwayml/stable-diffusion-v1-5
```

Diffusers image generation is resource intensive. A compatible GPU is strongly recommended.

If image generation fails, ComicCraft falls back to a mock panel image so the rest of the workflow remains testable.

## API

### POST /generate

HTML form generation endpoint.

Fields:

- story_prompt
- character_name
- setting
- tone
- art_style

### POST /generate-comic/json

JSON body:

```json
{
  "story_prompt": "A brave fox explores an enchanted forest.",
  "character_name": "Luna",
  "setting": "Forest",
  "tone": "Funny",
  "art_style": "Comic Book"
}
```

### GET /test-image

Example:

`/test-image?prompt=A%20robot%20in%20space`

## Troubleshooting

### Missing Gemini API key

Add `GEMINI_API_KEY` to `.env`.

### Image generation is slow

Use `MOCK_IMAGE_MODE=true` for development, or use a GPU for Stable Diffusion.

### Gemini model unavailable

Change `GEMINI_OUTLINE_MODEL` and `GEMINI_STORY_MODEL` to model IDs currently available to your API project.

## Security

Never commit `.env`. API keys are loaded from environment variables.
