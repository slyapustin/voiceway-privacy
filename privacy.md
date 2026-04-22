---
layout: default
title: Voiceway — Privacy Policy
---

# Voiceway — Privacy Policy

**Last updated:** 22 April 2026

Voiceway ("the app") is an iOS app that narrates Wikipedia articles about nearby places. This document explains what data the app handles and how.

## Summary

- No account, no login, no email, no password.
- Your location is used to find nearby places. It is never stored on our servers.
- A random, anonymous device identifier is used for rate-limiting. It is not linked to you or any account.
- The app does not display ads, does not track you across other apps or websites, and does not sell your data.

## What data the app uses

### Precise location
When the app is active, iOS provides your GPS coordinates to the app. Voiceway sends those coordinates to Wikipedia, OpenStreetMap Nominatim, and our own backend **only for the duration of the request** — to look up articles about places near you. We do not retain your location in any database, log, or analytics system.

### Anonymous device identifier
The app generates a SHA-256 hash of the device's `identifierForVendor` value. This hash is sent to our backend as the `X-Device-ID` header so we can apply per-device daily usage limits on narration and text-to-speech generation. The hash cannot be used to identify you, does not persist across app reinstalls, and is not linked to an Apple ID, email address, or any other identity.

### Wikipedia article text
When a place is nearby, the app fetches the corresponding Wikipedia article summary and generates a short spoken narration from it. Narration text is cached on your device and (in hashed form) on our backend so repeated requests do not re-generate the same content. Cached narration text is retained for up to three days on the backend; device-side cache is retained until you clear it in Settings.

### Generated audio
When you use the cloud voice (OpenAI text-to-speech), the generated audio file is cached both on your device and on our backend so re-listens are free and instant. Audio cache is keyed by a hash of the narration text and voice, not by your identifier.

## Data we do not collect

- Name, email address, phone number, or any other contact info
- Apple ID, sign-in credentials, or social-media profile
- Health, financial, or payment information
- Contacts, calendar, photos, microphone, or camera
- Advertising identifier (IDFA)
- Any usage analytics or behavioural tracking

## Where data goes

Voiceway sends data to the following services **only to service real-time requests**:

- **Wikipedia** (Wikimedia Foundation) — article search and summaries. See the [Wikimedia Privacy Policy](https://foundation.wikimedia.org/wiki/Privacy_policy).
- **OpenStreetMap Nominatim** — reverse-geocoding a coordinate to a country/region so we can pick a local-language Wikipedia. See the [Nominatim Usage Policy](https://operations.osmfoundation.org/policies/nominatim/).
- **OpenAI** — narration generation (gpt-5.4-mini) and cloud text-to-speech (gpt-4o-mini-tts), both reached via our backend proxy so no API key is exposed on device. See the [OpenAI API Privacy Policy](https://openai.com/policies/privacy-policy).
- **Cloudflare** — our backend is a Cloudflare Worker with KV and R2 storage. See the [Cloudflare Privacy Policy](https://www.cloudflare.com/privacypolicy/).

We do not sell data to any third party. We do not use data for advertising.

## Permissions the app requests

- **Location (While Using / Always)** — to find places near you and auto-play narrations as you approach them. Required for the app's core function.
- **Background audio / location** — to keep narrations playing when the screen is locked and to detect new places as you move with the app in the background. Only active when you tap the **Auto Narrate** button.

All permissions are optional. If you decline location access, the app still lets you browse and read about places manually from the map.

## Children's privacy

Voiceway is not directed at children under 13 and does not knowingly collect information from them.

## Retention

- Device-side caches (narrations, audio, settings): kept until you clear them in Settings, or uninstall the app.
- Backend narration text cache (hashed key): up to 3 days.
- Backend audio cache (hashed key): up to 30 days.
- Backend per-device daily quota counters: reset every 24 hours.

## Your choices

- Clear all caches: **Settings → Cache → Clear Cache** in the app.
- Export your on-device activity log: **Settings → Debug → Debug Logs → Export**. Logs stay on your device unless you choose to share the exported file.
- Revoke location access: iOS **Settings → Privacy & Security → Location Services → Voiceway**.
- Delete all data: uninstall the app.

## Changes to this policy

We'll post updates on this page with a new "Last updated" date. Material changes will be flagged in the app.

## Contact

Questions or requests about your privacy? Open an issue on [github.com/slyapustin/tour-guide/issues](https://github.com/slyapustin/tour-guide/issues) or email **s.lyapustin@gmail.com**.
