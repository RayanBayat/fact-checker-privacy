# Privacy Policy for YouTube Fact Checker

**Last updated:** October 6, 2026

YouTube Fact Checker is a client-side browser extension that fact-checks factual claims in YouTube videos while you watch.

---

## 1. No developer server and no telemetry

- **No developer servers:** Nothing is sent to the extension's developer: there is no developer server, and no analytics or tracking. The extension has no backend, proxy or tracking server, and we do not collect, view, store, sell or log your browsing history, IP address, device information or video viewing habits.
- **Client-side execution:** All processing logic runs inside your browser: in the extension's background service worker, its settings page and its content scripts. The extension loads no scripts, fonts or images from other websites.

---

## 2. What leaves your browser, and where it goes

Data leaves your browser **only** to the AI services you have turned on in the settings page, using your own API key or sign-in, and to YouTube itself to read a video's captions (section 2.4). Every request to an AI service is made by the extension's background service worker. Chrome asks for your permission for a service's address when you turn that service on (the address of Gemini is granted when you install the extension).

| Service | Where requests go |
|---|---|
| Google Gemini | `generativelanguage.googleapis.com` |
| Anthropic Claude | `api.anthropic.com` |
| OpenAI, with an API key | `api.openai.com` |
| OpenAI, with your ChatGPT plan | `api.openai.com`, and `auth.openai.com` for the sign-in (section 2.5) |
| xAI Grok | `api.x.ai` |
| DeepSeek | `api.deepseek.com` |
| OpenRouter | `openrouter.ai`, which forwards requests to the model you choose |

### 2.1 While you watch a video

While you watch, the video's title, channel, description and caption text are sent to the AI services you turned on, to find and check claims; each one handles them under its own terms and privacy policy.

In detail, at the default settings:

1. **Finding claims** goes to one service: the one chosen as the claim finder in the settings, or, when that one cannot be used, the first usable service that can search. It receives the video's title, channel and language; the caption text, about 40 sentences per request, with the two sentences before them for context; and up to three short notes taken from earlier captions (for example which country or year the video is about). It does not search the web.
2. **Checking claims** goes to every service you turned on. Each receives the claim with the caption text around it; the video's title, channel, publish date and language; today's date; and short context notes: the title and channel again, the first 500 characters of the video's description, the title of the chapter the claim is in, and notes taken from earlier captions. A model that searches the web does its own search and returns a verdict with the sources it cites. A model that cannot search (DeepSeek's API), or that you set to judge, also receives the titles, links and short quotes of the sources the other models found.

Everything someone else wrote (the title, channel, description, chapter titles, captions, and the titles and quotes of sources) is placed in the request as quoted material: it is cleaned of control and invisible characters, kept inside marked blocks, and each model is told it is data and never instructions.

How much is sent depends on your limits. By default at most 25 claims per video are checked and checking starts by itself when a video opens. You can raise the limit (up to 5,000, or all claims), find claims only in the part of the video you are watching, set checking to start only when you press a button, and skip videos longer than a length you choose. When checking is set to start manually, or a video is longer than your limit, nothing is sent to any service until you press Check this video or Check anyway.

### 2.2 When you open the settings page

Opening the settings page asks each service you turned on for its list of models. Your key is sent to it; no video text is.

- A service that is turned off is not asked. A key you have typed and not saved is used only for the one lookup or test you press, and is not stored.
- A list counts as fresh for 24 hours. The page asks the service again after that, when you press Refresh, and when you preview a preset (which refreshes lists older than an hour). The new list replaces the old one; if the service cannot be reached, the old list stays and is shown with its age.
- OpenRouter's list can be requested without a key; if you have saved an OpenRouter key, it is sent. While OpenRouter is turned on, the settings page may also ask it for its models in order of speed, in the same way.
- Each service is asked only if Chrome has allowed its address.

### 2.3 When you press a test button

