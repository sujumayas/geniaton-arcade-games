# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a collection of short, visually beautiful, fun-to-watch mini-games that blend intelligence, GenAI themes, and ease of development. Each game is designed for fast playthroughs (2–5 minutes max), strong visual engagement, and hackathon-style energy. Currently contains 4 fully implemented games.

**Social Gaming Focus:** These games are designed as "social tools" - encouraging friendly competition through visible highscore systems that make sharing and comparing scores a core part of the experience.

## Architecture

### Game Structure
- Each game is a **single HTML file** that links to a **shared external stylesheet** (`styles.css`)
- Games contain minimal embedded `<style>` tags for game-specific overrides only
- No external dependencies or build process required - games run directly in the browser
- Each game must include all required screens:
  - Start screen (with highscore popup button)
  - Pause screen
  - Game over screen (with name input for leaderboard)
  - Victory/Win screen (for games with defined end states)

### File Organization
- Game files: `{gameName}.html` in root directory
- `styles.css`: Shared stylesheet with centralized UI components, theme system, and responsive design
- `index.html`: Landing page with grid layout showcasing all games with descriptions and thumbnails
- All games are asset-free (using CSS-only graphics, Canvas rendering, and emojis)
- Games are portable (can run standalone with styles.css)

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
- **Styling System**: Centralized in `styles.css` with CSS custom properties (CSS variables) for theming
  - Primary theme: `--primary-color: #0f0` (neon green)
  - Secondary: `--secondary-color: #0ff` (cyan)
  - Accent: `--accent-color: #f0f` (magenta)
  - Glow effects defined as reusable variables (`--glow-primary`, `--glow-strong`, etc.)
- **Font**: Courier New monospace font family for retro-tech aesthetic
- **Visual effects**: Combination of CSS text-shadow and Canvas shadowBlur for consistent glow effects
- **Canvas backgrounds**: Game-specific gradients (radial, linear) or solid black defined in embedded styles
- **Variations**: Colorful gradients (`innovationManiac.html`, `bugCatcher.html`) vs dark monochrome (`parAIchute.html`, `aiLabEscape.html`)

**Game Architecture Patterns:**
- **Canvas-based action games** (`parAIchute.html`, `bugCatcher.html`, `innovationManiac.html`): HTML5 Canvas for all rendering with requestAnimationFrame game loop
- **Maze-based puzzle games** (`aiLabEscape.html`): Canvas for maze rendering with grid-based movement
- **Game loop**: RequestAnimationFrame with delta time calculations for frame-independent movement
- **Audio**: Web Audio API with oscillators and gain nodes for procedural sound effects (no audio files)
- **Input handling**: Direct DOM event listeners (keydown, click) with key state tracking for continuous movement
- **Collision detection**:
  - AABB (Axis-Aligned Bounding Box) for rectangular collisions
  - Distance-based collision for circular objects
  - Grid-based collision for maze games
- **Visual effects**:
  - Particle systems for explosions and collectibles
  - Screen shake effects (camera offset)
  - Parallax scrolling backgrounds (stars, grids)
  - Pulsing/glowing animations using Math.sin()
- **Difficulty scaling**: Progressive difficulty through speed increases, spawn rate changes, and time pressure

## Implemented Games

1. **Prompt Shooter** ✅ `parAIchute.html` - Type GenAI terms to shoot falling words before they hit the ground (10 levels, combo system)
2. **AI Lab Escape** ✅ `aiLabEscape.html` - Navigate procedurally generated mazes as an AI escaping a lab (decreasing time limit per level)
3. **Bug Catcher** ✅ `bugCatcher.html` - Infinite runner platformer - avoid meetings, catch bugs (jump mechanic, infinite difficulty scaling)
4. **Innovation Maniac** ✅ `innovationManiac.html` - Vertical scrolling shooter against obsolete tech (powerup system, wave-based difficulty)

## Development Guidelines

