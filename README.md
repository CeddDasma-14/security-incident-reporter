# Security Incident Reporter

A comprehensive web-based tool for security operations teams to analyze security camera footage, generate formatted incident reports, and manage daily security summaries.

![Version](https://img.shields.io/badge/version-2.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)

## 🚀 Features 

### Core Functionality
- **📸 Multi-Image Upload** - Drag & drop or click to upload multiple security camera images
- **🔍 OCR Timestamp Extraction** - Automatically extracts timestamps from images using Tesseract.js
- **📝 Pre-filled Templates** - Quick access to common incident types (Tailgating, Overstaying, Unauthorized Access)
- **🎯 Auto-Priority Assignment** - P2 for incidents after 11 PM, P3 otherwise
- **📋 Formatted Report Generation** - Creates properly formatted incident reports

### Advanced Features (v2)
- **✏️ Image Annotation** - Draw directly on images to highlight areas of concern with adjustable colors and brush sizes
- **💾 Custom Templates** - Save and load frequently used action descriptions
- **📜 Report History** - Stores all reports from the current day using localStorage
- **📧 Email Draft Export** - One-click copy of formatted daily summary email with nested bullet structure
- **⚠️ Time Validation** - Warns about unusual dates (future dates or >7 days old)
- **🖥️ One-View Layout** - Optimized 3-panel design with no scrolling required

## 📋 Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Email Report Format](#email-report-format)
- [File Structure](#file-structure)
- [Browser Compatibility](#browser-compatibility)
- [Contributing](#contributing)

## 💻 Installation

### Option 1: Download and Use Locally
1. Download `security-incident-reporter-v2.html`
2. Open the file in any modern web browser (Chrome, Firefox, Edge recommended)
3. No installation or server required!

### Option 2: Host on Web Server
1. Upload the HTML file to your web server
2. Access via URL: `https://yourserver.com/security-incident-reporter-v2.html`

### Option 3: GitHub Pages (Free Hosting)
1. Fork this repository
2. Enable GitHub Pages in repository settings
3. Access via: `https://yourusername.github.io/security-incident-reporter/`

## 🎯 Usage

### Basic Workflow

1. **Select Property**
   - Choose from: The Reserve, The Harrison, The Hermitage
   - If "Reserve" is selected, additional location dropdown appears (E124, E125, etc.)

2. **Upload Images**
   - Drag & drop security camera screenshots
   - Or click the upload area to browse files
   - Multiple images supported - displayed in horizontal scrolling gallery

3. **Enter Incident Details**
   - **Date**: When the incident occurred
   - **Issue Type**: Select from dropdown or choose "Other" for custom
   - **Actions Observed**: Pre-filled based on issue type, or enter custom description

4. **Annotate Images (Optional)**
   - Click "✏️ Draw" button on any image
   - Draw to highlight areas of concern
   - Adjust color and brush size
   - Click "Save" to apply annotations

5. **Generate Report**
   - Click "Generate Report" button
   - Report appears in the output panel
   - Auto-generated filenames shown below
   - Click "Copy Report" to copy to clipboard

6. **Daily Summary**
   - All reports stored in History panel (right side)
   - Click any history item to view
   - Use "📧 Copy Email Draft" to copy formatted daily summary
   - Use "📊 Export Day Report" to download .txt file

### Custom Templates

**Save Template:**
1. Enter a description in "Actions Observed" field
2. Type a template name in the input field
3. Click "💾 Save Template"

**Use Template:**
- Click any saved template to auto-fill the "Actions Observed" field

**Delete Template:**
- Click "×" next to any template to remove it

## 📧 Email Report Format

The tool generates a properly formatted daily summary email:

```
SUBJECT: 
The Reserve, The Harrison & The Hermitage – Daily Overnight Summary – 02/15/2026

BODY:
Hello Team,

Please see below for the incident report:

The Reserve:

    • P2 - Tailgating - (At 9:12 PM, Lashawn Simmons entered with six individuals)
        ○ Location: E125 Main Door
        ○ Date & Time: 02/15/2026 9:12 PM
        ○ Action Taken: flagged, saved screenshot, monitoring, sent to reserve-security channel
        ○ Clip/Screenshot: Reserve_2026-02-15_E125_Main_Door.png
        ○ VA Name: 

The Harrison:

The Hermitage:
```

### Email Format Features:
- ✅ Subject line with yesterday's date (auto-calculated)
- ✅ Grouped by property (Reserve, Harrison, Hermitage)
- ✅ Nested bullet structure (• main, ○ sub-bullets)
- ✅ Multiple filenames separated by commas
- ✅ VA Name field blank for manual entry
- ✅ Single-spaced, copy-paste ready

## 📁 File Structure

```
security-incident-reporter/
├── README.md                              # This file
├── security-incident-reporter.html        # Original version
└── security-incident-reporter-v2.html     # Enhanced version with all features
```

## 🌐 Browser Compatibility

| Browser | Supported | Notes |
|---------|-----------|-------|
| Chrome  | ✅ Yes    | Recommended |
| Firefox | ✅ Yes    | Recommended |
| Edge    | ✅ Yes    | Recommended |
| Safari  | ✅ Yes    | May have minor styling differences |
| IE 11   | ❌ No     | Not supported |

**Requirements:**
- JavaScript enabled
- LocalStorage enabled (for history and templates)
- Internet connection (for OCR/Tesseract.js CDN)

## 🔧 Technical Details

### Dependencies
- **Tesseract.js v4** - OCR for timestamp extraction (loaded via CDN)
- No other external dependencies

### Data Storage
- **LocalStorage** - Used for:
  - Report history (same day only, auto-clears at midnight)
  - Custom templates (persistent)
- **No server required** - All processing happens client-side

### Privacy & Security
- ✅ No data sent to external servers (except Tesseract.js CDN)
- ✅ Images processed locally in browser
- ✅ Reports stored only in browser localStorage
- ⚠️ For sensitive security data, consider hosting on internal servers

## 🎨 Customization

### Property & Location Options

To add/modify properties or locations, edit the HTML file:

**Properties** (line ~200):
```html
<select id="propertySelect" onchange="toggleLocationDropdown()">
    <option value="">Select Property</option>
    <option value="Reserve">The Reserve</option>
    <option value="Harrison">The Harrison</option>
    <option value="Hermitage">The Hermitage</option>
</select>
```

**Reserve Locations** (line ~210):
```html
<select id="locationSelect">
    <option value="">Select Location</option>
    <option value="E124 Main Door">E124 Main Door</option>
    <option value="E125 11th Floor Lounge">E125 11th Floor Lounge</option>
    <!-- Add more locations here -->
</select>
```

### Issue Templates

Modify pre-filled templates (line ~430):
```javascript
function updateActionsObserved() {
    const templates = {
        'Tailgating': 'At [TIME], [NAME] entered the [LOCATION] with [NUMBER] individuals...',
        'Overstaying': 'At [TIME], individuals were observed in the [LOCATION]...',
        // Add more templates
    };
}
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

### Development Setup
1. Clone the repository
2. Open HTML file in browser
3. Make changes and test locally
4. Submit pull request

## 📝 License

MIT License - feel free to use and modify for your organization's needs.

## 👥 Credits

Developed for security operations teams managing multiple properties.

## 📞 Support

For issues or questions, please open an issue on GitHub.

---

**Version History:**
- **v2.0** - Multi-image support, annotations, templates, history, email export, one-view layout
- **v1.0** - Initial release with basic reporting functionality
