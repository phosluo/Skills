# Naming And Fixups

## Filename cleanup

Use the source title by default, but sanitize characters that are invalid or risky in filesystem paths.

Common replacements:

- `/` -> `_`
- `:` -> ` -`
- repeated spaces -> single space

Avoid aggressive title rewriting. Keep the original wording unless the user asks for a shorter name.

## Safe finalization

When producing a repaired final file:

1. Confirm the original downloaded file exists.
2. Write the repaired file to a temporary or suffixed path first.
3. Confirm the repaired file exists and has non-zero size.
4. Only then rename it into the final desired filename.
5. Remove the original only if the user explicitly asked to keep only the repaired version.

## Size and quality choice

If multiple options are available, show only the practical shortlist:

- low size
- balanced
- high quality
- highest quality

If the user previously stated a stable preference such as `720p`, it is reasonable to reuse that preference for nearby follow-up requests unless the user says otherwise.