- **Test connection** makes a lookup at the service (of the chosen model, or of your key). The request carries your key or sign-in and no video text.
- **Test this model** sends one short request made only of text that the extension itself wrote (a made-up claim, made-up sources or made-up sentences, depending on what is tested). It carries no video text.
- **Try a claim** sends the claim you type, with a fixed title ("Manual test from the settings page"), to every service you turned on.

### 2.4 Captions from YouTube

To read a video's captions the extension asks YouTube for the video's caption file, the same request the video player makes, and, if needed, turns captions on in the background for a moment and puts your caption setting back. These requests go from the YouTube page you are watching to YouTube, as the player's own requests do. Nothing about them is sent anywhere else.

### 2.5 Signing in

- **OpenRouter:** If you sign in with OpenRouter, OpenRouter creates a key for your account and sends it back to the extension; it is stored like any other key.
- **ChatGPT plan:** If you choose **Continue with ChatGPT**, you sign in on OpenAI's own page (`auth.openai.com`); the extension never sees your password. OpenAI gives the extension a short-lived access token and a longer-lived refresh token that let it use your ChatGPT plan through OpenAI's "Sign in with ChatGPT" program. Requests go to `api.openai.com` with `store: false` and carry the same data as for any other service you turned on. By default this route only judges the sources other models found, because OpenAI documents it as text only; if you set it to search the web the extension asks it to, and whether OpenAI accepts that has not been verified. **Disconnect** deletes the sign-in from this browser and asks OpenAI to revoke it; you can also remove the app in ChatGPT settings. Usage counts against your ChatGPT plan's limits.

### 2.6 The cost estimate and usage counts

The cost summary on the Limits section is worked out on your device, from the prices the model lists give and from assumptions held in the extension. It is labelled "Estimate, not measured" and sends nothing. Counts of requests and how long each model took are kept on your device (section 3) and are never sent anywhere.

---

## 3. What is stored on your device

Your keys, sign-ins, settings, model lists, checked results and usage counts are stored only in this browser and are never synced.