### Game Implementation Pattern
Each game should follow this structure:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Game Name</title>
  <link rel="stylesheet" href="styles.css">
  <style>
    /* Game-specific CSS overrides only */
    #gameContainer {
      width: 800px;
      height: 600px;
    }
    canvas {
      background: /* game-specific gradient or color */;
    }
  </style>
</head>
<body>
  <div id="gameContainer">
    <canvas id="gameCanvas" width="800" height="600"></canvas>
    <!-- HUD, screens, and UI elements -->
  </div>
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

### Common UI Components (Defined in styles.css)
All UI components are styled centrally in `styles.css` for consistency:

- **HUD (Heads-Up Display)**: `#hud` - Absolute positioned flex container at top of screen
  - Color-coded elements: score (cyan), lives (red), level/wave (yellow)
  - Automatic glow effects via CSS variables
- **Game Container**: `#gameContainer` - Bordered container with neon glow box-shadow
- **Screens**: `.screen` class - Full-screen overlays with rgba(0,0,0,0.95) background
  - Start, pause, game over, victory screens
  - Flex column layout with centered content
  - Scrollable for long content
- **Buttons**: Transparent background with neon borders, glow on hover
- **Input fields**: `.name-input` - Styled text inputs with neon border and glow focus effect
- **Leaderboard**: Multiple styled options (`#leaderboard`, `#leaderboardDisplay`)
  - Entry styling with `.leaderboard-entry` and `.top3` classes
  - Rank, name, score components
- **Highscore Popup**: `#highscorePopup` - Full overlay with fade transition
- **Typography**: Automatic text-shadow glow effects via CSS variables
- **Utility classes**: `.hidden`, `.highlight`, `.warning`
- **Custom scrollbars**: Themed scrollbars for webkit and Firefox browsers

### Centralized Styles Architecture (styles.css)

The `styles.css` file provides a complete theming and UI component system:

**CSS Custom Properties (Theme Variables):**
```css
:root {
  --primary-color: #0f0;           /* Neon green */
  --secondary-color: #0ff;         /* Cyan */
  --accent-color: #f0f;            /* Magenta */
  --danger-color: #f00;            /* Red */
  --warning-color: #ff0;           /* Yellow */
  --background-color: #000;        /* Black */

  --glow-primary: 0 0 10px #0f0;   /* Standard glow */
  --glow-strong: 0 0 20px #0f0, 0 0 40px #0f0;  /* Intense glow */
  --font-family: 'Courier New', Courier, monospace;
  --border-width: 2px;
  --transition-speed: 0.3s;
}
```

**Predefined Components:**
- Base styles (body, reset)
- Game container with neon border
- HUD with color-coded elements
- Screen overlays (start, pause, game over)
- Button and link styling with hover effects
- Input fields with focus glow
- Leaderboard layouts and entry styling
- Highscore popup system
- Utility classes (.hidden, .highlight, .warning)
- Custom scrollbar styling
- Index page grid layout
- Responsive breakpoints

**Benefits:**
- Consistent visual language across all games
- Easy theming via CSS variables
- Minimal game-specific CSS needed
- Single source of truth for UI styling

### Leaderboard System (localStorage)

All games implement localStorage-based top 10 leaderboards with consistent patterns:

