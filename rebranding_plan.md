# Game Rebranding Plan: "Oh my Skibity Sigma"

## Overview
This document outlines the plan for rebranding the Baseball Fielding Trivia game to "Oh my Skibity Sigma" as requested by the user. The rebranding will involve updating all references to the game name throughout the application while maintaining the baseball theme.

## Rebranding Elements

### 1. HTML Updates
- Update the page title in index.html
- Update all header text references
- Update footer copyright information
- Update any meta tags or descriptions

### 2. CSS Updates
- Update any CSS classes or IDs that reference the old name
- Consider adding a new color scheme to reflect the new branding
- Create a logo or stylized text for the new name

### 3. JavaScript Updates
- Update any game name references in the JavaScript code
- Update welcome messages and instructions
- Update localStorage keys to reflect the new name

## Implementation Details

### HTML Updates
```html
<!-- Update page title -->
<title>Oh my Skibity Sigma</title>

<!-- Update header content -->
<header>
  <h1>Oh my Skibity Sigma</h1>
  <p>Test your knowledge of baseball fielding strategies and decisions</p>
</header>

<!-- Update footer content -->
<footer>
  <p>Oh my Skibity Sigma &copy; <span id="current-year"></span></p>
</footer>
```

### CSS Updates
```css
/* Add new branding styles */
:root {
  --primary-color: #6200ea; /* Deep purple */
  --primary-light: #9d46ff;
  --primary-dark: #0a00b6;
  --secondary-color: #00bcd4; /* Cyan */
  --secondary-light: #62efff;
  --secondary-dark: #008ba3;
  --accent-color: #ffab00; /* Amber */
}

/* Create a stylized logo for the header */
header h1 {
  font-family: 'Bangers', cursive; /* Fun, comic-style font */
  font-size: 3rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  letter-spacing: 2px;
}

/* Add a special style for "Skibity Sigma" */
header h1 .highlight {
  color: var(--accent-color);
  font-style: italic;
}
```

### JavaScript Updates
```javascript
// Update welcome screen content
function renderWelcomeScreen(container) {
  const welcomeScreen = document.createElement('div');
  welcomeScreen.className = 'welcome-screen';
  
  welcomeScreen.innerHTML = `
    <h2>Welcome to Oh my Skibity Sigma!</h2>
    <div class="welcome-content">
      <p>
        Test your knowledge of infield and outfield decision-making in various baseball scenarios.
        Select a difficulty level and click Start to begin.
      </p>
      <!-- Rest of welcome screen content -->
    </div>
  `;
  
  // Add event listeners
  // ...
  
  container.appendChild(welcomeScreen);
}

// Update localStorage keys
function saveGameState() {
  localStorage.setItem('skibitySigna_gameState', JSON.stringify(gameState));
}

function loadGameState() {
  const savedState = localStorage.getItem('skibitySigna_gameState');
  if (savedState) {
    gameState = JSON.parse(savedState);
  }
}
```

## Implementation Steps

1. **Create Font Assets**:
   - Find and include a fun, distinctive font for the new game title
   - Consider adding a small logo or icon to represent the game

2. **Update HTML Structure**:
   - Modify index.html to reflect the new game name
   - Update all visible text references to the game

3. **Update CSS Styling**:
   - Modify the color scheme to give the game a fresh look
   - Create special styling for the new game name
   - Ensure the baseball theme is still evident

4. **Update JavaScript References**:
   - Change any hardcoded game name references
   - Update localStorage keys
   - Modify welcome and instruction text

5. **Browser Tab Updates**:
   - Update the page title for browser tabs
   - Add a favicon if possible

## Visual Design Concept

The new branding will feature:
- A bold, fun typography for "Oh my Skibity Sigma"
- A color scheme of deep purple, cyan, and amber accents
- Maintained baseball imagery and theme
- Possibly a stylized "Σ" (sigma) symbol incorporated into the design
- A playful, energetic feel appropriate for both kids and adults

## Testing Checklist

- Verify all visible instances of the old name have been updated
- Check that the new styling is consistent across all game screens
- Ensure localStorage functionality works with the new keys
- Test that the game maintains its baseball theme despite the name change
- Verify the new branding works well in both adult and kid modes
