# Strategy Flowchart Generator

A powerful web application that transforms Excel strategy data into professional flowcharts with AI-powered text optimization. Built for financial planning teams who need to create consistent, visual strategy documentation.

![Strategy Flowchart Generator](assets/screenshots/main-interface.png)

## Features

### 🎯 Core Functionality
- **Excel-to-Flowchart Conversion**: Upload standardized Excel files and generate professional flowcharts instantly
- **AI Text Optimization**: Automatically shorten long text while preserving meaning using Azure OpenAI
- **Multiple Export Formats**: PNG, SVG, LucidChart CSV, and JSON exports
- **Professional Styling**: Color-coded elements with consistent visual design
- **Smart Layout**: Automatic positioning with manual override capabilities

### 🤖 AI Integration
- **Azure OpenAI Integration**: Seamless integration with your Azure tenant
- **Intelligent Text Processing**: Shortens overly long titles while maintaining accuracy
- **Fallback Handling**: Continues processing if AI services are unavailable
- **Enterprise Security**: All processing within your Azure environment

### 🎨 Visual Features
- **Color-Coded Elements**: Blue (Accounts), Green (Outcomes), Gray (Actions), Red/Yellow (Special)
- **Step ID Badges**: Optional numbering system for easy reference
- **Connection Arrows**: Automatic flow indicators between related elements
- **Responsive Design**: Works on desktop and mobile devices
- **Customizable Canvas**: Adjustable dimensions for different use cases

## Quick Start

### 1. Download and Setup
```bash
git clone https://github.com/yourusername/strategy-flowchart-generator.git
cd strategy-flowchart-generator
```

### 2. Open the Application
- Open `index.html` in any modern web browser
- Or deploy to Azure Static Web Apps for team access

### 3. Configure Azure OpenAI (Optional)
1. Get your Azure OpenAI API key and endpoint
2. Enter credentials in the AI Optimization panel
3. Enable AI text optimization

### 4. Create Your First Flowchart
1. Download the Excel template
2. Fill in your strategy data
3. Upload the file and generate your flowchart

## Excel Template Structure

The application uses a standardized Excel format with these columns:

| Column | Description | Example |
|--------|-------------|---------|
| `Step_ID` | Unique identifier | 1, 2, 3... |
| `Element_Type` | Account, Action, Outcome, Note | Account |
| `Title` | Display name | "Super Accumulation Account" |
| `Opening_Balance` | Starting amount | $500,000 |
| `Closing_Balance` | Ending amount | $0 |
| `Action_Description` | Details for actions | "Rollover to pension" |
| `Annual_Amount` | Yearly impact | $25,000 |
| `Color_Category` | Visual styling | Blue, Red, Green, Gray, Yellow, Purple |
| `Connects_To` | Connected Step_IDs | "2,3" (comma-separated) |
| `Position_Row` | Layout row hint | 1, 2, 3... |
| `Position_Col` | Layout column hint | 1, 2, 3... |

## Deployment Options

### Azure Static Web Apps (Recommended)
1. Fork this repository
2. Create new Static Web App in Azure
3. Connect to your GitHub repository
4. Configure network restrictions for intranet access
5. Set up Azure OpenAI integration

### GitHub Pages
1. Enable GitHub Pages in repository settings
2. Access via `https://yourusername.github.io/strategy-flowchart-generator`

### Local Hosting
- No server required - runs entirely in browser
- All processing happens client-side for data security

## Configuration

### Azure OpenAI Setup
1. Create Azure OpenAI resource
2. Deploy GPT-4 model
3. Get API key and endpoint URL
4. Enter credentials in application settings

### Network Security
For enterprise deployment:
- Use Azure networking rules to restrict access
- Deploy to internal Azure subscription
- Configure Azure AD authentication if needed

## Usage Examples

### Financial Strategy Planning
- Super fund rollovers and consolidations
- Pension commencement strategies
- Investment rebalancing workflows
- Estate planning flowcharts

### Business Process Documentation
- Client onboarding procedures
- Compliance workflows
- Decision trees
- Standard operating procedures

## Browser Support

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

## File Size Limits

- Excel files: Up to 10MB
- Generated flowcharts: Up to 2000x1500 pixels
- Export files: No practical limits

## Troubleshooting

### Common Issues

**Excel file not loading**
- Ensure file has .xlsx or .xls extension
- Check that required columns (Step_ID, Element_Type, Title) exist
- Verify no completely empty rows in data

**AI optimization not working**
- Verify Azure OpenAI API key and endpoint
- Check API key permissions
- Ensure network can reach Azure OpenAI service

**Flowchart elements overlapping**
- Adjust Position_Row and Position_Col values
- Increase canvas size in settings
- Reduce number of elements per row

**Export issues**
- Try different export format
- Check browser's download permissions
- Ensure adequate disk space

### Getting Help

1. Check the [User Guide](docs/user_guide.md)
2. Review [API Configuration](docs/api_configuration.md)
3. Create an issue in this repository
4. Contact your IT administrator for Azure-related issues

## Contributing

We welcome contributions! Please see [DEVELOPERS.md](DEVELOPERS.md) for technical details and development setup.

### Development Setup
```bash
# Clone repository
git clone https://github.com/yourusername/strategy-flowchart-generator.git

# No build process required - open index.html in browser
# For development, use a local server:
python -m http.server 8000
# or
npx serve .
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Security

- All processing happens client-side
- No data sent to external servers (except Azure OpenAI if configured)
- Excel files never leave your environment
- Azure OpenAI integration uses your tenant boundaries

## Roadmap

### Planned Features
- [ ] Investment Philosophy flowchart support
- [ ] Custom color themes
- [ ] Batch processing multiple Excel files
- [ ] Advanced layout algorithms
- [ ] PowerBI integration
- [ ] Multi-language support
- [ ] Audit trail functionality

### Version History
- **v1.0.0** - Initial release with core functionality
- **v1.1.0** - Azure OpenAI integration
- **v1.2.0** - LucidChart export capability

## Support

For enterprise support and customization:
- Technical documentation: [docs/](docs/)
- Development guide: [DEVELOPERS.md](DEVELOPERS.md)
- Azure deployment: [docs/setup_guide.md](docs/setup_guide.md)

---

**Built for financial planning teams who value precision, consistency, and professional presentation.**
