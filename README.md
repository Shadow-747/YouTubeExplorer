https://github.com/Shadow-747/YouTubeExplorer/releases

[![Releases](https://img.shields.io/badge/YouTubeExplorer-Downloads-blue?logo=github&logoColor=white)](https://github.com/Shadow-747/YouTubeExplorer/releases)

# YouTube Explorer: Unofficial Comments Search, Filter & Analysis Tool

A practical, open tool for searching, filtering, and displaying YouTube video comments by keywords using the YouTube Data API v3. It runs in the terminal and aims to be straightforward to use, fast to operate, and easy to extend. This project emphasizes clarity, reliable behavior, and transparent data handling. It combines a robust data pipeline with simple command line controls so developers, researchers, and hobbyists can explore comment data with minimal setup.

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Roadmap and Goals](#roadmap-and-goals)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage Guide](#usage-guide)
- [Working with Keywords](#working-with-keywords)
- [Comment Extraction](#comment-extraction)
- [Text Analysis](#text-analysis)
- [Filtering Mechanisms](#filtering-mechanisms)
- [Command Line Interface](#command-line-interface)
- [Examples](#examples)
- [Output and Formats](#output-and-formats)
- [Data Flow and Architecture](#data-flow-and-architecture)
- [Performance and Monitoring](#performance-and-monitoring)
- [Error Handling](#error-handling)
- [Security and Privacy](#security-and-privacy)
- [Testing and Quality Assurance](#testing-and-quality-assurance)
- [Development and Contribution](#development-and-contribution)
- [Documentation and Help](#documentation-and-help)
- [Changelog](#changelog)
- [Releases](#releases)
- [Credits and License](#credits-and-license)

---

## Overview

YouTube Explorer is an unofficial tool designed to help you search YouTube video comments by keywords, filter the results, and display findings clearly. It uses the YouTube Data API v3 under the hood and relies on the Google API Python client for access. The app is a terminal program, built to be dependable for scripting, research, or quick investigations into comment content. It supports keyword-based filtering, content-based filters, and basic text analysis to surface meaningful patterns in large sets of comments.

The project is designed with three core ideas in mind:

- Simplicity: a clean command line interface with predictable behavior.
- Extensibility: modular components you can replace or extend.
- Responsibility: clear handling of API quotas, rate limits, and privacy considerations.

The repository topics reflect its scope across API integration, comment extraction, content filtering, keyword filtering, Python, and YouTube tooling. It serves as a practical base for anyone who wants to learn how to work with YouTube comments programmatically while keeping control over what to extract and how to present it.

---

## Key Features

- Keyword-based search of YouTube video comments
- Filtering by content quality, sentiment hints, or profanity checks
- Display of results with metadata like author, timestamp, and like count
- Support for multiple videos in a single run
- Lightweight, terminal-based UI that works on Windows, macOS, and Linux
- Optional text analysis helpers to summarize topics and themes
- Easy-to-use CLI with sensible defaults
- Clear logs and progress indicators to monitor long runs
- Lightweight dependency footprint with widely used libraries

This feature set makes YouTube Explorer suitable for researchers, educators, content teams, and curious developers who want to inspect discussion around YouTube videos without building a full browser-based tool.

---

## Roadmap and Goals

- Improve keyword matching with case-insensitive checks and Unicode normalization
- Add more robust text analysis modules, including basic topic modeling
- Introduce per-video quotas guidance and quota-aware scheduling
- Expand export options to CSV, JSON Lines, and Markdown tables
- Improve language support with multilingual keyword filtering
- Provide optional OAuth-based access for cases requiring user-specific data
- Create a plug-in hub for extra filters and analyzers
- Enhance error reporting with actionable messages and retry strategies

The roadmap aims to keep the project practical while allowing growth if the community shows interest. You can track progress in the Releases section. See the releases page for the latest assets and notes.

Releases page for downloads and assets: https://github.com/Shadow-747/YouTubeExplorer/releases

Note: If the link doesn’t load, check the Releases section on the repository to find the latest assets and installation instructions.

---

## Prerequisites

Before installing YouTube Explorer, gather a few essentials. The tool is built with Python and uses the Google API Python Client to interact with the YouTube Data API v3. You should have:

- A modern system with Python 3.8 or newer
- pip for Python package installation
- A YouTube Data API v3 API key (or OAuth credentials for user-specific access)
- Basic command line experience
- A stable internet connection for initial setup and data fetching

Optional but recommended:

- A basic virtual environment setup (venv or conda) to isolate dependencies
- A terminal or shell with proper color support for readable output

It helps to know how to install dependencies from a requirements file and how to set environment variables for API keys. If you plan to work with multiple videos, ensure you have enough quota on your API key, as YouTube Data API v3 usage counts toward your quota.

---

## Installation

YouTube Explorer ships with a straightforward installation flow. The goal is to get you up and running quickly while keeping the setup transparent and stable.

1. Prepare your environment
   - Install Python 3.8+ from the official source or your OS package manager.
   - Ensure you can run python and pip from the command line.

2. Create a virtual environment (optional but recommended)
   - On Windows: python -m venv venv
   - On macOS/Linux: python3 -m venv venv
   - Activate the environment:
     - Windows: venv\Scripts\activate
     - macOS/Linux: source venv/bin/activate

3. Install dependencies
   - pip install -r requirements.txt
   - The project uses the google-api-python-client for YouTube Data API access and a handful of text-processing libraries for keyword matching and analysis.

4. Configure API credentials
   - Obtain a YouTube Data API v3 key from Google Cloud Console
   - Set the API key as an environment variable or pass it through a config file
   - Common names: YT_API_KEY, YOUTUBE_API_KEY, or API_KEY

5. Run the tool
   - The CLI provides a set of commands for video selection, keyword filtering, and output formatting
   - Example: youTube-explorer --video-id dQw4w9WgXcQ --keywords "music, nostalgia" --limit 100

6. Access the releases page for installers and assets
   - See the link at the beginning of this document for quick access to the latest releases. For a direct download, visit the releases page and grab the installer or packaged artifacts that match your operating system. https://github.com/Shadow-747/YouTubeExplorer/releases

If you need step-by-step guidance for a specific OS, a fuller guide is provided in the Documentation section below.

---

## Configuration

The tool uses a combination of environment variables and a simple config file to control its behavior. This makes it easy to automate runs or tailor the setup for different projects.

- API key management
  - Environment variable: YOUTUBE_API_KEY
  - Fallback: a config.yml file with an api_key field

- Video selection
  - video_id: the YouTube video you want to inspect
  - playlist_id: optional if you want to analyze a playlist instead of a single video
  - max_results: number of comments to fetch per video (respect quotas)

- Filtering rules
  - keywords: a list of keywords to match against comments
  - min_throughput: a threshold for how often a keyword must appear to be included
  - language: constrain to a particular language code, if supported

- Output
  - format: json, jsonl, or markdown
  - output_file: path to save results
  - verbose: enable detailed logs

- Logging and monitoring
  - log_file: path to a log file
  - log_level: info, warning, error

- Localization and language support
  - locale: language/locale for text normalization
  - tokenization rules: optional tweaks to how text is split

- Privacy and data handling
  - opt_out_share: disable any data sharing for non-essential operations
  - anonymize_user_ids: replace user IDs with anonymized tokens for privacy

Config files give you a reproducible setup. You can share a single config across runs or keep per-project configurations. The key is to keep credentials secure and not commit them to version control.

---

## Usage Guide

This guide covers common tasks you will perform with YouTube Explorer. It emphasizes practical workflows that let you extract meaningful comment data quickly and reliably.

- Quick start
  - Get a video ready for analysis by providing its ID
  - Provide one or more keywords to search for in comments
  - Run a single-pass fetch and filter to see initial results

- Multi-video workflows
  - You can analyze several videos in a single run
  - Aggregate results by video, keyword, or tag
  - Produce a single report that contains all findings or split reports per video

- Filter strategies
  - Simple keyword matching: filter comments that contain at least one keyword
  - Phrase matching: enforce exact phrases to improve relevance
  - Proximity filtering: find comments where keywords appear close to each other
  - Sentiment hints: optionally flag comments with positive or negative cues

- Exporting results
  - Output as JSON for programmatic processing
  - Output as Markdown for easy sharing in docs or notes
  - Output as CSV/TSV for spreadsheet analysis

- Scheduling and automation
  - Use cron or task schedulers to run routines at set times
  - Combine with other data sources to build richer reports

- Error handling and retries
  - If a request hits a quota limit, the tool will back off and retry
  - If a temporary network error occurs, the tool will retry after a short delay
  - Clear error messages guide you toward resolution

- Debugging tips
  - Run with verbose logging to capture API responses
  - Verify your API key is valid and has access to YouTube Data API v3
  - Check your quota usage in the Google Cloud Console

The usage guide aims to be practical and concise. If you want more detail, consult the API reference and the internal module docs that accompany the codebase.

---

## Working with Keywords

Keywords drive the core search and filtering process. They should be chosen to maximize signal while minimizing noise. Here are practical tips for selecting keywords and building robust keyword sets:

- Start with a core list of terms tied to your research question or content focus
- Include synonyms and common misspellings to improve capture
- Use exact phrases for precise matching when you need tight relevance
- Combine keywords with logical operators to implement complex filters
- Consider languages and encodings; ensure your keywords handle unicode characters
- Maintain a separate keyword file for large projects and load it at runtime

Keyword lists can be stored in a plain text or YAML file. The tool reads these lists at startup and prepares the matching rules. You can update the lists between runs without changing code, which makes it easy to experiment.

---

## Comment Extraction

The extraction phase fetches comments from the YouTube Data API v3 and prepares them for filtering. This part of the pipeline is designed to be robust and predictable:

- Fetch comments from one or more videos
- Normalize text to reduce case sensitivity and punctuation noise
- Preserve essential metadata: author, time, like count, and reply status
- Apply content filters to exclude irrelevant comments
- Pass the filtered comments to the analysis stage for further processing

Extraction respects the API quotas and adheres to best practices to avoid excessive requests. The code uses careful batching to stay within limits while maintaining speed.

---

## Text Analysis

Text analysis turns raw comment data into insights. This module focuses on practical, actionable results rather than theoretical metrics. Core capabilities include:

- Tokenization and normalization (lowercasing, Unicode normalization)
- Keyword scoring and relevance ranking
- Basic sentiment hints using rule-based heuristics
- Stop-word filtering to reduce noise
- Topic tagging based on frequent keyword co-occurrence
- Optional summarization for long comment threads

The emphasis is on speed and clarity. The analysis results should be easy to interpret in reports or dashboards.

---

## Filtering Mechanisms

Filtering is central to the tool. It helps you keep only the comments that matter. The available mechanisms include:

- Keyword matching: presence of one or more keywords
- Phrase matching: exact sequences of words
- Proximity checks: keywords appearing near each other in the same comment
- Language filtering: comments in a target language
- Quality filters: length and content quality heuristics
- Spam and repetition checks: simple deduplication and repetition tests
- Custom filters: user-defined Python functions can be plugged into the pipeline

Filters are designed to be composable. You can stack several filters to create precise rules for your data.

---

## Command Line Interface

The interface is designed for clarity. It uses short, descriptive flags and sensible defaults. Common commands include:

- Start a session for a single video
  - youTube-explorer --video-id VIDEO_ID --keywords "term1, term2" --limit 200
- Analyze a playlist
  - youTube-explorer --playlist-id PLAYLIST_ID --keywords "term" --max-pages 5
- Export results
  - youTube-explorer --video-id VIDEO_ID --output results.json
- List available videos and their IDs
  - youTube-explorer --list-videos --channel-id CHANNEL_ID
- Dry run to validate configuration without API calls
  - youTube-explorer --video-id VIDEO_ID --keywords "term" --dry-run

The CLI is intentionally forgiving. If inputs are missing, the tool will guide you with helpful prompts. You can combine multiple flags for more complex queries.

---

## Examples

- Example 1: Simple keyword search on a single video
  - Command: youTube-explorer --video-id dQw4w9WgXcQ --keywords "nostalgia, 80s" --limit 100
  - Result: A JSON file (or Markdown) with matching comments, including author and timestamp.

- Example 2: Analyze a playlist with multiple keywords and export as Markdown
  - Command: youTube-explorer --playlist-id PL12345 --keywords "music, dance" --format markdown --output playlist_report.md
  - Result: A markdown table with comments by video, ranked by keyword relevance.

- Example 3: Quick health check
  - Command: youTube-explorer --video-id dQw4w9WgXcQ --dry-run
  - Result: A summary of what would be fetched and which filters would apply.

These examples show typical usage patterns. You can adapt them to your project needs.

---

## Output and Formats

YouTube Explorer supports several output formats to suit different workflows:

- JSON: Structured, easy to parse with code
- JSON Lines (JSONL): One object per line, suitable for streaming
- Markdown: Readable in docs and notes
- CSV/TSV: Easy to import into spreadsheets or BI tools

Each output includes core fields like comment_id, author, text, published_at, like_count, video_id, and the applied filters. Some optional fields may be included for context, such as keywords matched and analysis scores.

You can customize the fields included in the output by adjusting the configuration. The default is a compact, actionable set of fields that cover most needs.

---

## Data Flow and Architecture

The tool follows a clean, modular data flow. Each stage is designed to be tested independently and replaced if needed.

1. Input handling
   - Collect video IDs, playlist IDs, and keywords from the user
   - Validate inputs and prepare API requests
2. Comment retrieval
   - Fetch comments via YouTube Data API v3
   - Batch requests to stay within quotas
   - Normalize text for consistent processing
3. Filtering
   - Apply keyword and content filters
   - Remove duplicates and obvious spam
4. Text analysis
   - Tokenize and normalize text
   - Score relevance and surface topics
5. Output generation
   - Format results into the chosen output format
   - Save to a file or stdout for piping into other tools
6. Logging and metrics
   - Record processing times and quota usage
   - Emit warnings for potential issues

The system is designed to be robust against API failures and network hiccups. It prioritizes clear failure modes and actionable error messages.

---

## Performance and Monitoring

Performance is important when working with large comment datasets. The tool uses batching and memoization to reduce repeated work. It also offers options to limit the number of results and to adjust how aggressively the API is queried.

- Batching: Requests are grouped to minimize overhead
- Caching: Frequently seen data can be reused within a session
- Quota awareness: The tool monitors quota usage and backs off when approaching limits
- Progress feedback: Real-time progress bars and status messages help you stay informed
- Resource usage: The program keeps memory usage in check and cleans up after runs

For long runs, consider running in a screen or tmux session to avoid interruptions.

---

## Error Handling

Error handling is designed to be straightforward. When something goes wrong, you will see:

- A clear error message describing the problem
- An error code or type to help you diagnose the issue
- Suggested steps to fix or retry
- Information about quota or temporary API issues if relevant

The goal is to help you recover quickly without losing context from the run. If an error is transient, the tool will retry with backoff.

---

## Security and Privacy

The tool interacts with public YouTube comments via the YouTube Data API v3. It does not collect personal data beyond what you fetch, and it does not publish data unless you choose to export it. If you enable anonymization, user identifiers will be replaced with tokens for privacy reasons. It is your responsibility to handle and store data in a compliant manner for your use case.

- API keys should be stored securely and not committed to source control
- Use per-project credentials when possible
- Review data handling policies if you plan to share results publicly

---

## Testing and Quality Assurance

Quality checks help keep the project reliable. The testing strategy includes:

- Unit tests for individual modules, such as keyword matching and text normalization
- Integration tests for API interactions with mocked responses
- End-to-end tests for common user workflows via the CLI
- Performance tests to assess batch processing and quota usage
- Linting and formatting checks to maintain code quality

You can run tests via the provided test suite and verify that changes do not regress behavior.

---

## Development and Contribution

You are welcome to contribute to this project. The code is organized into clear modules that map to core concepts:

- api_client: Handles YouTube Data API v3 requests
- comment_extractor: Fetches and normalizes comments
- keyword_filtering: Applies keyword-based filters
- content_filtering: Applies quality and content-based filters
- text_analysis: Performs tokenization, normalization, and scoring
- cli: Command line interface and argument parsing
- exports: Output formatting and serialization

If you want to contribute, follow these steps:

- Open an issue to discuss the change
- Create a feature branch off of main
- Write tests for your changes
- Run the test suite and fix any issues
- Submit a pull request with a clear description

Your pull requests should include:

- A summary of the change
- Rationale and potential impact
- How to test the change
- Any known caveats or limitations

You can review the releases page for the latest assets and notes, and you can fork the repository to start your own work.

Releases page for downloads and assets: https://github.com/Shadow-747/YouTubeExplorer/releases

If the link is not loading, check the Releases section for the latest assets and installation instructions.

---

## Documentation and Help

- Project documentation lives in the docs directory. It covers installation, configuration, and usage in more depth.
- API references describe the request shapes, response parsing, and error codes from the YouTube Data API v3.
- The CLI reference lists all commands, flags, and examples.
- A contribution guide provides coding standards, testing procedures, and how to run the project locally.
- AFAQ (frequently asked questions) covers common gotchas and troubleshooting steps.

If you need more help, you can open an issue to ask for guidance or search the existing issues for similar topics.

---

## Changelog

- v1.0.x: Initial release with core CLI features, keyword filtering, and simple output formats
- v1.1.x: Added playlist support, improved tokenization, and extended output options
- v1.2.x: Introduced basic sentiment hints, error handling improvements, and performance tweaks
- v1.3.x: Enhanced quota management, added anonymization options, and more robust filtering
- v1.4.x: UI refinements, more export formats, and better logging
- v1.5.x: Documentation updates, test suite improvements, and API usage refinements

Changelog entries help users understand the evolution of the tool and what to expect when upgrading.

---

## Re releases

The project uses GitHub Releases to distribute binaries, installers, and packaged artifacts. You can download the latest release from the releases page and run the installer appropriate for your environment. The link above is the primary source for these assets. If the link does not load, visit the Releases section on the repository to locate the latest assets and instructions.

Releases page for downloads and assets: https://github.com/Shadow-747/YouTubeExplorer/releases

---

## Credits and License

- Core contributors and testers who helped shape the project
- Open source libraries used for API interactions, parsing, and utilities
- The license for the project is intended to be permissive and community-friendly. Check the LICENSE file in the repository for the exact terms.

Thank you for exploring YouTube Explorer. This project focuses on clarity, reliability, and practical utility for anyone who wants to work with YouTube comments in a programmatic, repeatable way.