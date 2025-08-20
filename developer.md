# Strategy Flowchart Generator - Developer Documentation

This document provides technical details for developers working on the Strategy Flowchart Generator application.

## Architecture Overview

### Single-Page Application
- **Type**: Client-side HTML5 application
- **Dependencies**: Minimal external libraries
- **Processing**: All data processing happens in browser
- **Security**: No server-side components, data never leaves client

### Key Technologies
- **Frontend**: Vanilla JavaScript, HTML5 Canvas, CSS3
- **Excel Processing**: SheetJS (XLSX library)
- **AI Integration**: Azure OpenAI REST API
- **Export Formats**: Canvas PNG, SVG generation, CSV creation

## Code Structure

### Main Application File: `index.html`
```
├── HTML Structure
│   ├── Header section
│   ├── Sidebar (settings and upload)
│   └── Main content area (canvas and controls)
├── CSS Styling
│   ├── Modern gradient design
│   ├── Responsive layout
│   └── Animation and transitions
└── JavaScript Application Logic
    ├── File processing functions
    ├── AI integration
    ├── Canvas rendering engine
    └── Export functionality
```

## Core Functions Reference

### File Processing
```javascript
// Main file upload handler
async function processFile(file)
// Validates Excel structure and converts to JSON

// Excel validation
function validateExcelData(data)
// Returns array of validation errors

// Data preprocessing
function calculateLayout(data)
// Converts Excel data to positioned elements
```

### AI Integration
```javascript
// Azure OpenAI text optimization
async function optimizeTextWithAI(data)
// Shortens long text while preserving meaning

// Configuration management
function saveSettings() / loadSettings()
// Persists user preferences in localStorage
```

### Canvas Rendering
```javascript
// Main rendering function
function renderFlowchart(layoutData)
// Draws complete flowchart on canvas

// Element drawing
function drawElement(ctx, element)
// Renders individual flowchart elements

// Connection drawing
function drawConnections(ctx, layoutData)
// Draws arrows between connected elements
```

### Export Functions
```javascript
// Image exports
function downloadPNG() / downloadSVG()
// Generate and download image files

// Data exports
function exportForLucidChart() / exportDataAsJSON()
// Create structured data for external tools
```

## Data Models

### Excel Input Schema
```javascript
{
  Step_ID: number,           // Unique identifier
  Element_Type: string,      // "Account" | "Action" | "Outcome" | "Note"
  Title: string,             // Display text
  Opening_Balance: string,   // Financial amount (optional)
  Closing_Balance: string,   // Financial amount (optional)
  Action_Description: string,// Details for actions (optional)
  Annual_Amount: string,     // Yearly impact (optional)
  Color_Category: string,    // "Blue" | "Red" | "Green" | "Gray" | "Yellow" | "Purple"
  Connects_To: string,       // Comma-separated Step_IDs
  Position_Row: number,      // Layout hint (optional)
  Position_Col: number       // Layout hint (optional)
}
```

### Internal Layout Schema
```javascript
{
  ...inputData,              // All original Excel data
  x: number,                 // Calculated X position
  y: number,                 // Calculated Y position
  width: number,             // Element width (default: 180)
  height: number             // Element height (default: 80)
}
```

## Configuration Management

### Application Settings
```javascript
const settings = {
  chartTitle: string,        // Flowchart title
  chartWidth: number,        // Canvas width (800-2000)
  chartHeight: number,       // Canvas height (600-1500)
  showStepIds: boolean,      // Display Step ID badges
  aiEnabled: boolean,        // Enable AI optimization
  aiApiKey: string,          // Azure OpenAI API key
  aiEndpoint: string         // Azure OpenAI endpoint URL
};
```

### Storage
- Settings saved to `localStorage` as JSON
- No server-side storage required
- All data processing in memory only

## Azure OpenAI Integration

### API Configuration
```javascript
// Endpoint format
const endpoint = "https://your-resource.openai.azure.com/";

// API call structure
const response = await fetch(
  `${endpoint}/openai/deployments/gpt-4/chat/completions?api-version=2024-02-15-preview`,
  {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'api-key': apiKey
    },
    body: JSON.stringify({
      messages: [{ role: 'user', content: prompt }],
      max_tokens: 100,
      temperature: 0.3
    })
  }
);
```

### Text Optimization Prompt
```
Shorten this financial flowchart element title while preserving all important information and meaning. Keep it under 40 characters. Original: "{originalText}"
```

## Canvas Rendering Details

### Drawing Coordinates
- **Origin**: Top-left (0,0)
- **Element Size**: 180px × 80px (default)
- **Spacing**: 220px horizontal, 120px vertical
- **Margins**: 50px from edges
- **Title Area**: Top 60px reserved

### Color Palette
```javascript
const colors = {
  'Blue': '#3498db',     // Account elements
  'Red': '#e74c3c',      // Special/closing accounts
  'Green': '#27ae60',    // Outcome elements
  'Gray': '#95a5a6',     // Action elements
  'Yellow': '#f39c12',   // Cash accounts
  'Purple': '#9b59b6'    // Special outcomes (e.g., UK pensions)
};
```

### Text Rendering
- **Main Title**: Bold 13px, white text
- **Financial Data**: Regular 11px, white text
- **Step ID Badge**: Bold 14px, white on red background
- **Text Wrapping**: Automatic word wrap within element bounds

## Export Formats

### SVG Generation
```javascript
function canvasToSVG(canvas, data) {
  // Converts canvas rendering to scalable SVG
  // Preserves all visual elements and styling
  // Compatible with professional design tools
}
```

