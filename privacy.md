---
layout: default
title: VoiceWay — Privacy Policy
---

# VoiceWay — Privacy Policy

_Last updated: 2026-10-09_

VoiceWay is a GPS-based audio tour guide app developed by Sergey Lyapustin (individual developer, contact: voiceway@slyapustin.com).

This policy describes what information the app collects, why, and who it's shared with.

## What we collect

### Stored on your device
- **Listening history** — which places you've heard narrations about
- **Played points of interest** — to avoid repeating narrations during a tour
- **Cached narration text and audio files** — so you can replay without re-fetching
- **Preferences** — language, voice, trigger distance, enabled categories, etc.
- **Debug log** — your recent actions inside the app, which can include place and location context, for your own troubleshooting via "Export Logs"

Full debug logs and listening history are not uploaded automatically. You can explicitly export and share them. Optional automatic diagnostic sharing uses the restricted report described below.

### Sent to Wikimedia and our backend (only during active use)
When the app searches for nearby places, it sends your location coordinates and selected Wikipedia language to Wikimedia's geosearch API. When it requests a narration, the app sends to our Cloudflare Worker backend:
- **Your precise location** (latitude/longitude), when available — used for location-based article lookup. The backend does not write these coordinates into its usage counters, device metadata, narration/audio caches, or automatic diagnostic reports.
- **The Wikipedia page ID and title** of the place you're interested in
- **Your narration language and length preference**
- **A hash of your device's vendor identifier** (SHA-256 of iOS `identifierForVendor`) — used to enforce usage limits and protect app endpoints from excessive requests
- When cloud text-to-speech is enabled, the narration text and selected voice are sent to the backend to generate audio.

Cloudflare derives a country, city, region, and time zone from the request IP. The backend stores those fields with the device hash, app version, and first/last-seen times for up to 30 days after the last metadata update. This record does not contain the raw IP address. Cloudflare also processes IP addresses and request metadata to operate its services.

We do **not** collect or store:
- Your name, email, phone number, Apple ID, or any account identifier
- Your contact list, photos, calendar, or other personal data
- Your IP address beyond what Cloudflare's standard request logging retains
- Analytics events tied to an identifiable user
- Any behavioral profile, advertising identifier, or third-party tracking data

### Optional automatic diagnostics
Automatic diagnostic sharing is off by default. If you enable it in Settings, the app may send a bounded report of recent app events and technical failures to our backend, no more than once every 15 minutes. Reports contain app version, event times, session/request/operation identifiers, screen/control names, selected technical settings, error codes, and request timings.

These automatic reports exclude precise coordinates, place titles and Wikipedia page IDs, typed search terms, narration text, feedback notes, and credentials. The existing device header authenticates/rate-limits requests; it is not copied into the diagnostic report. The backend independently filters report fields.

Raw reports are kept for up to seven days and may be deleted sooner after processing. Sanitized technical summaries may be retained in our private GitHub issue tracker and processed by AI-assisted development tools to reproduce, fix, and verify bugs. Turn off automatic sharing in Settings to stop future uploads. This does not delete reports already submitted; contact us for help with removal.

To enforce the 15-minute upload limit, the backend also keeps a hash of the device hash in a cooldown record for up to 15 minutes.

### Sub-processors
- **GitHub and AI-assisted development tools** — process filtered technical bug summaries for diagnosis and repair.
- **Cloudflare Workers + KV + R2** — hosts our backend, caches generated narrations and audio, and stores device-linked usage counters and limited device metadata
- **OpenAI API** — generates the narration text (Chat Completions) and the synthesized voice audio (Text-to-Speech) from Wikipedia article content. Our backend sends the Wikipedia article text + your narration language to OpenAI. Per OpenAI's API data usage policy, data sent through the API is not used to train OpenAI models.
- **Wikipedia (Wikimedia Foundation)** — source of place descriptions. The app fetches public Wikipedia articles via the Wikimedia APIs.
- **OpenStreetMap Nominatim** — the backend may send coordinates for reverse geocoding to select the local Wikipedia language.

## How long we keep it

- **Device-side cache**: cached Wikipedia summaries, narration text, and audio stay until you clear the cache (Settings → Clear Cache) or delete the app. Listening history, played-place records, preferences, and debug logs have their own in-app reset or clear controls; debug logs are limited to the newest 5,000 entries.
- **Backend usage counters**: per-day narration and cloud-TTS usage counters expire three days after the start of their UTC usage day. Device metadata (IP-derived country/city/region/time zone, app version, and first/last-seen times) expires up to 30 days after its last update.
- **Shared narration text cache (backend)**: generated narration text is kept for up to 90 days so other users asking for the same place can get a faster response.
- **Shared audio cache (backend)**: generated audio is stored in an R2 cache. The current backend does not set an automatic per-object expiration; files remain until manually deleted.
- **Automatic diagnostics (backend)**: accepted reports are kept for up to seven days and may be deleted sooner after their sanitized summary has been added to our private issue tracker. The private issue tracker may retain those summaries after the raw reports are deleted.
- **Service request logs**: Cloudflare handles IP addresses and request metadata under its service configuration and [privacy policy](https://www.cloudflare.com/privacypolicy/).

## Your rights

- **Remove app data**: deleting the app removes its local data. It does not immediately remove backend records: usage counters expire three days after their UTC usage day, and device metadata expires up to 30 days after its last update. Shared caches and issue summaries follow the retention described above.
- **See what we have**: email us. Given the small scope, we can usually reply within a few days.
- **Stop location sharing**: revoke Location permission in iOS Settings → VoiceWay. The app falls back to manual map browsing.
- **Use on-device speech**: turn on "Device TTS" in Settings. The audio is spoken on your device and the cloud TTS path is not invoked, so the cloud TTS character quota does not apply. Narration text is still generated through our backend and requires an internet connection; the daily narration quota still applies.

## Children

VoiceWay is not directed at children under 13. We don't knowingly collect information from children. If you believe we have, contact us and we'll delete it.

## Changes

We may update this policy. When we do, the "Last updated" date above changes.

## Contact

**Email**: voiceway@slyapustin.com
