# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a collection of short, visually beautiful, fun-to-watch mini-games that blend intelligence, GenAI themes, and ease of development. Each game is designed for fast playthroughs (2–5 minutes max), strong visual engagement, and hackathon-style energy. Currently contains 4 fully implemented games.

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
- `index.html`: Landing page with grid layout showcasing all games with descriptions and thumbnails
- All games are currently asset-free (using CSS-only graphics and text)
- Each game is completely independent and portable

### Running Games
To play games:
```bash
# Option 1: View all games through the landing page
open index.html
# or with local server:
python3 -m http.server 8000
# Then navigate to http://localhost:8000/

# Option 2: Open individual games directly
open parAIchute.html
open bugCatcher.html
open innovationManiac.html
open aiLabEscape.html
```

No build process, dependencies, or installation required.

### Coding Conventions

**Visual Design:**
- **Styling**: Embedded CSS with terminal/hacker aesthetic (black backgrounds, neon colors like #0f0, #f0f, #0ff)
- **Font**: Courier New for that retro-tech feel
- **Visual effects**: CSS text-shadow and canvas shadowBlur for glow effects
- **Variations**: Some games use colorful gradients (`innovationManiac.html`) vs monochrome terminal (`parAIchute.html`, `aiLabEscape.html`)

**Game Architecture Patterns:**
- **Canvas-based action games** (`parAIchute.html`, `bugCatcher.html`, `innovationManiac.html`): Use HTML5 Canvas for sprite-based gameplay with requestAnimationFrame
- **DOM-based puzzle games** (`aiLabEscape.html`): Canvas for visual effects, DOM input for text-based puzzles
- **Game loop**: RequestAnimationFrame for smooth 60fps in all canvas-based games
- **Input handling**: Direct DOM event listeners (keydown, click, etc.)
- **Collision detection**: Custom collision logic for platformers and shooters
- **Parallax scrolling**: Used in vertical scrollers like `innovationManiac.html`

## Implemented Games

1. **Prompt Shooter** ✅ `parAIchute.html` - Type GenAI terms to shoot falling words (canvas-based typing game)
2. **AI Lab Escape** ✅ `aiLabEscape.html` - Puzzle game with keyword-based solutions (DOM/canvas hybrid)
3. **Bug Catcher** ✅ `bugCatcher.html` - Infinite runner where you're a developer avoiding meetings and catching bugs (canvas-based platformer)
4. **Innovation Maniac** ✅ `innovationManiac.html` - Vertical scrolling shooter piloting through waves of obsolete tech (canvas-based shooter)

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
- "Back to Menu" link on game over screen returning to `index.html`

### Common UI Components
- **HUD (Heads-Up Display)**: Absolute positioned div showing score, lives, level/wave info
- **Neon button styling**: Transparent background with colored borders that glow on hover
- **Screen overlays**: Full-screen modals (start, pause, game over) with rgba(0,0,0,0.95) backgrounds
- **Typography**: All text uses text-shadow for glow effect matching the game's theme color

## Testing
- Test each game in multiple browsers (Chrome, Firefox, Safari)
- Verify games work offline (no external dependencies)
- Check performance on lower-end devices
- Ensure all game states (start, pause, game over) function correctly

## File Naming
- Use descriptive, lowercase names with no spaces
- Examples: `promptShooter.html`, `aiLabEscape.html`, `biasHunt.html`