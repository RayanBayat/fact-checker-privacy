# Privacy Policy for YouTube Fact Checker

**Last updated:** November 3, 2026

YouTube Fact Checker is a client-side browser extension that fact-checks factual claims in YouTube videos while you watch.

---

## 1. No developer server and no telemetry

- **No developer servers:** Nothing is sent to the extension's developer: there is no developer server, and no analytics or tracking. The extension has no backend, proxy or tracking server, and we do not collect, view, store, sell or log your browsing history, IP address, device information or video viewing habits.
- **Client-side execution:** All processing logic runs inside your browser: in the extension's background service worker, its settings page and its content scripts. The extension loads no scripts, fonts or images from other websites.

---

## 2. What leaves your browser, and where it goes

Data leaves your browser **only** to the one AI service the extension uses, which you sign in to in the settings page, and to YouTube itself to read a video's captions (section 2.4). That service is OpenAI, through your ChatGPT plan (the "ChatGPT plan" in the settings page). Every request to it is made by the extension's background service worker. Chrome asks for your permission for OpenAI's addresses when you choose **Continue with ChatGPT**; at install, the extension asks only for YouTube.

| Service | Where requests go |
|---|---|
| OpenAI, with your ChatGPT plan | `api.openai.com`, and `auth.openai.com` for the sign-in (section 2.5) |

Earlier versions could also use other AI services with your own API key. This version does not offer them: it does not ask Chrome for their addresses, and it sends them nothing, even if an earlier version left one of their keys in this browser.

### 2.1 While you watch a video

While you watch, the video's title, channel, description and caption text are sent to the AI service you signed in to, to find and check claims; it handles them under its own terms and privacy policy.

In detail, at the default settings:

1. **Finding claims** sends the video's title, channel and language; the caption text, about 40 sentences per request, with the two sentences before them for context; and up to three short notes taken from earlier captions (for example which country or year the video is about). This step does not search the web.
2. **Checking claims** sends each claim with the caption text around it; the video's title, channel, publish date and language; today's date; and short context notes: the title and channel again, the first 500 characters of the video's description, the title of the chapter the claim is in, and notes taken from earlier captions. The model searches the web itself and returns a verdict with the sources its search cites.

Everything someone else wrote (the title, channel, description, chapter titles, captions, and the titles and quotes of sources) is placed in the request as quoted material: it is cleaned of control and invisible characters, kept inside marked blocks, and the model is told it is data and never instructions.

How much is sent depends on your limits. By default at most 25 claims per video are checked and checking starts by itself when a video opens. You can raise the limit (up to 5,000, or all claims), find claims only in the part of the video you are watching, set checking to start only when you press a button, and skip videos longer than a length you choose. When checking is set to start manually, or a video is longer than your limit, nothing is sent until you press Check this video or Check anyway.

### 2.2 When you open the settings page

Opening the settings page asks the service you signed in to for the list of models on your plan. Your sign-in is sent to it; no video text is.

- Nothing is asked while you are not signed in, or while the service is turned off.
- A list counts as fresh for 24 hours. The page asks again after that, when you press Refresh, and when you preview a preset (which refreshes a list older than an hour). The new list replaces the old one; if the service cannot be reached, the old list stays and is shown with its age.
- The service is asked only if Chrome has allowed its addresses.

### 2.3 When you press a test button

- **Test connection** lists the models on your plan. The request carries your sign-in and no video text.
- **Test this model** sends one short request made only of text that the extension itself wrote (a made-up claim, made-up sources or made-up sentences, depending on what is tested). It carries no video text.
- **Try a claim** sends the claim you type, with a fixed title ("Manual test from the settings page").

### 2.4 Captions from YouTube

To read a video's captions the extension asks YouTube for the video's caption file, the same request the video player makes, and, if needed, turns captions on in the background for a moment and puts your caption setting back. These requests go from the YouTube page you are watching to YouTube, as the player's own requests do. Nothing about them is sent anywhere else.

### 2.5 Signing in

If you choose **Continue with ChatGPT**, you sign in on OpenAI's own page (`auth.openai.com`); the extension never sees your password. OpenAI gives the extension a short-lived access token and a longer-lived refresh token that let it use your ChatGPT plan through OpenAI's "Sign in with ChatGPT" program. Requests go to `api.openai.com` with `store: false`. The extension asks the model to search the web for each claim; whether OpenAI's route always returns the sources of that search has not been verified, and a verdict without a source the search cited is shown as Unclear. **Disconnect** deletes the sign-in from this browser and asks OpenAI to revoke it; you can also remove the app in ChatGPT settings. Usage counts against your ChatGPT plan's limits.

### 2.6 The cost estimate and usage counts

The cost summary on the Limits section is worked out on your device, from the prices the model list gives and from assumptions held in the extension. It is labelled "Estimate, not measured" and sends nothing. Counts of requests and how long each model took are kept on your device (section 3) and are never sent anywhere.

---

## 3. What is stored on your device

Your sign-in, settings, model lists, checked results and usage counts are stored only in this browser and are never synced.

