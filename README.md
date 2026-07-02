# SE Learning Content

Static content for the [SE_Learning_Platform](https://github.com/Keerthi-1104) Flutter app.
Served free via **jsDelivr CDN**.

## Layout

```
content_manifest.json     # index — the app fetches this first on launch
roadmap.json              # 16-level roadmap
level_01/*.json           # per-topic JSON (analogy, sections, quiz, ...)
level_02/*.json
...
level_12/*.json
```

## How to publish an update

The source of truth lives in the **main app repo** at
`SE_Learning_Platform/app/assets/content/`. This repo is a **mirror**.
Regenerate it after any content edit:

```bash
cd path/to/SE_Learning_Platform
node tools/publish_content.js         # → writes ../se-learning-content/
cd ../se-learning-content
git add -A && git commit -m "content update" && git push
```

jsDelivr edge-cache picks up the push in ~10 min. To purge immediately,
visit `https://purge.jsdelivr.net/gh/<user>/se-learning-content@main/content_manifest.json`.

## CDN URLs the app uses

```
https://cdn.jsdelivr.net/gh/Keerthi-1104/se-learning-content@main/content_manifest.json
https://cdn.jsdelivr.net/gh/Keerthi-1104/se-learning-content@main/level_02/streams.json
```

Override for a fork:

```bash
flutter run --dart-define=CONTENT_CDN=https://cdn.jsdelivr.net/gh/your-name/your-fork@main
```

## Why this over Firebase / Supabase?

Content is read-only and versioned in git — static hosting is enough.
GitHub + jsDelivr = **₹0/month, unlimited bandwidth, no auth to manage**.
Graduate to Firebase only when we need per-user progress sync across devices
or premium-content gating.