- **Keys and sign-ins:** API keys, the ChatGPT refresh token, the identifier OpenAI gave the app, your ChatGPT account's identifier, and the email address or name on that account (shown in settings) are kept in Chrome's local extension storage (`chrome.storage.local`). Chrome does not encrypt this storage; anyone with access to your browser profile could read it. The ChatGPT access token (valid for about an hour) is kept only in memory (`chrome.storage.session`): it is gone when the browser restarts and when the extension is reloaded, updated or turned off.
- **Never synced:** Nothing is stored in `chrome.storage.sync`, so nothing is synced across devices or Google accounts.
- **Restricted use:** Keys stay in this browser and are sent only to the service they belong to. Keys and sign-ins are stored on this device without encryption, so anyone with access to this browser profile could read them. The key is read only by the extension's background service worker; the extension never sends a key or a sign-in token to the YouTube page or to its content scripts.
- **Settings:** which services are on, their models and roles, the claim finder, your limits, display choices and the main on/off switch.
- **Model lists:** the public lists of model names and numbers that each service returned (no key, no video text), and OpenRouter's speed order. The extension deletes a service's list when that service's key is added, changed or removed, and ChatGPT's list when you disconnect; no other control clears lists.
- **Usage counts:** for each model you use, how many requests it made, how many failed and how long the newest successful ones took (up to 20), and how many claims were checked in this browser session (session storage, cleared when the browser restarts or the extension is reloaded, updated or turned off). They stay on your device and are used only to show timings in the settings page (the Overview, the Models section and the model picker) and for the Fastest preset. No button clears the request counts and timings; Reset counter sets the session's claim count back to zero (section 5); removing the extension deletes all of them.
- **Small flags:** whether a Try a claim has worked; the outcome of the last web-search test of your ChatGPT plan (with the model's name and a time) and the code of its last plan-level error (with a time), never a token or an email; and, in this page's own storage, your theme choice and which parts of the settings page are open. Disconnect deletes the web-search outcome and the plan-level error code, and Reset settings puts the theme back to System; whether a Try a claim has worked and which parts of the page are open have no button, and only removing the extension deletes them.

### Stored results

- To avoid redundant requests, the extension stores which sentences are claims and the verdicts for each video locally in `chrome.storage.local`.
- Stored results expire after 30 days without being used and are capped at about 5 MB using a least-recently-used (LRU) policy. The extension removes expired results, and the least recently used ones beyond the cap, each time its background service worker starts. Clear stored results deletes them all (section 5).

---

## 4. The settings file

A settings file holds no keys and no sign-in, and it stays on your computer.

**Export settings** (Data and privacy) saves your saved settings as a file named `youtube-fact-checker-settings.json` through your browser's download: which services are on, their models and roles, the claim finder, thresholds, limits, display choices and the main switch. It never holds a key, a sign-in, your email, a model list, a stored result or a usage count, and the extension never uploads it. **Import settings** reads a file you choose, on your device only: it checks the file, lists what it would change, and puts the values on the settings page; nothing is saved until you press Save, and your keys, sign-ins and model lists are never touched. There is no export or import of checked results.

---

## 5. How to delete your data

The Data and privacy section of the settings page clears stored results, removes keys and sign-ins and resets settings; request counts, timings, model lists and a few small flags have no button of their own. Removing the extension from Chrome deletes everything it stored.

What each control deletes, and what it leaves:

- **Remove one key:** In Services, press **Remove key** under the service's key field. This deletes that service's saved key from this browser, and with it that service's stored model list. Everything else is kept.
- **Remove every key and sign-in:** In Data and privacy, open Advanced and press **Remove all keys**. This deletes every saved key, disconnects ChatGPT (next item) and deletes the model lists of the services whose keys went. Your settings, stored results and usage counts are kept.
- **Disconnect ChatGPT:** In Services, press **Disconnect**. This deletes the sign-in from this browser (the tokens, the identifiers OpenAI gave the app, the email address or name shown in settings, the records of the last web-search test and the last plan-level error, and ChatGPT's stored model list) and asks OpenAI to revoke it.
- **Delete stored results:** In Data and privacy, press **Clear stored results**. This deletes every stored claim and verdict. Model lists, usage counts, keys, sign-ins and settings are kept.
- **Reset settings:** In Data and privacy, open Advanced and press **Reset settings**. This puts which services are on, their models and roles, the claim finder, your limits, your display choices, the main on/off switch, whether the panel is collapsed and this page's theme back to what a first run uses. Keys, sign-ins, model lists, stored results and usage counts are kept.
- **Reset the session count:** In Limits, open Advanced and press **Reset counter**. This sets the count of claims checked in this browser session back to zero. Nothing else changes.
- **What no button deletes:** the request counts and timings kept for each model, model lists (except as described above), OpenRouter's speed order, whether a Try a claim has worked, and which parts of the settings page are open. Only removing the extension deletes them.
- **Delete everything:** Right-click the extension's icon and choose **Remove from Chrome**. This erases everything the extension stored in this browser: your keys, sign-ins, settings, model lists, stored results and usage counts. (Clearing browsing data in Chrome's settings does not remove extension storage.)

**What deleting here does not do:**

- It does not delete what the AI services already received while you watched. Each handles that under its own terms and privacy policy.
- It does not cancel a key at the service that issued it: delete or replace the key in that service's own account. For ChatGPT, Disconnect asks OpenAI to revoke the sign-in, and you can also remove the app in ChatGPT settings.
- A settings file you exported is an ordinary file on your computer. Delete it yourself.

---

YouTube is a trademark of Google LLC. Use of this trademark is subject to Google Permissions. This extension is not affiliated with, endorsed by or sponsored by YouTube, Google, OpenAI, Anthropic, xAI, DeepSeek or OpenRouter.
