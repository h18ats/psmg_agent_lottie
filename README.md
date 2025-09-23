# PSMG Agent Lottie

## Overview
This project is a single-page web application for the PSMG Full Day London Summit, featuring the "Lottie" agent widget powered by ElevenLabs and Legal Engine. The page collects user identity and UTM parameters from the URL and passes them to the agent widget for personalized interaction and analytics.

## UTM Parameter Handling

### 1. Extraction
- The script reads UTM parameters (`utm_source`, `utm_medium`, `utm_campaign`, `utm_term`, `utm_content`) from the URL query string using `URLSearchParams`.
- It also supports alternative keys (e.g., `source` for `utm_source`).

### 2. Normalization and Storage
- The script sanitizes all values to prevent XSS.
- A unique `client_id` is generated and stored in `localStorage` if not already present.

### 3. Display
- User identity fields (name, company, email, role) are prefilled in read-only form fields for transparency.

### 4. Passing to the 11L Widget
- All extracted and normalized UTM parameters, along with user identity and `client_id`, are bundled into a `dyn` object.
- This object is passed to the `<elevenlabs-convai>` widget as a JSON string via the `dynamic-variables` attribute.
- The widget can then use these variables for personalized conversation and analytics.

### 5. Analytics
- The same parameters are sent to an n8n webhook for logging and analytics.
- The query string is also appended to Legal Engine "About" links to preserve UTM tracking across navigation.

## Example
If a user visits:

```
https://example.com/?utm_source=linkedin&utm_campaign=summit2025&name=Jane+Doe&company=Acme
```

- The form will show "Jane Doe" and "Acme".
- The widget will receive all UTM and identity parameters in its `dynamic-variables`.
- Analytics will be logged with these details.

## File Structure
- `index.html` — Main application and all logic

## Dependencies
- [@elevenlabs/convai-widget-embed](https://www.npmjs.com/package/@elevenlabs/convai-widget-embed) (loaded via CDN)

---
For questions, contact the PSMG Summit team or Legal Engine.
