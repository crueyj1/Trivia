# Age-Appropriate Modes Implementation

## Overview
This document outlines the implementation of age-appropriate modes for the "Oh my Skibity Sigma" baseball trivia game, providing both adult and kid (11-year-old) experiences.

## Mode Characteristics

### Kid Mode (11-year-old)
- **Content Level**: Challenging but appropriate for an 11-year-old baseball fan
- **Language**: Simpler explanations with more enthusiastic tone
- **Question Focus**: 
  - Basic baseball rules and positions
  - Famous players and teams
  - Fundamental baseball concepts
  - Simple strategic decisions
  - Current baseball facts presented in an accessible way
- **Visual Elements**: More colorful, engaging interface
- **Feedback**: More encouraging and educational

### Adult Mode
- **Content Level**: Full complexity of baseball strategy and trivia
- **Language**: Technical baseball terminology
- **Question Focus**:
  - Advanced fielding strategies
  - Complex game situations
  - Detailed statistical analysis
  - Historical and current baseball knowledge
- **Visual Elements**: Standard professional interface
- **Feedback**: Straightforward and informative

## Implementation Details

### Mode Toggle Component
```html
<div class="mode-toggle">
  <span class="mode-label">Game Mode:</span>
  <div class="toggle-switch">
    <input type="checkbox" id="mode-switch" class="toggle-input">
    <label for="mode-switch" class="toggle-label">
      <span class="toggle-text-kid">Kid</span>
      <span class="toggle-handle"></span>
      <span class="toggle-text-adult">Adult</span>
    </label>
  </div>
</div>
```

### Mode Selection Logic
```javascript
// Mode selection function
function setGameMode(mode) {
  if (mode !== 'adult' && mode !== 'kid') {
    console.error('Invalid game mode');
    return;
  }
  
  gameState.gameMode = mode;
  
  // Update UI to reflect current mode
  document.body.classList.remove('mode-adult', 'mode-kid');
  document.body.classList.add(`mode-${mode}`);
  
  // Update toggle switch position
  const modeSwitch = document.getElementById('mode-switch');
  if (modeSwitch) {
    modeSwitch.checked = (mode === 'adult');
  }
  
  // Store preference in localStorage
  localStorage.setItem('preferredGameMode', mode);
  
  return gameState;
}

// Event listener for mode toggle
document.getElementById('mode-switch').addEventListener('change', function() {
  const newMode = this.checked ? 'adult' : 'kid';
  setGameMode(newMode);
});

// Initialize with saved preference or default to kid mode
function initializeGameMode() {
  const savedMode = localStorage.getItem('preferredGameMode') || 'kid';
  setGameMode(savedMode);
}
```

### Question Selection Based on Mode
```javascript
// Get appropriate questions based on current game mode and category
function getQuestionsForCurrentMode() {
  const mode = gameState.gameMode; // 'adult' or 'kid'
  const category = gameState.categoryType; // 'fielding' or 'current'
  
  if (category === 'fielding') {
    // Use existing fielding scenarios but filter by difficulty
    if (mode === 'kid') {
      // For kids, primarily use easy questions with some medium
      return [
        ...scenarios.easy,
        ...scenarios.medium.filter((q, i) => i < 2) // Just a few medium ones
      ];
    } else {
      // For adults, use all difficulties
      return [
        ...scenarios.easy,
        ...scenarios.medium,
        ...scenarios.hard
      ];
    }
  } else if (category === 'current') {
    // Use the appropriate set from current trivia
    return currentBaseballTrivia[mode];
  }
  
  // Fallback
  return scenarios.medium;
}
```

### Visual Differentiation
```css
/* Base styles */
:root {
  /* Common variables */
}

/* Adult mode styling */
body.mode-adult {
  --primary-color: #0d47a1; /* Deep blue */
  --secondary-color: #388e3c; /* Green */
  --accent-color: #f57c00; /* Orange */
}

/* Kid mode styling */
body.mode-kid {
  --primary-color: #1e88e5; /* Brighter blue */
  --secondary-color: #43a047; /* Brighter green */
  --accent-color: #ff9800; /* Brighter orange */
  --font-size-base: 1.1rem; /* Slightly larger text */
}

/* Kid mode specific elements */
body.mode-kid .scenario-box {
  background-color: #4fc3f7; /* Light blue */
  border: 3px solid #1565c0;
  border-radius: 12px;
}

body.mode-kid .option-btn {
  border-width: 2px;
  border-radius: 10px;
}

body.mode-kid .result-box.correct {
  background-color: rgba(76, 175, 80, 0.2);
  border-width: 3px;
}

body.mode-kid .result-box.incorrect {
  background-color: rgba(244, 67, 54, 0.2);
  border-width: 3px;
}
```

### Feedback Adaptation
```javascript
// Get age-appropriate feedback based on game mode
function getPerformanceFeedback(score) {
  const mode = gameState.gameMode;
  
  if (mode === 'kid') {
    if (score === 0) {
      return "Keep practicing! Everyone starts somewhere in learning baseball!";
    } else if (score < 5) {
      return "Good job! You're learning about baseball and that's awesome!";
    } else if (score < 10) {
      return "Wow! You really know your baseball stuff! That's impressive!";
    } else if (score < 15) {
      return "Amazing! You could teach others about baseball with all that knowledge!";
    } else {
      return "INCREDIBLE! You're a baseball genius! Maybe you'll be a coach someday!";
    }
  } else {
    // Adult feedback (existing)
    if (score === 0) {
      return "Keep practicing! Baseball fielding decisions require experience.";
    } else if (score < 5) {
      return "Good start! You're developing your baseball IQ.";
    } else if (score < 10) {
      return "Solid performance! You know your way around the diamond.";
    } else if (score < 15) {
      return "Excellent! You could be a field manager with that baseball knowledge.";
    } else {
      return "Outstanding! You have professional-level understanding of baseball strategy!";
    }
  }
}
```

## Integration Points

1. **Game Initialization**:
   - Add mode selection to welcome screen
   - Initialize with saved preference or default to kid mode

2. **Question Selection**:
   - Modify question selection logic to consider both category and mode
   - Filter questions appropriately for kid mode

3. **UI Updates**:
   - Add mode toggle component to relevant screens
   - Implement CSS changes for visual differentiation
   - Update explanation text based on mode

4. **Feedback System**:
   - Modify feedback messages based on current mode
   - Adjust tone and language for kid mode

5. **Persistence**:
   - Save mode preference in localStorage
   - Remember user's preference between sessions
