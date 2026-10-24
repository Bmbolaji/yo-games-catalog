# Yo! Games catalog

The live game list for **Yo! Games** on the yo! TV stick. Every stick downloads
`https://bmbolaji.github.io/yo-games-catalog/catalog.json` when Yo! Games opens and every 30 minutes.

**Whatever is committed here goes live on every stick within a few minutes.** Check before you push:

```
python3 tools/validate_catalog.py catalog.json   # tool lives in the yo-games repository
```

## Add or update a game

1. Small game (under 100 MB): put the APK in `apks/<game-id>-<versionCode>.apk`.
   Larger game: create a **Release** in this repository and attach the APK there.
   Never overwrite an existing APK file; use a new file name for each version.
2. Artwork: `art/<game-id>/banner.jpg` (640x360), optionally `hero.jpg` (1280x720).
3. Get the `source` block (in the yo-games repository):
   `python3 tools/apk_entry.py game.apk https://bmbolaji.github.io/yo-games-catalog/apks/<file>.apk`
4. Add the game to `games` in `catalog.json`. The format and a full example are in
   `server/catalog.example.json` and `server/README.md` in the yo-games repository.
5. Validate, commit, push.

## Update Yo! Games itself

Add a `hub` block (see yo-games `docs/RELEASE.md`). The APK must be signed with the Yo! release key.

## Move to another server later

Set `"catalogUrl": "https://new-address/catalog.json"` here and keep this file online until
sticks have checked in.
