# YouTube Looper

A minimal single-page web application that allows users to loop any section of a YouTube video between two custom time points.

## Overview

Created: October 31, 2025

This is a pure HTML/CSS/JavaScript application with no frameworks or dependencies. It uses the YouTube IFrame Player API to embed and control video playback with custom loop points.

## Features

- **YouTube URL Input**: Paste any YouTube URL and the app automatically extracts the video ID
- **Custom Time Points**: Set start and end times in seconds (supports decimals)
- **Automatic Looping**: Video seamlessly loops between the specified time points
- **Clean UI**: Minimalist design with gradient background, sans-serif typography, and good whitespace
- **Input Validation**: Validates URLs and ensures end time is greater than start time
- **API Race Condition Handling**: Queues video requests if YouTube API hasn't loaded yet

## Technical Details

### Architecture
- **Single File**: All HTML, CSS, and JavaScript in `index.html`
- **YouTube IFrame API**: Asynchronously loaded for video control
- **Pure Vanilla JS**: No frameworks, no build tools, no dependencies

### Key Implementation Details
- Video ID extraction supports multiple YouTube URL formats
- API ready flag prevents race conditions when clicking "Load & Loop" before API loads
- Timeout management prevents overlapping loop timers
- Player state monitoring ensures accurate loop timing

## File Structure

```
.
├── index.html          # Main application file (HTML, CSS, JS)
└── replit.md           # This documentation file
```

## How to Use

1. Paste a YouTube URL into the input field
2. Enter start time in seconds (e.g., 50.95)
3. Enter end time in seconds (e.g., 54.5)
4. Click "Load & Loop"
5. The video will play and loop between your specified times

## Development

The app is served using Python's built-in HTTP server on port 5000. The workflow automatically starts when the project runs.

### Workflow
- **Name**: webserver
- **Command**: `python -m http.server 5000`
- **Output**: webview on port 5000

## Design Choices

- **Compact Code**: All code in one file for simplicity
- **Well-Commented**: Clear documentation for all functions
- **Modern UI**: Gradient background, rounded corners, smooth transitions
- **Typography**: System sans-serif font stack for consistent cross-platform appearance
- **Responsive**: Grid layout for time inputs, flexbox for overall structure