### LucidChart CSV Format
```csv
Id,Name,Shape,Line to,Description
1,"Account Name","Rectangle","2","Additional details"
2,"Action Name","Diamond","3",""
```

### Data Export Structure
- **JSON**: Complete data model with positioning
- **CSV**: LucidChart-compatible import format
- **SVG**: Vector graphics for scaling
- **PNG**: Raster image for immediate use

## Development Setup

### Local Development
```bash
# No build process required
# Option 1: Direct file access
open index.html

# Option 2: Local server (recommended)
python -m http.server 8000
# Access at http://localhost:8000

# Option 3: Node.js server
npx serve .
# Access at provided URL
```

### Testing
```javascript
// Test data validation
const testData = [/* sample Excel data */];
const errors = validateExcelData(testData);
console.log('Validation errors:', errors);

// Test layout calculation
const layoutData = calculateLayout(testData);
console.log('Layout positions:', layoutData);

// Test AI integration (requires API key)
const optimizedData = await optimizeTextWithAI(testData);
console.log('AI optimized text:', optimizedData);
```

## Performance Considerations

### Memory Usage
- Excel files loaded entirely into memory
- Canvas rendering creates temporary image data
- No memory leaks (all references properly cleaned)

### Processing Limits
- **Excel size**: Recommend < 1000 rows for optimal performance
- **Canvas size**: Maximum 2000×1500 pixels
- **AI requests**: Rate-limited by Azure OpenAI quotas

### Optimization Opportunities
- Implement virtual scrolling for large datasets
- Add canvas caching for repeated renders
- Optimize AI batching for multiple text elements

## Error Handling

### File Processing Errors
```javascript
try {
  const data = await processFile(file);
} catch (error) {
  showStatus(`Error processing file: ${error.message}`, 'error');
}
```

### AI Integration Errors
```javascript
// Graceful fallback to original text
if (!response.ok) {
  console.warn('AI optimization failed, using original text');
  return originalData;
}
```

### Canvas Rendering Errors
```javascript
// Canvas context validation
const ctx = canvas.getContext('2d');
if (!ctx) {
  throw new Error('Canvas rendering not supported');
}
```

## Future Enhancement Areas

### Planned Features
1. **Investment Philosophy Charts**: Matrix-style layouts
2. **Custom Themes**: User-defined color schemes
3. **Batch Processing**: Multiple Excel files
4. **Advanced Layouts**: Force-directed positioning
5. **Real-time Collaboration**: Multi-user editing

### Technical Improvements
1. **WebGL Rendering**: Better performance for large charts
2. **Web Workers**: Background processing for AI calls
3. **IndexedDB**: Client-side data persistence
4. **PWA Features**: Offline functionality
5. **WebAssembly**: Performance-critical calculations

### Integration Opportunities
1. **Power BI**: Embedded custom visual
2. **SharePoint**: Native integration
3. **Teams**: Bot-based chart generation
4. **Excel Add-in**: Direct Excel integration
5. **PowerAutomate**: Workflow automation

## Security Considerations

### Data Privacy
- All processing client-side only
- No data transmission except to user's Azure OpenAI
- No tracking or analytics
- No server-side logging

### Azure OpenAI Security
- API keys stored only in browser memory
- Requests go to user's Azure tenant only
- No data stored by AI service
- Network policies can restrict access

### Input Validation
- Excel file type validation
- Data structure validation
- Sanitized text output for SVG export
- XSS prevention in dynamic content

## Deployment Strategies

### Azure Static Web Apps
```yaml
# azure-static-web-apps.yml
name: Azure Static Web Apps CI/CD
on:
  push:
    branches: [main]
jobs:
  build_and_deploy_job:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Build And Deploy
        uses: Azure/static-web-apps-deploy@v1
        with:
          app_location: "/"
          output_location: "/"
```

### Network Security
```javascript
// Content Security Policy recommendations
const csp = `
  default-src 'self';
  script-src 'self' 'unsafe-inline' cdnjs.cloudflare.com;
  style-src 'self' 'unsafe-inline';
  connect-src 'self' *.openai.azure.com;
  img-src 'self' data: blob:;
`;
```

## API Documentation

### Internal API Functions

#### File Processing API
```javascript
// Process uploaded Excel file
processFile(file: File): Promise<Object[]>

// Validate Excel data structure
validateExcelData(data: Object[]): string[]

// Calculate element positions
calculateLayout(data: Object[]): Object[]
```

#### Rendering API
```javascript
// Render complete flowchart
renderFlowchart(layoutData: Object[]): void

// Draw individual element
drawElement(ctx: CanvasRenderingContext2D, element: Object): void

// Draw connection arrows
drawConnections(ctx: CanvasRenderingContext2D, layoutData: Object[]): void
```

#### Export API
```javascript
// Generate PNG download
downloadPNG(): void

// Generate SVG download
downloadSVG(): void

// Generate LucidChart CSV
exportForLucidChart(): void

// Generate JSON data export
exportDataAsJSON(): void
```

## Contributing Guidelines

### Code Style
- Use modern JavaScript (ES6+)
- Consistent indentation (2 spaces)
- Descriptive function and variable names
- Comprehensive error handling
- JSDoc comments for complex functions

### Testing Checklist
- [ ] Excel upload and validation
- [ ] Layout calculation accuracy
- [ ] Canvas rendering quality
- [ ] Export functionality
- [ ] AI integration (with valid credentials)
- [ ] Responsive design
- [ ] Browser compatibility

### Pull Request Process
1. Fork the repository
2. Create feature branch
3. Implement changes with tests
4. Update documentation
5. Submit pull request with description

---

**For additional technical questions, please create an issue in the repository or contact the development team.**
