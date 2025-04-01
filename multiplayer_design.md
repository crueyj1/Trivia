# Multiplayer Functionality Design

## Overview
This document outlines the design for implementing multiplayer functionality in the "Oh my Skibity Sigma" baseball trivia game. The multiplayer mode will be implemented as a "hot-seat" style game where players take turns on the same device.

## Game Structure
- **Game Format**: 10 questions per game
- **Series Format**: Best of 3 rounds to determine the overall winner
- **Player Count**: Support for 2-4 players

## Data Structures

### Player Object
```javascript
{
  id: Number,          // Unique player identifier
  name: String,        // Player name
  score: Number,       // Current round score
  seriesWins: Number,  // Number of rounds won in the series
  isActive: Boolean    // Whether it's this player's turn
}
```

### Multiplayer Game State
```javascript
{
  players: Array,           // Array of Player objects
  currentPlayerIndex: Number, // Index of current player in the players array
  currentRound: Number,     // Current round (1-3)
  questionsPerRound: Number, // Set to 10
  questionCount: Number,    // Current question number within the round
  roundWinners: Array,      // Array of player IDs who won each round
  gameMode: String,         // 'adult' or 'kid'
  categoryType: String,     // 'fielding' or 'current'
  isMultiplayer: Boolean,   // Set to true for multiplayer games
  gameStatus: String        // 'setup', 'playing', 'roundEnd', 'seriesEnd'
}
```

## Game Flow

### 1. Game Setup
- Player enters number of players (2-4)
- Each player enters their name
- Players select game mode (adult/kid)
- Players select category (fielding strategy/current trivia)
- System initializes game state with round 1, question 1

### 2. Gameplay Loop
- Current player is shown a question
- Player selects an answer
- System evaluates answer and updates player's score
- System advances to next player
- After all players have answered the current question, advance to next question
- After 10 questions, end the round

### 3. Round End
- System determines round winner (highest score)
- Round winner gets a series point
- Display round results showing each player's score
- Reset question count and player scores for next round
- If any player has 2 series wins, end the series
- Otherwise, begin next round

### 4. Series End
- Display final results showing each player's series wins
- Declare player with most series wins as the overall winner
- Offer option to play again

## UI Components

### Player Setup Screen
- Input fields for number of players and player names
- Mode selection (adult/kid)
- Category selection (fielding/current)
- Start game button

### Game Screen Enhancements
- Player indicator showing whose turn it is
- Question counter (e.g., "Question 3 of 10")
- Round indicator (e.g., "Round 1 of 3")
- Series score display showing each player's round wins

### Round Results Screen
- Display each player's score for the round
- Highlight the round winner
- Show updated series standings
- Button to continue to next round

### Series Results Screen
- Display final series results
- Highlight the overall winner
- Option to play again or return to main menu

## Implementation Approach

### 1. Player Management
- Create functions to add, remove, and update players
- Implement turn rotation logic
- Store player data in game state

### 2. Round Management
- Track questions per round (fixed at 10)
- Calculate and store round winners
- Reset appropriate state between rounds

### 3. Series Management
- Track round wins for each player
- Determine series winner (first to 2 round wins)
- Handle series completion and restart

### 4. UI Updates
- Create new UI components for multiplayer-specific screens
- Update existing components to show multiplayer information
- Ensure clear visual indication of current player

### 5. State Persistence
- Use localStorage to save game state between page refreshes
- Allow resuming an in-progress multiplayer game