- **Sign-in:** the ChatGPT refresh token, the identifier OpenAI gave the app, your ChatGPT account's identifier, and the email address or name on that account (shown in settings) are kept in Chrome's local extension storage (`chrome.storage.local`). Chrome does not encrypt this storage; anyone with access to your browser profile could read it. The ChatGPT access token (valid for about an hour) is kept only in memory (`chrome.storage.session`): it is gone when the browser restarts and when the extension is reloaded, updated or turned off. A key saved by an earlier version stays in local storage until you remove it (section 5); this version never uses it.
- **Never synced:** Nothing is stored in `chrome.storage.sync`, so nothing is synced across devices or Google accounts.
- **Restricted use:** Your sign-in stays in this browser and is sent only to the service it belongs to. It is stored on this device without encryption, so anyone with access to this browser profile could read it. The sign-in is read only by the extension's background service worker; the extension never sends a sign-in token to the YouTube page or to its content scripts.
- **Settings:** whether the service is on, its model, the model that finds claims, your limits, display choices and the main on/off switch.
- **Model lists:** the list of model names on your plan that the service returned (no video text). The extension deletes it when you disconnect; no other control clears it.
- **Usage counts:** for each model you use, how many requests it made, how many failed and how long the newest successful ones took (up to 20), and how many claims were checked in this browser session (session storage, cleared when the browser restarts or the extension is reloaded, updated or turned off). They stay on your device and are used only to show timings in the settings page (the Overview, the Models section and the model picker) and for the Fastest preset. No button clears the request counts and timings; Reset counter sets the session's claim count back to zero (section 5); removing the extension deletes all of them.
- **Small flags:** whether a Try a claim has worked; the outcome of the last web-search test of your ChatGPT plan (with the model's name and a time) and the code of its last plan-level error (with a time), never a token or an email; and, in this page's own storage, your theme choice and which parts of the settings page are open. Disconnect deletes the web-search outcome and the plan-level error code, and Reset settings puts the theme back to System; whether a Try a claim has worked and which parts of the page are open have no button, and only removing the extension deletes them.

### Stored results

- To avoid redundant requests, the extension stores which sentences are claims and the verdicts for each video locally in `chrome.storage.local`.
- Stored results expire after 30 days without being used and are capped at about 5 MB using a least-recently-used (LRU) policy. The extension removes expired results, and the least recently used ones beyond the cap, each time its background service worker starts. Clear stored results deletes them all (section 5).

---

## 4. The settings file

A settings file holds no keys and no sign-in, and it stays on your computer.

**Export settings** (Data and privacy) saves your saved settings as a file named `youtube-fact-checker-settings.json` through your browser's download: whether the service is on, its model, the model that finds claims, thresholds, limits, display choices and the main switch. It never holds a sign-in, your email, a model list, a stored result or a usage count, and the extension never uploads it. **Import settings** reads a file you choose, on your device only: it checks the file, lists what it would change, and puts the values on the settings page; nothing is saved until you press Save, and your sign-in and model lists are never touched. There is no export or import of checked results.

---

## 5. How to delete your data

The Data and privacy section of the settings page clears stored results, removes the sign-in and resets settings; request counts, timings, model lists and a few small flags have no button of their own. Removing the extension from Chrome deletes everything it stored.

What each control deletes, and what it leaves:

- **Disconnect ChatGPT:** In Services, press **Disconnect**. This deletes the sign-in from this browser (the tokens, the identifiers OpenAI gave the app, the email address or name shown in settings, the records of the last web-search test and the last plan-level error, and the stored model list) and asks OpenAI to revoke it.
- **Remove the sign-in and any old key:** In Data and privacy, open Advanced and press **Remove all keys**. This disconnects ChatGPT (previous item) and deletes any key an earlier version saved, with the model lists of those services. Your settings, stored results and usage counts are kept.
- **Delete stored results:** In Data and privacy, press **Clear stored results**. This deletes every stored claim and verdict. Model lists, usage counts, the sign-in and settings are kept.
- **Reset settings:** In Data and privacy, open Advanced and press **Reset settings**. This puts whether the service is on, its model, the model that finds claims, your limits, your display choices, the main on/off switch, whether the panel is collapsed and this page's theme back to what a first run uses. The sign-in, model lists, stored results and usage counts are kept.
- **Reset the session count:** In Limits, open Advanced and press **Reset counter**. This sets the count of claims checked in this browser session back to zero. Nothing else changes.
- **What no button deletes:** the request counts and timings kept for each model, the model list (except as described above), whether a Try a claim has worked, and which parts of the settings page are open. Only removing the extension deletes them.
- **Delete everything:** Right-click the extension's icon and choose **Remove from Chrome**. This erases everything the extension stored in this browser: your sign-in, any old key, settings, model lists, stored results and usage counts. (Clearing browsing data in Chrome's settings does not remove extension storage.)

**What deleting here does not do:**

- It does not delete what the AI services already received while you watched. Each handles that under its own terms and privacy policy.
- It does not cancel a key at the service that issued it: if an earlier version held one of your API keys, delete or replace it in that service's own account. For ChatGPT, Disconnect asks OpenAI to revoke the sign-in, and you can also remove the app in ChatGPT settings.
- A settings file you exported is an ordinary file on your computer. Delete it yourself.

---

YouTube is a trademark of Google LLC. Use of this trademark is subject to Google Permissions. This extension is not affiliated with, endorsed by or sponsored by YouTube, Google, OpenAI, Anthropic, xAI, DeepSeek or OpenRouter.
