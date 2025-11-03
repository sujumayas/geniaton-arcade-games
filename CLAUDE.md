# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a curated collection of 10 short, visually beautiful, fun-to-watch mini-games that blend intelligence, GenAI themes, and ease of development. Each game is designed for fast playthroughs (2–5 minutes max), strong visual engagement, and hackathon-style energy.

## Architecture

### Game Structure
- Each game is a **single, self-contained HTML file** with embedded CSS and JavaScript
- No external dependencies or build process required - games run directly in the browser
- Each game must include all required screens:
  - Start screen
  - Pause screen
  - Game over screen
  - Game state (with 5-10 levels max, or single level for simplicity)

### File Organization
- Game files: `{gameName}.html` in root directory
- All games are currently asset-free (using CSS-only graphics and text)
- Each game is completely independent and portable

### Running Games
To play any game:
```bash
# Option 1: Open directly in browser
open parAIchute.html

# Option 2: Start local server (for better compatibility)
python3 -m http.server 8000
# Then navigate to http://localhost:8000/{gameName}.html
```

No build process, dependencies, or installation required.

### Coding Conventions

**Visual Design:**
- **Styling**: Embedded CSS with terminal/hacker aesthetic (black backgrounds, neon colors like #0f0, #f0f, #0ff)
- **Font**: Courier New for that retro-tech feel
- **Visual effects**: CSS text-shadow and canvas shadowBlur for glow effects
- **Variations**: Some games use colorful gradients (llmOlympics.html) vs monochrome terminal (parAIchute.html, aiLabEscape.html)

**Game Architecture Patterns:**
- **Canvas-based action games** (`parAIchute.html`): Use HTML5 Canvas for sprite-based gameplay with requestAnimationFrame
- **DOM-based puzzle games** (`aiLabEscape.html`): Canvas for visual effects, DOM input for text-based puzzles
- **Hybrid minigame collections** (`llmOlympics.html`): Multiple game modes with state switching
- **Game loop**: RequestAnimationFrame for smooth 60fps in all canvas-based games
- **Input handling**: Direct DOM event listeners (keydown, click, etc.)

## Game Concepts (All Implemented)

1. **Prompt Shooter** ✅ `parAIchute.html` - Type GenAI terms to shoot falling words
2. **AI Lab Escape** ✅ `aiLabEscape.html` - Puzzle game with keyword-based solutions
3. **Prompt or Plagiarism?** ✅ `promptOrPlagiarism.html` - Trivia + judgment game
4. **GenAI Karaoke** ✅ `genaiKaraoke.html` - Audio + text guessing
5. **Prompt Jenga** ✅ `promptJenga.html` - Stack & balance game
6. **Bias Bug Hunt** ✅ `biasBugHunt.html` - Whack-a-mole meets debugging
7. **Dream Designer** ✅ `dreamDesigner.html` - Image generation + storytelling
8. **AI Zoo Tycoon** ✅ `aiZooTycoon.html` - Simulation game
9. **The Trolley Prompt** ✅ `trolleyPrompt.html` - Ethical decision-making
10. **LLM Olympics** ✅ `llmOlympics.html` - Minigame bundle

## Development Guidelines

### Game Implementation Pattern
Each game should follow this structure:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Game Name</title>
  <style>/* Embedded CSS */</style>
</head>
<body>
  <!-- Game UI elements -->
  <script>/* Complete game logic */</script>
</body>
</html>
```

### Visual Themes
- **Neon terminal interface** with glowing text effects
- **Dark backgrounds** (#000, #111) with bright accent colors
- **Retro-futuristic** aesthetic (think Tron, Matrix, cyberpunk)
- **AI/tech terminology** prominently featured in gameplay

### Technical Requirements
- Pure HTML/CSS/JavaScript (no frameworks)
- Responsive design for different screen sizes
- 60fps performance target
- Keyboard and mouse input support
- Clean, readable code with meaningful variable names

### Game State Management Pattern
All games should implement consistent state management:
- `gameState` variable tracking: 'start', 'playing', 'paused', 'complete'
- Screen divs with `.screen` class and `.hidden` toggle
- ESC key to pause/resume during gameplay
- Clear separation between UI screens and game canvas

## Testing
- Test each game in multiple browsers (Chrome, Firefox, Safari)
- Verify games work offline (no external dependencies)
- Check performance on lower-end devices
- Ensure all game states (start, pause, game over) function correctly

## File Naming
- Use descriptive, lowercase names with no spaces
- Examples: `promptShooter.html`, `aiLabEscape.html`, `biasHunt.html`