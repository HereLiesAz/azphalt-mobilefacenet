# MobileFaceNet

**MobileFaceNet (face recognition embedding)** — Maps a detected face to an identity embedding.

An **azphalt** AI-model plugin, packaged as a `.azp` (the azphalt analogue of a VS Code `.vsix`). It is
named for the *model*, not a single feature — the same model powers many tools, and it is **host-neutral**:
any azphalt host that understands its role can use it, not just one app. Install it from any host's
**Azphalt Storefront**.

## What it can do

- face ID / recognition
- per-person tagging
- grouping clips by person

## Roles (host-neutral routing)

This plugin contributes the role(s): `face-embedding`. A host routes the model by role — it carries no
`targetApps`, so it is not tied to any single application.

**Example host — [Guillotine](https://github.com/HereLiesAz/Guillotine):** Desktop `faceEmbedModelPath` — face-ID.

## Model file(s)

- **`face-embed.onnx`** (role `face-embedding`) — [upstream](https://huggingface.co/onnx-community/mobilefacenet/resolve/main/mobilefacenet.onnx)

Model license: **MIT (MobileFaceNet)**. This plugin's manifest/packaging is `MIT`.

## How it works — the VSCode Header Pattern

The `.azp` does **not** bundle the weights. The manifest declares each model as a *remote asset*
(`"path": ""` + `remoteUrl` + `checksum` + `byteSize`); the host downloads the weights on install and
verifies them against the pinned SHA-256 — exactly how a large VS Code extension fetches its language
server instead of shipping it inside the `.vsix`. `remoteUrl` points at this repo's own GitHub **Release**
asset (named the exact filename the host expects); the `release` workflow fetches the upstream model,
renames it, checksums it, and publishes it beside the packed `.azp`.

## Build / release

```sh
npm install && npm run build     # packs com.hereliesaz.azphalt.mobilefacenet-1.0.0.azp
git tag v1.0.0 && git push --tags   # runs the release workflow: hosts the model + .azp
```
