# Dark Mode Implementation

## Overview
This document explains the implementation of the dark mode feature for the AI Stationery Bill Validator application. The dark mode provides a true dark experience while maintaining the color palette requested.

## Color Scheme

### Light Mode (Default)
- **Background 1**: `#E2F0F9` (Light Blue)
- **Background 2**: `#B0DDE4` (Medium Blue)
- **Cards**: `#FFFFFF` (White)
- **Text**: `#286FB4` (Dark Blue)
- **Muted Text**: `#6a8faf` (Muted Blue)
- **Accent Color**: `#DF4C73` (Pink)

### Dark Mode
- **Background 1**: `#0a1a25` (Dark Blue)
- **Background 2**: `#0d2535` (Darker Blue)
- **Cards**: `#102d42` (Dark Blue)
- **Text**: `#e0f0ff` (Light Blue)
- **Muted Text**: `#a0c0e0` (Muted Light Blue)
- **Accent Color**: `#DF4C73` (Pink - remains the same for contrast)

## Implementation Details

### CSS Variables
The dark mode is implemented using CSS variables that change based on the presence of the `dark-mode` class on the body element:

```css
:root {
  /* Light mode variables */
  --bg1: #E2F0F9;
  --bg2: #B0DDE4;
  --card: #FFFFFF;
  --text: #286FB4;
  --muted: #6a8faf;
  --brand1: #286FB4;
  --brand2: #286FB4;
}

body.dark-mode {
  /* Dark mode variables */
  --bg1: #0a1a25;
  --bg2: #0d2535;
  --card: #102d42;
  --text: #e0f0ff;
  --muted: #a0c0e0;
  --brand1: #5a9bd5;
  --brand2: #5a9bd5;
}
```

### JavaScript Implementation
The dark mode toggle is handled by JavaScript in the `script.js` file:

```javascript
let isDarkMode = localStorage.getItem('darkMode') === 'true' || 
  (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches);

function updateTheme() {
  if (isDarkMode) {
    document.body.classList.add('dark-mode');
    themeToggle.innerHTML = '<i class="fas fa-sun"></i> Light Mode';
  } else {
    document.body.classList.remove('dark-mode');
    themeToggle.innerHTML = '<i class="fas fa-moon"></i> Dark Mode';
  }
  localStorage.setItem('darkMode', isDarkMode);
}

// Initialize theme
updateTheme();

themeToggle.addEventListener('click', () => {
  isDarkMode = !isDarkMode;
  updateTheme();
});
```

### Blob Elements
The background blob elements also change colors in dark mode to match the theme:

```css
/* Light mode blobs */
.b1{background:conic-gradient(from 0.35turn, #286FB4, #B0DDE4, #E2F0F9, #286FB4)}
.b2{background:conic-gradient(from 0.1turn, #286FB4, #DF4C73, #B0DDE4, #286FB4)}
.b3{background:conic-gradient(from 0.7turn, #286FB4, #DF4C73, #E2F0F9, #286FB4)}

/* Dark mode blobs */
body.dark-mode .b1{background:conic-gradient(from 0.35turn, #1a4a7a, #0d2535, #0a1a25, #1a4a7a)}
body.dark-mode .b2{background:conic-gradient(from 0.1turn, #1a4a7a, #DF4C73, #0d2535, #1a4a7a)}
body.dark-mode .b3{background:conic-gradient(from 0.7turn, #1a4a7a, #DF4C73, #0a1a25, #1a4a7a)}
```

## Features

1. **Persistent Setting**: The user's preference is saved in localStorage
2. **System Preference Detection**: Automatically detects the user's system preference for dark mode
3. **Smooth Transitions**: All color changes have smooth transitions
4. **Comprehensive Coverage**: All UI elements are properly themed
5. **Accessibility**: Proper contrast ratios maintained in both modes

## Testing

The dark mode has been tested on:
- Desktop browsers (Chrome, Firefox, Edge, Safari)
- Mobile devices (iOS Safari, Android Chrome)
- Various screen sizes and resolutions
- With and without system-level dark mode enabled

## Usage

Users can toggle between light and dark mode by clicking the theme toggle button in the header. The button icon and text change to indicate the current mode and the available alternative.