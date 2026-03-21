# README Banner Design

## Goal

Add the provided image as a visible banner at the top of the GitHub repository page by rendering it at the top of `README.md`.

## Chosen Approach

Use a repo-local image asset at `assets/banner.png` and reference it from the top of `README.md` with an HTML `<img>` tag inside a centered paragraph.

## Why This Approach

- Keeps the banner versioned with the repository.
- Works on GitHub without requiring external hosting.
- Allows predictable sizing with `width="100%"`.
- Preserves the existing README title and content below the banner.

## Scope

- Copy the provided PNG into `assets/banner.png`.
- Add the banner markup above the existing README heading.
- Leave all existing README content unchanged.

## Risks

- Large image dimensions may make the banner visually tall on GitHub.
- Relative path rendering depends on the asset remaining in `assets/banner.png`.

## Validation

- Confirm `README.md` references `assets/banner.png`.
- Confirm the asset exists in the repository.
