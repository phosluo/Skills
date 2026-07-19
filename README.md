# Skills

A collection of reusable AI agent skills for [Codex](https://github.com/openai/codex).

## Skills

| Skill | Description |
|-------|-------------|
| [packy-imagegen](packy-imagegen/) | Generate images via PackyAPI's gpt-image-2 endpoint and save verified PNG/JPEG files locally |
| [yt-dlp-smart-downloader](yt-dlp-smart-downloader/) | Inspect formats, download media with yt-dlp, repair files with ffmpeg, and clean up filenames |
| [markdown-to-applebooks](markdown-to-applebooks/) | Convert Markdown to EPUB with pandoc and copy into Apple Books |

## Usage

Copy the desired skill folder into your Codex skills directory:

```bash
cp -r <skill-name> ~/.codex/skills/
```

Each skill contains a `SKILL.md` that describes its purpose and workflow.
