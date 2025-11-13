# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file, client-side web application for batch image optimization. The entire application is contained in `web-image-optimizer.html` - a standalone HTML file with embedded CSS and JavaScript.

## Architecture

### Core Technology Stack
- **Frontend**: Vanilla JavaScript (no build tools or frameworks)
- **Image Processing**: Compressor.js library (via CDN)
- **Storage API**: File System Access API (Chrome/Edge/Opera only)

### Key Components

The application is structured as a single HTML file containing three main sections:

1. **Styles (lines 8-431)**: Complete CSS styling with responsive design
2. **HTML Structure (lines 433-570)**: UI layout with sections for input/output selection, presets, options, progress tracking, and reporting
3. **JavaScript Logic (lines 572-914)**: All application functionality

### Core Functionality Flow

1. **Folder Selection** (`selectInputFolder`, `selectOutputFolder`):
   - Uses File System Access API to request folder permissions
   - `scanFolder` recursively finds all image files in input directory
   - Maintains folder structure information for each file

2. **Image Processing** (`processImages`):
   - Iterates through all discovered images sequentially
   - For each image:
     - Compresses using Compressor.js with user-specified settings
     - Saves to output folder (maintaining or flattening directory structure)
     - Tracks processing results (original size, optimized size, savings, timing)

3. **Compression** (`compressImage`):
   - Wraps Compressor.js in a Promise for async/await compatibility
   - Applies quality, dimensions, format conversion, and metadata stripping
   - Returns optimized Blob

4. **File Saving** (`saveCompressedImage`):
   - Recreates directory structure in output folder if requested
   - Uses FileSystemDirectoryHandle API to create nested directories
   - Writes compressed blob to file

5. **Reporting** (`displayReport`):
   - Calculates aggregate statistics (total savings, compression ratios)
   - Sorts results by compression efficiency
   - Provides CSV and JSON export options

### Data Structures

- **`imageFiles`**: Array of `{file, name, path}` objects representing input images
- **`processedResults`**: Array of processing results with metrics:
  - `name`, `path`: File identification
  - `originalSize`, `optimizedSize`, `savings`, `savingsPercent`: Size metrics
  - `processingTime`: Performance timing
  - `status`: 'success' or 'error'
  - `error`: Error message if failed

### Optimization Presets

Five presets are defined in the `presets` object (lines 578-584):
- **thumbnail**: 400px, 0.7 quality
- **mobile**: 768px, 0.75 quality
- **tablet**: 1024px, 0.8 quality
- **desktop**: 1920px, 0.8 quality
- **hero**: 2560px, 0.85 quality

### Format Comparison Feature

The application supports generating images in all three formats (WebP, JPEG, PNG) simultaneously for comparison:
- When "Generate all formats" checkbox is enabled, each input image is processed three times
- Output files are organized into format-specific subfolders: `webp/`, `jpeg/`, `png/`
- The report displays all format variants with color-coded badges (blue for WebP, orange for JPEG, purple for PNG)
- Results are sorted by compression ratio to identify the most efficient format for each image
- Total optimized size includes all format variants when in comparison mode

## Browser Compatibility

The application requires the File System Access API, which is only available in:
- Chrome 86+
- Edge 86+
- Opera 72+

The application includes runtime detection (lines 900-913) that displays an error if the API is unavailable.

## Running the Application

Simply open `web-image-optimizer.html` in a supported browser - no build step, server, or installation required.

## Testing the Application

Since this is a client-side only application with no build process:
- Manual testing in Chrome/Edge/Opera is the primary verification method
- Test with various image formats (JPEG, PNG, WebP)
- Test with nested folder structures to verify path handling
- Verify File System Access API permissions work correctly

## Key Implementation Details

### File System Access API Usage
- Requires user gesture to trigger `showDirectoryPicker()`
- `mode: 'read'` for input, `mode: 'readwrite'` for output
- Directory handles persist for the session but not across page reloads

### Async Iteration Pattern
The `scanFolder` function uses `for await...of` to iterate through directory entries:
```javascript
for await (const entry of dirHandle.values()) {
    // Process files and recurse into subdirectories
}
```

### Path Handling
- Relative paths are maintained as strings during scanning
- Paths are split and used to recreate directory structure in output
- File extensions are replaced based on output format selection

### Error Handling
- Try-catch blocks around folder selection handle AbortError (user cancellation)
- Individual image processing errors are caught and logged in results
- Failed images are marked but don't stop batch processing
