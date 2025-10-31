# YouTube Looper

A feature-rich single-page web application that allows users to loop any section of a YouTube video between two custom time points, save favorite clips, and manage a collection of loops.

## Overview

Created: October 31, 2025
Last Updated: October 31, 2025

This is a pure HTML/CSS/JavaScript application with no frameworks or dependencies. It uses the YouTube IFrame Player API to embed and control video playback with custom loop points, localStorage for persistence, and includes comprehensive security features.

## Features

### Core Functionality
- **YouTube URL Input**: Paste any YouTube URL and the app automatically extracts the video ID
- **Custom Time Points**: Set start and end times in seconds (supports decimals)
- **Automatic Looping**: Video seamlessly loops between the specified time points
- **Video Titles**: Automatically fetches and displays video titles using YouTube API
- **Fullscreen Mode**: Cross-browser fullscreen support with vendor-prefixed APIs

### Persistence & Storage
- **Auto-Save Form Data**: URL and time values automatically saved to localStorage as you type
- **Auto-Restore**: Previously entered values restored on page load
- **Saved Clips List**: Build a collection of your favorite video loops
- **Export/Import**: Save and load clip collections as JSON files

### Clip Management
- **Save to List**: Add current video and loop points to saved clips
- **Play Clip**: One-click playback of any saved clip
- **Delete Clip**: Remove individual clips from the list
- **Clear All**: Remove all saved clips with confirmation dialog
- **Clip Metadata**: Each clip shows title, time range, and duration

### User Interface
- **Clean Design**: Minimalist interface with gradient background and card layout
- **Modern Typography**: System sans-serif font stack for consistency
- **Responsive Layout**: Grid and flexbox for adaptive design
- **Status Messages**: Auto-hiding feedback messages (3 second timeout)
- **Empty States**: Helpful messages when lists are empty

## Security Features

### XSS Protection
- **Input Sanitization**: All imported data is validated and type-coerced
- **HTML Escaping**: All user-generated content is escaped before rendering
- **Import Validation**: JSON imports are thoroughly validated for structure and types
- **Safe Rendering**: Numeric fields validated with parseFloat/parseInt to prevent injection

### Cross-Browser Compatibility
- **Fullscreen API**: Supports all vendor prefixes (webkit, moz, ms, standard)
- **API Race Condition Handling**: Queues operations until YouTube API loads
- **Timeout Management**: Prevents overlapping loop timers

## Technical Details

### Architecture
- **Single File**: All HTML, CSS, and JavaScript in `index.html`
- **YouTube IFrame API**: Asynchronously loaded for video control
- **localStorage**: Used for persistence (better than cookies for structured data)
- **Pure Vanilla JS**: No frameworks, no build tools, no dependencies

### Data Structure
```javascript
{
  id: Number,           // Unique timestamp-based ID
  url: String,          // Full YouTube URL
  videoId: String,      // Extracted video ID
  title: String,        // Video title from YouTube API
  startTime: Number,    // Start time in seconds
  endTime: Number,      // End time in seconds
  duration: Number      // Loop duration (endTime - startTime)
}
```

### Key Implementation Details
- Video ID extraction supports multiple YouTube URL formats
- API ready flag prevents race conditions when clicking buttons before API loads
- Timeout management prevents overlapping loop timers
- Player state monitoring ensures accurate loop timing
- Comprehensive validation on import to prevent malformed data

## File Structure

```
.
├── index.html          # Main application file (HTML, CSS, JS)
├── replit.md           # This documentation file
└── .gitignore          # Git ignore patterns
```

## How to Use

### Basic Looping
1. Paste a YouTube URL into the input field
2. Enter start time in seconds (e.g., 50.95)
3. Enter end time in seconds (e.g., 54.5)
4. Click "Load & Loop"
5. The video will play and loop between your specified times

### Saving Clips
1. Set up a loop as described above
2. Click "Save to List" (green button)
3. The current video and loop points are saved
4. Clip appears in the "Saved Clips" section below

### Managing Clips
- **Play**: Click the "▶ Play" button next to any clip to load and play it
- **Delete**: Click the "✕" button to remove a clip
- **Clear All**: Click the red "🗑️ Clear All" button to remove all clips (with confirmation)

### Exporting & Importing
- **Save List**: Click "💾 Save List" to download clips as JSON
- **Load List**: Click "📂 Load List" to import clips from a JSON file
- Files are named with the current date (e.g., `youtube-loops-2025-10-31.json`)

### Fullscreen
- Click the "⛶ Fullscreen" button on the video player
- Works across all major browsers (Chrome, Firefox, Safari, Edge)
- Click again (or press ESC) to exit fullscreen

## Development

The app is served using Python's built-in HTTP server on port 5000.

### Workflow
- **Name**: webserver
- **Command**: `python -m http.server 5000`
- **Output**: webview on port 5000

### Testing
- Form data persistence: Enter values and reload page
- Clip saving: Save clips and verify they appear in the list
- Import/Export: Export clips, clear all, then import to restore
- Fullscreen: Test across different browsers
- XSS Prevention: Try importing malformed JSON to verify validation

## Browser Compatibility

- **Modern Browsers**: Chrome, Firefox, Safari, Edge (full support)
- **Legacy Support**: IE11 (with vendor prefixes)
- **Mobile**: iOS Safari, Chrome Mobile (fullscreen may vary by device)

## Security Considerations

- All imported data is validated and sanitized
- HTML escaping prevents XSS attacks
- No external dependencies reduce attack surface
- localStorage is domain-isolated
- No backend = no server-side vulnerabilities

## Design Choices

### Why localStorage instead of cookies?
- Better for structured data (JSON)
- Larger storage capacity (5-10MB vs 4KB)
- Simpler API for JavaScript
- Automatic domain isolation

### Why single HTML file?
- Simplicity and portability
- No build process required
- Easy to understand and modify
- Perfect for learning/prototyping

### Why JSON for export?
- Human-readable and editable
- Easy to share and version control
- Native JavaScript support
- Future-proof format

## Future Enhancement Ideas

- Visual timeline scrubber for selecting loop points
- Keyboard shortcuts (Space for play/pause, etc.)
- Multiple simultaneous loops
- Playlist mode (auto-advance through clips)
- Share clips via URL parameters
- Dark mode toggle
- Custom keyboard shortcuts per clip
- Volume and playback speed controls
- Tags/categories for organizing clips
