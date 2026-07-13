# Blog Taxonomy Guide

This file defines the preferred metadata taxonomy for posts in this repository.

## Principles

1. Keep `categories` as broad topic clusters used for top-level navigation.
2. Use `tags` for specific concepts, standards, technologies, and workflows.
3. Use lowercase kebab-case for all tags and categories.
4. Prefer explicit terms over ambiguous shorthand.

## Categories

Current category clusters in use:

- development
- eventities
- experiments
- iiif
- instructional
- news
- posts
- rerum
- technology
- tpen
- tradamus
- transcription

Notes:

- `eventities` is intentional and should be preserved.
- Categories are allowed to co-occur when a post spans multiple clusters.

## Tag Normalization Rules

Use these preferred forms when editing or creating posts:

- linked-data-notification (instead of `ldn`)
- open-data (instead of `open`)
- text-analysis (instead of generic `text`)

## Common Tag Clusters

Platform and ecosystem:

- rerum
- tpen-2-8
- tpen-3-0
- mirador
- tradamus

Standards and data model:

- iiif
- web-annotation
- linked-data-notification
- geojson
- geojson-ld
- geolocation

Workflow and implementation:

- authentication
- authorization
- versioning
- ux
- interface
- services

Domain/content focus:

- transcription
- manuscripts
- word-list
- text-analysis

## Authoring Checklist

For each new post front matter:

1. Add at least 1 category.
2. Add 3 to 6 tags.
3. Reuse existing tags when possible before inventing new ones.
4. If introducing a new tag, prefer specific, reusable wording.
