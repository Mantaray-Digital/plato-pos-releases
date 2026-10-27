# Plato POS releases

Public Windows installers and update metadata for Plato POS. Application source code is maintained separately.

## Install or move to GitHub updates

Download the `.exe` from the [Windows update channel](https://github.com/Mantaray-Digital/plato-pos-releases/releases/tag/unsigned-candidate).
Finish checkout, synchronization and printing, quit the existing POS from its tray menu, then run the installer. Do not uninstall the existing app or clear its data first.

Version `0.4.0-rc.3` introduces GitHub updates. Older `rc.1` and `rc.2` installations need this installer once manually because they check the previous website address.

Once installed, use **Settings → General → Check for updates → Download update → Restart and update**. Downloads and restarts require operator action. Normal Quit does not install updates.

The app displays **Plato POS** and keeps the existing candidate register identity and data directory. Moving between candidate and stable installations remains a separate setup. This release is unsigned; Windows may show an unknown-publisher prompt.

## Update channels

Each channel has a permanent release tag. Do not rename or delete these tags.

| Build | Release tag | Metadata asset |
|---|---|---|
| Current unsigned Windows build | `unsigned-candidate` | `unsigned-candidate.yml` |
| Unsigned stable build | `unsigned` | `unsigned.yml` |
| Signed candidate build | `candidate` | `candidate.yml` |
| Signed stable build | `stable` | `latest.yml` |

Only channels with a published build have a release. Signed and unsigned channels are separate; version checks never move installations between candidate and stable.

## Publishing another update

1. Build a strictly newer application version with English and Arabic notes. Run the desktop checks and stage its verified installer, blockmap and metadata using the source repository's release scripts.
2. Upload the versioned installer and blockmap to the matching channel release first. Never replace an existing installer's bytes or remove older installers/blockmaps.
3. Verify their uploaded sizes and hashes, then upload that channel's metadata last. Use `gh release upload <channel> <manifest> --clobber --repo Mantaray-Digital/plato-pos-releases` only for the metadata asset.
4. Run the source repository's `release:verify-feed` command and verify a real installed previous version can check, download and upgrade without losing saved work or duplicating synchronized orders.

Protect repository write access: the unsigned channel verifies download hashes but cannot establish the installer's publisher identity independently of this repository.
