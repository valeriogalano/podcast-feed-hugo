# podcast-feed-hugo

A Hugo module that generates a standards-compliant podcast RSS feed, supporting:

- **iTunes / Apple Podcasts** namespace
- **Podcast Index** namespace (`podcast:guid`, `podcast:funding`, `podcast:updateFrequency`, `podcast:transcript`, `podcast:chapters`, `podcast:soundbite`)
- **Dual CDN URLs** — one for GUID/canonical, one with analytics tracking (e.g. [OP3](https://op3.dev))
- **Transcripts** — SRT, VTT, JSON
- **Chapters** — JSON chapters format
- **Soundbites** — read from `assets/soundbites/<episode>.txt`

## Demo

- [Podcast feed](https://valeriogalano.github.io/podcast-feed-hugo/podcast/index.xml)
- [Sitemap](https://valeriogalano.github.io/podcast-feed-hugo/sitemap.xml)

---

## Usage

### Standalone site

Clone or download this repository, configure `config.toml`, then:

```bash
# Create a new episode
hugo new podcast/my-episode-title.md

# Serve locally
hugo server -D
```

Feed available at: `http://localhost:1313/podcast/index.xml`

### As a Hugo module

Add this module to an existing Hugo site.

**1. Initialize your site as a module** (if not already done):

```bash
hugo mod init github.com/YOUR_USER/YOUR_SITE
```

**2. Add the import to `config.toml`:**

```toml
[module]
  [[module.imports]]
    path = "github.com/valeriogalano/podcast-feed-hugo"
```

**3. Fetch the module:**

```bash
hugo mod get github.com/valeriogalano/podcast-feed-hugo
```

The module provides:
- `layouts/podcast/podcast.rss.xml` — RSS feed template (section-based)
- `layouts/podcast/episode.html` — basic episode page
- `layouts/partials/podcast/soundbites.html` — soundbites partial
- `archetypes/podcast.md` — episode archetype

Override any of these by placing a file with the same path in your site's `layouts/` or theme directory.

---

## Configuration (`config.toml`)

```toml
[params.podcast]
  title        = "My Podcast"
  subtitle     = "Subtitle"
  summary      = "Description shown in podcast apps"
  authors      = ["Author Name"]
  email        = "author@example.com"
  image        = "img/podcast-logo.png"

  # Base CDN URL for audio, images, transcripts, and chapters
  cdn_base_url = "https://cdn.example.com/podcast/"

  # Optional: URL with analytics tracking (e.g. OP3).
  # Falls back to cdn_base_url if not set.
  cdn_tracked_base_url = "https://op3.dev/e/cdn.example.com/podcast/"

  # Unique podcast GUID — generate one at https://podcastindex.org/
  guid = ""

  copyright   = "© 2025 Author Name"
  category    = "Technology"
  sub_category = ""
  explicit    = "no"
  itunes_type = "episodic"   # "episodic" or "serial"

  # Update frequency (RRULE FREQ value): DAILY, WEEKLY, MONTHLY, YEARLY
  updateFrequency = "weekly"

  funding_url  = "https://example.com/support"
  funding_text = "Support the show"
```

---

## Episode frontmatter

```yaml
---
layout: episode
title: "Episode title"
subtitle: ""            # optional
date: 2025-01-01T08:00:00+01:00
number: "42"            # episode number (optional)
season: "2"             # season number (optional)
episode_type: "full"    # full | bonus | trailer
explicit: "no"
audio: "episodes/my-episode.mp3"
audio_duration: "01:23:45"
audio_size: 0           # file size in bytes
transcript: "transcripts/srt/my-episode.srt"   # optional: .srt .vtt .json
chapters:   "chapters/my-episode.json"          # optional
image:      "covers/my-episode.jpg"             # optional, falls back to podcast logo
authors:    ["Author Name"]
series:     []
tags:       ["tag1", "tag2"]
draft: true
---
```

### Soundbites

Create `assets/soundbites/<episode-filename>.txt` (tab-separated or space-separated):

```
12.5	45.0	This is a soundbite title
```

Columns: `start_time`, `end_time`, `title`

---

## Local development

```bash
hugo server -D
# → http://localhost:1313/podcast/index.xml
```

## Deploy to GitHub Pages

Push to `main` — the included GitHub Actions workflow builds and deploys automatically.