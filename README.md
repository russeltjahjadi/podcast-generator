# Podcast Generator

A GitHub Action that generates an RSS podcast feed from a YAML configuration file. This action reads your podcast metadata and episodes defined in `feed.yaml`, then produces a standard-compliant `podcast.xml` file ready for distribution to podcast directories and hosting platforms.

## Features

- **YAML-based Configuration**: Define your podcast metadata and episodes in a simple, human-readable YAML format
- **iTunes Podcast Support**: Generates RSS feeds with iTunes-specific tags for maximum compatibility with podcast directories
- **Automated Feed Generation**: Automatically runs on push events to keep your feed up to date
- **Docker-based**: Runs in a containerized environment for consistency across platforms

## About This Action

This action is designed to work in your podcast repository to automate the generation of your RSS feed. When you push changes to your `feed.yaml` file, this action will regenerate your `podcast.xml`, which can then be committed back to your repository or used directly for distribution.

## Prerequisites

Your repository should have the following structure:

```
podcast-test/
├── feed.yaml          # Your podcast configuration and episode definitions
├── audio/             # Directory containing episode audio files
├── images/            # Directory containing podcast artwork
└── podcast.xml        # Generated RSS feed (created by this action)
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `email` | true | `${{ github.actor }}@localhost` | The git committer's email address |
| `name` | true | `${{ github.actor }}` | The git committer's name |



### Feed Metadata

- **title**: Your podcast name
- **subtitle**: Short tagline for your podcast
- **author**: Podcast creator/host name
- **description**: Detailed description of your podcast
- **link**: Base URL where your podcast feed will be published
- **image**: Path to your podcast artwork (relative path prefixed with link)
- **language**: Language code (e.g., `en-us`)
- **category**: iTunes category (e.g., Technology, Arts, Business, etc.)
- **format**: Audio format (typically `audio/mpeg` for MP3)

### Episode Items

Each episode must include:

- **title**: Episode name
- **description**: Episode summary
- **published**: Publication date in RFC 2822 format (e.g., `Wed, 01 Jan 2024 12:00:00 GMT`)
- **duration**: Episode duration in `HH:MM:SS` format
- **file**: Path to the audio file (relative, will be prefixed with link)
- **length**: File size in bytes

## What Gets Generated

This action generates `podcast.xml`, a standard-compliant RSS feed that includes:

- All podcast metadata with iTunes-specific tags
- Episode information with proper enclosure elements for audio files
- Proper XML formatting and encoding

The generated feed can be:
- Published directly as your podcast RSS URL
- Submitted to podcast directories (Apple Podcasts, Spotify, Google Podcasts, etc.)
- Used by podcast hosting platforms

## Requirements

- Python 3.8+
- PyYAML library
- Docker (for local testing)

## Local Development

To run the feed generator locally:

```bash
pip install pyyaml
python feed.py
```

This will read `feed.yaml` and generate `podcast.xml` in the current directory.

## Related Project

This action is used by the [podcast-test](https://github.com/russeltjahjadi/podcast-test) repository as an example of how to integrate podcast feed generation into a GitHub workflow.

## License

This project is provided as-is for generating podcast RSS feeds from YAML definitions.