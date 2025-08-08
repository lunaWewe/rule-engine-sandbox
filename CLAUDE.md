# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Risk Rule Engine Sandbox** (風險規則引擎沙盒) - a web-based financial transaction risk assessment system built with vanilla JavaScript, HTML, and CSS. The application simulates real-time transaction processing with configurable risk detection rules and interactive data visualization.

## Architecture and Key Components

### Core Application Structure
- **Single-page application** with no build system or package manager
- **Frontend-only**: Pure HTML/CSS/JavaScript with no backend dependencies
- **Modular JavaScript architecture** with distinct manager modules:
  - `RuleManager` - Handles rule configuration and drag-drop functionality
  - `TransactionManager` - Manages transaction data loading and processing
  - `ChartManager` - Controls ECharts visualizations (world map, pie chart, bar chart)
  - `Utils` - Common utility functions for date formatting and data processing

### File Structure
```
/
├── index.html          # Main application file (1454 lines)
├── style.css           # Comprehensive styling with custom design system
├── data1.json          # Sample transaction data (200 transactions)
├── wMap.json           # World map GeoJSON data for ECharts
├── bj2.jpg            # Background image
└── [font files]       # Poppins font variants
```

### Key Features
1. **Rule Engine**: 7 predefined risk assessment rules with drag-and-drop interface
2. **Transaction Processing**: Sequential processing of transactions with rule matching
3. **Multi-country Support**: International transaction data with country code mapping
4. **Real-time Visualization**: Interactive charts showing risk distribution and geographic data
5. **Risk Levels**: Three-tier system (low/medium/high risk) with configurable defaults

## Data Model

### Transaction Structure
```javascript
{
  id: number,
  card: string,           // 16-digit card number
  countryCode: string,    // ISO country code
  amount: number,         // Transaction amount
  deviceRisk: number,     // Risk score (-1.0 to 1.0)
  timestamp: string       // ISO datetime
}
```

### Rule System
- **Rule Types**: Success (approve), Warning (review), Danger (block)
- **Conditions**: Support both single-transaction and historical transaction analysis
- **Sequential Processing**: Rules evaluated in order, first match wins
- **Default Actions**: Configurable fallback behavior based on risk level

## Development Guidelines

### Running the Application
```bash
# No build process required - serve static files
python -m http.server 8000
# OR
npx serve .
# OR open index.html directly in browser
```

### Key Technical Considerations

1. **No Package Manager**: This is a vanilla JavaScript project with no npm/package.json
2. **External Dependencies**: 
   - Bootstrap 5.3.0 (CSS framework)
   - ECharts 5.4.3 (data visualization)
   - Font Awesome 6.4.0 (icons)
   - All loaded via CDN

3. **Data Loading**: Application attempts to load `data1.json`, falls back to generating synthetic data
4. **Browser Compatibility**: Modern browsers required for ES6+ features
5. **Internationalization**: UI text in Traditional Chinese, requires font support

### Debugging and Development
- Built-in debug logging system (can be enabled via UI)
- Console logging throughout transaction processing
- Visual indicators for transaction states and rule matches

### Code Patterns
- **Module Pattern**: Each manager is a self-contained object with init() method
- **Event-driven**: Heavy use of DOM events and callbacks
- **Functional Programming**: Extensive use of array methods (filter, map, reduce)
- **Async Operations**: Promise-based data loading with fallbacks

## Common Modifications

When working on this codebase:

1. **Adding New Rules**: Extend the `Data.rules` array in the main JavaScript section
2. **Modifying Visualizations**: Work with the `ChartManager` module and ECharts options
3. **Transaction Processing**: Core logic is in `RuleManager.processTransaction()`
4. **Styling Changes**: All styles are in `style.css` with a cohesive design system
5. **Data Sources**: Modify `TransactionManager.loadOrGenerateTransactions()` for different data sources

## Important Notes

- The application includes both real and synthetic transaction generation
- All text and UI elements are in Traditional Chinese
- The rule engine processes transactions sequentially by timestamp
- Charts update automatically after rule execution
- Geographic data visualization requires the `wMap.json` file for world map rendering