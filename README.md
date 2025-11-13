# Web Image Optimizer

A powerful, client-side web application for batch image optimization and compression. Process multiple images at once with customizable presets, format conversion, and detailed reporting - all running directly in your browser with no server required.

**[🚀 Try it Live](https://crypto69.github.io/web-image-optimizer/web-image-optimizer.html)**

![Web Image Optimizer UI](images/Web%20image%20optimise.png)

## Features

### Batch Processing
- Process entire folders of images recursively
- Maintain or flatten directory structure in output
- Real-time progress tracking with percentage indicators
- Individual file processing metrics

### Optimization Presets
Choose from 6 built-in presets optimized for different use cases:
- **Thumbnail** (400px, 70% quality) - Perfect for small previews
- **Mobile** (768px, 75% quality) - Mobile-friendly images
- **Tablet** (1024px, 80% quality) - Tablet displays
- **Desktop** (1920px, 80% quality) - Full HD screens
- **Hero** (2560px, 85% quality) - Large banner images
- **Custom** - Define your own dimensions and quality settings

### Advanced Options
- **Format Conversion**: Convert to WebP, JPEG, or PNG
- **Quality Control**: Fine-tune compression (0.1 - 1.0 scale)
- **Dimension Control**: Set maximum width and height
- **Metadata Stripping**: Remove EXIF data to reduce file size
- **Format Comparison**: Generate all three formats simultaneously to compare compression efficiency

### Detailed Reporting
After processing, get comprehensive analytics:
- Total images processed
- Original vs. optimized size
- Total space savings (MB and %)
- Per-image breakdown with:
  - File path and name
  - Format badge (color-coded)
  - Size reduction
  - Compression percentage
  - Processing time
  - Status (success/error)

![Processing Report](images/Web%20optimise%20report.png)

### Export Options
- **CSV Export**: Download results as spreadsheet
- **JSON Export**: Get structured data for further analysis

## Browser Compatibility

This application uses the File System Access API and requires:
- **Chrome** 86+
- **Edge** 86+
- **Opera** 72+

⚠️ **Note**: Firefox and Safari do not currently support the File System Access API.

## How to Use

1. **Download**: Save the `web-image-optimizer.html` file to your computer
2. **Open**: Double-click the file to open it in a supported browser (Chrome/Edge/Opera)
3. **Select Input Folder**: Click "Select Input Folder" and choose your source images directory
4. **Select Output Folder**: Click "Select Output Folder" and choose where optimized images should be saved
5. **Choose Preset**: Select a preset or customize your own settings
6. **Configure Options**:
   - Choose output format (WebP recommended for best compression)
   - Adjust quality and dimensions if using custom preset
   - Toggle metadata stripping
   - Enable "Generate all formats" for comparison mode
7. **Process**: Click "Optimize Images" and watch the progress
8. **Review Report**: Analyze results and download CSV/JSON if needed

## Technical Details

### Architecture
- **Single-file application**: No installation, build tools, or frameworks required
- **Vanilla JavaScript**: Pure ES6+ with no external dependencies except Compressor.js
- **Client-side processing**: All image compression happens in your browser - images never leave your computer
- **Zero backend**: No server, no upload, 100% local processing

### Technology Stack
- **HTML5/CSS3**: Responsive UI with gradient backgrounds
- **JavaScript (ES6+)**: Modern async/await patterns
- **Compressor.js**: Image compression library (v1.2.1 via CDN)
- **File System Access API**: Native folder access for batch processing

### Key Capabilities
- Recursive folder scanning
- Maintains directory structure in output (optional)
- Sequential image processing with error handling
- Format-specific subfolder organization in comparison mode
- Real-time progress updates
- Comprehensive error logging

## Installation

No installation required! Simply:

1. Download `web-image-optimizer.html`
2. Open it in Chrome, Edge, or Opera
3. Start optimizing images

That's it - no npm install, no build process, no dependencies to manage.

## Privacy & Security

- **100% Local Processing**: All image processing happens in your browser
- **No Upload**: Images are never sent to any server
- **No Tracking**: No analytics, no cookies, no data collection
- **Open Source**: View the source code directly in the HTML file

## Format Comparison Mode

When enabled, the application generates WebP, JPEG, and PNG versions of each image:
- Output organized into `webp/`, `jpeg/`, `png/` subfolders
- Report shows all format variants with color-coded badges
- Results sorted by compression efficiency
- Helps identify the best format for each specific image

## Use Cases

- **Web Development**: Optimize images before deployment
- **Content Creation**: Prepare images for blogs, social media, or websites
- **Photography**: Reduce file sizes while maintaining quality
- **E-commerce**: Batch process product images
- **Digital Assets**: Organize and compress media libraries
- **Performance Testing**: Compare format efficiency across different images

## Contributing

Contributions are welcome! This is a single-file application, so modifications are straightforward:

1. Fork the repository
2. Make your changes to `web-image-optimizer.html`
3. Test in Chrome/Edge/Opera
4. Submit a pull request

## License

MIT License - Feel free to use, modify, and distribute.

## Acknowledgments

- **Compressor.js** by fengyuanchen - Excellent image compression library
- **File System Access API** - Modern browser capability for local file handling

---

**Made with ❤️ for the web development community**

Need help? Found a bug? [Open an issue](../../issues) on GitHub!