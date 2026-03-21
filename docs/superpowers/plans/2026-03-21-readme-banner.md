# README Banner Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add the provided PNG as a repo-local banner rendered at the top of the GitHub README.

**Architecture:** Store the banner image in `assets/banner.png` and reference it from `README.md` using GitHub-compatible HTML. Keep the existing heading and body text unchanged so the banner is additive, not a rewrite.

**Tech Stack:** Markdown, GitHub README HTML rendering, repo-local PNG asset

---

## Chunk 1: Banner Asset And README Update

### Task 1: Prepare stable asset path

**Files:**
- Create: `assets/banner.png`

- [x] **Step 1: Copy the provided screenshot into a stable asset path**

Run: `cp "Screenshot 2026-03-21 at 14.54.43.png" assets/banner.png`
Expected: `assets/banner.png` exists

- [x] **Step 2: Verify the asset is present**

Run: `ls assets`
Expected: `banner.png`

### Task 2: Render banner in README

**Files:**
- Modify: `README.md`

- [x] **Step 1: Add banner markup at the top of the README**

Insert:

```html
<p align="center">
  <img src="assets/banner.png" alt="Avoid Slop banner" width="100%" />
</p>
```

above:

```md
# Avoid Slop
```

- [x] **Step 2: Verify the README still keeps its existing title and intro**

Run: inspect the top of `README.md`
Expected: banner first, heading second, existing text preserved

### Task 3: Sanity check

**Files:**
- Modify: `README.md`
- Create: `assets/banner.png`

- [x] **Step 1: Confirm the README references the repo-local asset**

Run: inspect `README.md`
Expected: image source is `assets/banner.png`

- [x] **Step 2: Confirm no other README content changed unexpectedly**

Run: compare the remainder of the file
Expected: original sections remain intact