**Standard Functions:**
```javascript
function loadLeaderboard() {
  const data = localStorage.getItem('gameNameLeaderboard');
  return data ? JSON.parse(data) : [];
}

function saveLeaderboard(leaderboard) {
  localStorage.setItem('gameNameLeaderboard', JSON.stringify(leaderboard));
}

function addScoreToLeaderboard(name, score, ...additionalStats) {
  const leaderboard = loadLeaderboard();

  // Optional: Check if score qualifies for top 10
  if (leaderboard.length >= 10) {
    const lowestScore = leaderboard[leaderboard.length - 1].score;
    if (score <= lowestScore) return false;
  }

  leaderboard.push({
    name: name.trim() || 'ANONYMOUS',
    score: score,
    date: new Date().toLocaleDateString()
    // Additional game-specific stats
  });

  leaderboard.sort((a, b) => b.score - a.score);
  saveLeaderboard(leaderboard.slice(0, 10));
  return true;
}

function displayLeaderboard() {
  const leaderboard = loadLeaderboard();
  const listElement = document.getElementById('leaderboardList');

  if (leaderboard.length === 0) {
    listElement.innerHTML = '<p>No scores yet. Be the first!</p>';
    return;
  }

  listElement.innerHTML = leaderboard.map((entry, index) => {
    const rank = index + 1;
    const medal = rank === 1 ? '🥇' : rank === 2 ? '🥈' : rank === 3 ? '🥉' : `${rank}.`;
    const topClass = rank <= 3 ? 'top3' : '';

    return `
      <div class="leaderboard-entry ${topClass}">
        <span class="leaderboard-rank">${medal}</span>
        <span class="leaderboard-name">${entry.name}</span>
        <span class="leaderboard-score">${entry.score}</span>
      </div>
    `;
  }).join('');
}
```

**Key Patterns:**
- Unique localStorage key per game (e.g., `'promptShooterLeaderboard'`)
- Top 10 limit enforced on save
- Medals for top 3 positions (🥇🥈🥉)
- `.top3` class for visual distinction
- Name defaults to 'ANONYMOUS' if empty
- Enter key support for submitting scores
- Auto-focus on name input after game over

### Highscore Popup System
All games implement a standardized highscore viewing system for social sharing:

**Implementation Pattern:**
```html
<!-- Start screen with class -->
<div id="startScreen" class="screen with-popup-leaderboard">
  <h1>Game Title</h1>
  <!-- Game instructions -->
  <button onclick="startGame()">START GAME</button>
  <button onclick="showHighscores()">VIEW HIGHSCORES</button>
  <a href="index.html">← ALL GAMES</a>
</div>

<!-- Highscore popup overlay -->
<div id="highscorePopup" onclick="hideHighscores()">
  <h2>🏆 TOP 10 LEADERBOARD</h2>
  <div id="leaderboard">
    <div id="leaderboardList"></div>
  </div>
  <p>Click anywhere to return</p>
</div>
```

**JavaScript Functions:**
```javascript
function showHighscores() {
  displayLeaderboard();
  document.getElementById('highscorePopup').classList.add('show');
}

function hideHighscores() {
  document.getElementById('highscorePopup').classList.remove('show');
}
```

