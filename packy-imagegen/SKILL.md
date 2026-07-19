---
name: packy-imagegen
description: Generate raster images with PackyAPI's Sora-group gpt-image-2 endpoint and save verified PNG or JPEG files locally. Use when Codex needs to create an image through PackyAPI, when the built-in image_gen tool is unavailable, when the standard imagegen CLI fails to save PackyAPI URL responses, or when users mention PackyAPI, a Sora image key, gpt-image-2, or the Packy drawing API.
---

# Packy Imagegen

Generate one image through PackyAPI's OpenAI-compatible Images API with the bundled dependency-free script. Do not modify or invoke the system `imagegen` CLI for this route.

## Requirements

Require a PackyAPI token created in the `sora` group. Read it from `PACKY_API_KEY`; fall back to `OPENAI_API_KEY`. Never place a key in a command argument, prompt, file, output, or chat response.

If neither variable is set, ask the user to set one locally. Do not ask them to paste a key into chat.

```bash
export PACKY_API_KEY="<Sora group token>"
```

## Workflow

1. Shape the user's request into a concise production prompt. Preserve exact requested text and list essential constraints.
2. Choose a valid size. Prefer `1024x1024`, `1536x1024`, or `1024x1536`; use `quality=low` for tests and `medium` or `high` for finals.
3. Choose a workspace output under `output/imagegen/` unless the user names another destination.
4. Run `scripts/generate.py`. Use `--force` only when the user explicitly requested replacement or the target is a disposable test artifact.
5. Inspect the resulting image with the available image-viewing tool. Check subject, composition, text, dimensions, and obvious artifacts.
6. Iterate with one targeted prompt change if necessary.
7. Return the absolute saved path, final prompt summary, size, quality, and that PackyAPI CLI mode was used.

## Command

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/packy-imagegen/scripts/generate.py" \
  --prompt "A realistic product photo of a ceramic mug" \
  --size 1024x1024 \
  --quality medium \
  --out output/imagegen/ceramic-mug.png
```

Use `--prompt-file` for long prompts. Use `--dry-run` to validate parameters without a network request. The script waits synchronously, requests `b64_json`, accepts a URL response if the provider returns one, validates the file signature, and writes atomically.

## Guardrails

- Use only `POST /v1/images/generations`; PackyAPI does not support gpt-image-2 generation through Responses or Chat Completions.
- Keep `n=1`; make separate calls for variants.
- Do not request transparent output. PackyAPI gpt-image-2 supports opaque/default backgrounds, not native transparency.
- Do not persist credentials in this skill or copy tokens from `~/.codex/config.toml` unless the user explicitly requests credential migration.
- Do not run duplicate requests after an execution tool yields early. Check the returned session/process and wait for it to finish before retrying.
- Treat a valid PNG/JPEG output as success only after visual inspection.

Read [references/packy-api.md](references/packy-api.md) when diagnosing provider errors, changing advanced parameters, or selecting nonstandard sizes.
