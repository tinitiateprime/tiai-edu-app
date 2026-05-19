# Tinitiate Education Content Repository

This repository is the content source for the Tinitiate education web app.

Recommended future repository name:

- `tiai-edu-app`

Until the GitHub rename happens, the app can continue to fetch from the current repository name and switch over later through one central config value.

## Purpose

This repository organizes every major learning module in one place:

- `interview-qna`
- `courses`
- `cbt`
- `news-ticker`

The website should fetch data from this repository so content updates can be managed through GitHub instead of hardcoding data inside the app.

## Folder Guide

### `interview-qna`

Stores interview questions and answers in markdown.

- `catalog.yaml` is the app manifest
- `questions/*.md` are the detailed answer files

### `courses`

Stores the course catalog and subject entry READMEs.

- `catalog.yaml` is the subject manifest
- `courses/<subject>/README.md` defines topic order for that subject

The subject READMEs in this repository are imported from the existing course repositories so the app can use one content index while still reusing the current course material.

### `cbt`

Stores all CBT content in one folder:

- `cbt/slideshows`
- `cbt/training-videos`
- `cbt/audio-books`

### `cbt/slideshows`

Stores markdown slideshow decks for CBT.

- `av-metadata.yaml` is the deck manifest
- each deck contains a `slideshow-content.md`
- slide separator: `---`

### `cbt/training-videos`

Stores training-video metadata for content that can be embedded or streamed directly by the app.

- `av-metadata.yaml` is the media manifest
- `collections/*.md` provides optional notes for the UI

### `cbt/audio-books`

Stores audio-learning metadata and optional notes.

- `av-metadata.yaml` is the media manifest
- `collections/*.md` provides optional notes for the UI

### `news-ticker`

Stores top-strip content for:

- jobs
- trending technologies
- TinitiateAI events

## Content Update Rules

### Interview QnA

1. Add a new markdown file in `interview-qna/questions/`
2. Add a matching entry in `interview-qna/catalog.yaml`

### Courses

1. Add or update the subject entry in `courses/catalog.yaml`
2. Keep subject topic order inside the subject `README.md`
3. Topic markdown links inside that README should point to valid markdown files

### Slideshows

1. Add a new deck entry in `cbt/slideshows/av-metadata.yaml`
2. Add the deck markdown file
3. Keep slide order in markdown using `---`

### Videos and Audio

1. Add metadata in the correct `cbt/*/av-metadata.yaml`
2. Add optional notes markdown if needed
3. For repo-hosted offline playback, use `mediaPath` for files such as `.mp4`, `.webm`, `.mp3`, or `.m4a`
4. Optional fields:
   `posterPath` for thumbnails, `mimeType` for explicit media type, `embedUrl` for demo embeds, and `playlistUrl` for external source links

### News Ticker

1. Add a new item in `news-ticker/feed.yaml`
2. Set `kind`, `label`, `title`, `href`, and `priority`

## App Fetching Model

The website should:

1. fetch manifest files from this repository
2. resolve markdown or metadata paths from those manifests
3. render content without hardcoding the data inside the app

This keeps GitHub as the content CMS and keeps the frontend focused on presentation.
