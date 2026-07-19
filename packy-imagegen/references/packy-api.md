# PackyAPI GPT Image 2 Reference

Official guide: <https://docs.packyapi.com/docs/paint/GPTImage.html>

## Endpoint

- Base URL: `https://www.packyapi.com/v1`
- Generate: `POST /images/generations`
- Model: `gpt-image-2`
- Authentication: Sora-group bearer token
- Unsupported generation routes: Responses API and Chat Completions API

## Parameters

- `prompt`: required string
- `n`: only `1`
- `size`: `auto` or a valid custom size
- `quality`: `low`, `medium`, `high`, or `auto`
- `response_format`: `url` or `b64_json`
- `output_format`: prefer `png` or `jpeg`
- `background`: default or `opaque`; transparent is unsupported
- `moderation`: `auto` or `low`

Custom sizes must have edges divisible by 16, a maximum edge of 3840, a long-to-short ratio no greater than 3:1, and 655,360 to 8,294,400 total pixels.

## Errors

- `401` or `403`: invalid token or wrong permissions.
- `503 model_not_found`: token is not in the Sora group or the group has no gpt-image-2 distributor.
- Timeout near 60 seconds: bypass a local proxy for `packyapi.com` or increase the client timeout. Image generation can take several minutes.
- Successful response but no file: inspect `data[0]`; PackyAPI may return either `url` or `b64_json`. The bundled script handles both.
