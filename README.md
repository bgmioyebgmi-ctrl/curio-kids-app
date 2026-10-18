# Curio — Kids Learning App

Curio is a browser-based, responsive kids learning app prototype. It includes:

- **Daily 10**: request a fresh set of 10 kid-friendly questions, with age and language settings.
- **Ask & Watch**: ask a question and create a short educational story made from animated scene cards, narration, captions, and source links.
- **Narration**: uses the browser's built-in speech synthesis; the learner can play/pause and mute narration.
- **Evidence corner**: lists source links alongside the answer, plus a reminder that AI answers should be checked.
- **Demo mode**: runs without an AI key, so the UI can be tried immediately. Demo answers for custom questions are explicitly labelled as a preview and are not research.
- **Configurable AI provider**: server-side API key and OpenAI-compatible chat-completions endpoint.

## Requirements

- Node.js 20+ recommended
- An internet connection for package installation, hosted deployment, and AI API calls

## Run locally for development

1. Install Node.js.
2. Extract this project folder.
3. In the project folder, run `npm install`.
4. Copy `.env.example` to `.env`.
5. Leave `AI_API_KEY` blank to test demo mode, or add your provider's API key and set `AI_BASE_URL` and `AI_MODEL`.
6. Run `npm run dev`.
7. Open the Vite URL shown in the terminal (usually `http://localhost:5173`). The API runs on port 3001.

## Deploy online

This is a single Node web service, so a Node-capable host such as Render, Railway, or another Node hosting provider can run it.

1. Push the project folder to a private Git repository.
2. Create a new **Node web service** from the repository.
3. Build command: `npm install && npm run build`
4. Start command: `npm start`
5. Set environment variables in the host dashboard: `AI_BASE_URL`, `AI_API_KEY`, `AI_MODEL`. `PORT` is supplied by most hosts automatically.
6. Deploy and open the service's HTTPS URL.

Do not put the AI key in frontend files or commit `.env`. Keep it only in the hosting provider's server-side environment settings. Free hosting tiers and AI quotas change; check the current terms and limits before relying on them.

## AI setup

The backend calls an OpenAI-compatible `/chat/completions` endpoint. Set:

- `AI_BASE_URL`: API base URL, without a trailing slash (default `https://api.openai.com/v1`)
- `AI_API_KEY`: your secret API key
- `AI_MODEL`: a model available to your provider (default `gpt-4o-mini`)

The key is only read by the server. Without a key, Daily 10 uses a small curated demo set and Ask & Watch displays a demo storyboard rather than pretending it researched the custom question.

## Important limitations before public use

This is a functional MVP, not a finished child-safety-certified product. AI-generated source links may be wrong or irrelevant; source URLs must be verified before presenting an answer as fact-checked. For a stronger production version, add source retrieval and URL validation, content moderation, rate limits, parent controls, privacy notice/consent, abuse reporting, and automated tests. The current “animation” is an illustrated scene presentation with gentle motion and browser narration—not a generated cinematic MP4. Browser speech voices depend on the device and installed languages. Hindi output is requested from the AI and speech synthesis but quality varies by model/browser.

## Project layout

- `server/index.js` — API, demo content, AI provider integration, static production serving
- `client/src/main.jsx` — React app and user interactions
- `client/src/style.css` — responsive UI and animated scene styling
- `.env.example` — server configuration template