**Key Features:**
- Popup overlays entire game screen within the border (z-index: 200)
- Smooth fade-in/fade-out transitions (0.3s)
- Click anywhere on popup to dismiss
- Positioned within game container square border
- Uses centralized CSS from styles.css (#highscorePopup)
- Start screen uses `.with-popup-leaderboard` class to hide inline leaderboard
- Supports localStorage-based top 10 leaderboards per game

### Audio System (Web Audio API)

All games use procedural audio generation with the Web Audio API (no audio files):

**Standard Pattern:**
```javascript
// Initialize audio context at top of file
const audioCtx = new (window.AudioContext || window.webkitAudioContext)();

// Base sound function
function playSound(frequency, duration, type = 'sine', volume = 0.3) {
  const oscillator = audioCtx.createOscillator();
  const gainNode = audioCtx.createGain();

  oscillator.connect(gainNode);
  gainNode.connect(audioCtx.destination);

  oscillator.frequency.value = frequency;
  oscillator.type = type;  // 'sine', 'square', 'sawtooth', 'triangle'

  gainNode.gain.setValueAtTime(volume, audioCtx.currentTime);
  gainNode.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + duration);

  oscillator.start(audioCtx.currentTime);
  oscillator.stop(audioCtx.currentTime + duration);
}

// Game-specific sound effects
function shootSound() {
  playSound(600, 0.1, 'square', 0.2);
}

function hitSound() {
  playSound(800, 0.1, 'sine');
  setTimeout(() => playSound(1000, 0.08, 'sine'), 40);
}

function gameOverSound() {
  playSound(400, 0.2, 'sawtooth');
  setTimeout(() => playSound(300, 0.2, 'sawtooth'), 150);
  setTimeout(() => playSound(200, 0.4, 'sawtooth'), 300);
}
```

**Common Sound Types:**
- **Shoot/Fire**: High frequency (600-800Hz), square wave, short duration (0.1s)
- **Hit/Collect**: Mid-high frequency (800-1200Hz), sine wave, often with ascending pitch
- **Explosion/Damage**: Low frequency (100-200Hz), sawtooth wave, descending pitch
- **Powerup**: Ascending sequence of sine waves (800 → 1000 → 1200Hz)
- **UI/Menu**: Single sine tones

**Benefits:**
- Zero file size for audio assets
- No loading times
- Retro arcade aesthetic
- Consistent across all games
- Works offline

### Visual Effects Patterns

Common visual effects implemented across games:

**Particle Systems:**
```javascript
class Particle {
  constructor(x, y, color, size = 3) {
    this.x = x;
    this.y = y;
    this.vx = (Math.random() - 0.5) * 200;  // Random velocity
    this.vy = (Math.random() - 0.5) * 200;
    this.life = 1;  // Fade from 1 to 0
    this.color = color;
    this.size = size;
  }

  update(delta) {
    this.x += this.vx * delta;
    this.y += this.vy * delta;
    this.vy += 200 * delta;  // Gravity
    this.life -= delta * 2;  // Fade out
  }

  draw() {
    ctx.globalAlpha = this.life;
    ctx.fillStyle = this.color;
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
    ctx.fill();
    ctx.globalAlpha = 1;
  }
}

// Usage: Spawn particles on collision/collection
for (let i = 0; i < 20; i++) {
  particles.push(new Particle(x, y, '#0f0', 4));
}

// Update/draw in game loop
particles = particles.filter(p => {
  p.update(delta);
  p.draw();
  return p.life > 0;  // Remove dead particles
});
```

**Screen Shake Effect:**
```javascript
let screenShake = 0;

// Trigger shake on impact
function impact() {
  screenShake = 0.5;  // Shake intensity
}

// In game loop
if (screenShake > 0) {
  const offsetX = (Math.random() - 0.5) * screenShake * 20;
  const offsetY = (Math.random() - 0.5) * screenShake * 20;
  ctx.translate(offsetX, offsetY);
  screenShake -= delta * 2;  // Decay
}
```

**Pulsing/Glowing Animations:**
```javascript
// Pulsing effect using sine wave
const pulse = Math.sin(Date.now() / 200) * 0.2 + 0.8;
ctx.shadowBlur = 20 * pulse;

// Wobble effect
const wobble = Math.sin(this.wobbleTimer) * 5;
this.y += wobble;
this.wobbleTimer += delta * 3;
```

**Parallax Scrolling:**
```javascript
// Background stars at different speeds
for (let star of stars) {
  star.y += star.speed * delta;
  if (star.y > canvas.height) {
    star.y = 0;
    star.x = Math.random() * canvas.width;
  }
  ctx.fillRect(star.x, star.y, star.size, star.size);
}
```

**Delta Time for Frame Independence:**
```javascript
let lastFrame = 0;

function gameLoop(timestamp) {
  const delta = (timestamp - lastFrame) / 1000;  // Convert to seconds
  lastFrame = timestamp;

  // Cap delta to prevent large jumps
  if (delta > 0.1) delta = 0.1;

  // Use delta for all movement and timers
  player.x += velocity * delta;
  timer -= delta;

  requestAnimationFrame(gameLoop);
}
```

## Testing
- Test each game in multiple browsers (Chrome, Firefox, Safari)
- Verify games work offline (no external dependencies)
- Check performance on lower-end devices
- Ensure all game states (start, pause, game over) function correctly

## File Naming
- Use descriptive, lowercase names with no spaces
- Examples: `promptShooter.html`, `aiLabEscape.html`, `biasHunt.html`