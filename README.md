# Whats The TL;DR -WhatsApp Chat TL;DR

Chrome extension that exports the current WhatsApp Web chat, filters messages by selected time window, removes phone numbers and other sensitive patterns, and generates concise summaries using Google's Gemini API.

## Features

- One-click summary generation from the active WhatsApp Web chat
- Selectable time ranges: last 6 hours, 12 hours, 24 hours, 2 days, 1 week, or all visible messages
- Automatic redaction of 10-digit phone numbers
- Two summary modes:
  - Short: single tight paragraph (100–150 words)
  - Detailed: bullet-point list of key facts, decisions, tasks, dates, and names
- Local storage for your Gemini API key
- No messages are stored or sent anywhere except to the Gemini API for summarization

## Requirements

- Google Chrome (or compatible Chromium-based browser)
- Active WhatsApp Web session[](https://web.whatsapp.com)
- Gemini API key (free tier available at https://aistudio.google.com/app/apikey)

## Installation (Development)

1. Clone or download this repository
2. Open Chrome and navigate to `chrome://extensions/`
3. Enable "Developer mode" (top right)
4. Click "Load unpacked" and select the extension folder
5. Visit https://web.whatsapp.com and open any chat

The extension icon should appear in the toolbar.

## Usage

1. Open a chat on WhatsApp Web
2. Click the extension icon
3. (First time only) Enter your Gemini API key and save
4. Select desired time window from the dropdown
5. Choose summary type (Short or Detailed)
6. Click "Generate Summary"
7. Wait a few seconds → copy the result or read directly in the popup

## Privacy & Security Notes

- Only the filtered chat content from the selected time window is sent to Google's Gemini API
- No chat data is stored locally beyond your API key (chrome.storage.local)
- Phone numbers matching the pattern `\b\d{10}\b` are replaced with `[PHONE]`
- Extension does **not** read contacts, profile pictures, media files, or voice messages
- No analytics, no telemetry, no third-party servers except Google AI

## Current Limitations

- Relies on current WhatsApp Web DOM structure (may break after WhatsApp UI updates)
- Only processes messages currently loaded in the viewport or reached by limited upward scrolling
- Maximum practical limit ≈ 800–1200 messages (performance / Gemini token constraints)
- Does not handle quoted messages, replies, or forwarded content context perfectly
- System messages ("This message was deleted", encryption notices, etc.) are included unless filtered

## Planned Improvements

- More robust message extraction (MutationObserver + better fallback selectors)
- Optional filtering of very short messages / greetings / emojis
- Support for custom time ranges
- Export summary to clipboard in markdown / plain text
- Better error handling and user feedback when chat is not loaded
- Option to exclude media captions / links

## Tech Stack

- Manifest V3
- Vanilla JavaScript (no build tools in base version)
- Chrome Extensions APIs: content scripts, messaging, storage, scripting
- Fetch API → Google Generative Language API (Gemini Flash model family)
- DOM observation via MutationObserver
- Simple regex-based content cleaning


