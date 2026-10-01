# Rock Paper Scissors 🎮

A responsive, browser-based **Rock Paper Scissors** game built with
**HTML, CSS, and vanilla JavaScript**.

The project provides a complete playable experience with configurable
difficulty, multiple round options, an adaptive computer opponent,
match-by-match results, persistent history using `localStorage`,
keyboard controls, and reduced-motion accessibility support.

## ✨ Features

-   🎮 Play Rock, Paper, Scissors against the computer
-   🎚️ Three difficulty levels:
    -   **Easy** --- computer chooses randomly
    -   **Medium** --- computer sometimes counters your most-played move
    -   **Hard** --- computer uses recent play patterns to predict your
        next move
-   🔢 Choose **3, 5, or 10 rounds**
-   📊 Live scoreboard for:
    -   Player wins
    -   Draws
    -   Computer wins
-   📝 Round-by-round match log
-   🏆 Match result screen after the final round
-   📚 History of completed matches
-   💾 Persistent match history with browser `localStorage`
-   🧹 Clear saved history
-   🔄 Replay a completed match
-   ⚙️ Change game settings between matches
-   ⌨️ Keyboard shortcuts:
    -   `R` → Rock
    -   `P` → Paper
    -   `S` → Scissors
-   📱 Responsive mobile-friendly layout
-   ♿ `prefers-reduced-motion` support
-   🎨 Custom colorful UI built without external CSS frameworks

## 🛠️ Technologies Used

-   **HTML5** --- page structure and game interface
-   **CSS3** --- responsive layout, styling, animations, and
    accessibility states
-   **JavaScript (ES6+)** --- game logic, computer AI, state management,
    event handling, and storage
-   **Web Storage API** --- saves match history in the browser

No backend, database, package manager, or external library is required.

## 📁 Project Structure

``` text
rock-paper-scissors/
│
├── rock-paper-scissors-4.html
└── README.md
```

The entire application is currently contained in one HTML file,
including its HTML markup, CSS, and JavaScript.

## 🚀 How to Run

### Option 1 --- Open directly

1.  Download or clone this repository.
2.  Open `rock-paper-scissors-4.html` in a modern web browser.
3.  Select the difficulty and number of rounds.
4.  Click **Start match**.
5.  Choose Rock, Paper, or Scissors.

### Option 2 --- Run with a local server

For a more development-friendly setup, run the project through a local
HTTP server.

For example, with Python:

``` bash
python -m http.server 8000
```

Then open:

``` text
http://localhost:8000
```

## 🎯 How the Game Works

The standard Rock Paper Scissors rules are used:

``` text
Rock     beats Scissors
Paper    beats Rock
Scissors beats Paper
```

If both players choose the same move, the round is a draw.

Each round updates the scoreboard and the round history. Draws still
count toward the selected number of rounds.

## 🤖 Computer Difficulty / AI

The computer opponent has three modes.

### Easy

The computer randomly selects one of the three moves.

``` javascript
if(d === 'easy') return rand(MOVES);
```

### Medium

The computer checks which move the player has used most frequently. With
a probability of 50%, it chooses the move that counters that most-played
move; otherwise it selects randomly.

This creates a partially adaptive opponent while retaining randomness.

### Hard

The computer attempts to predict the player's next move using recent
patterns.

The game stores transitions based on the player's previous two moves:

``` text
previous move 1 + previous move 2 → next observed move
```

When enough information exists, the computer predicts the next move and,
with an 85% probability, selects the counter to that prediction.

The AI memory lasts while the page remains open, so replaying matches
can continue using learned patterns.

## 🧠 Game State

The application keeps the current settings and match state in
JavaScript.

Example settings:

``` javascript
let settings = {
  difficulty: 'medium',
  rounds: 5
};
```

A match tracks:

-   Current round
-   Player score
-   Computer score
-   Draw count
-   Round-by-round log
-   Difficulty
-   Number of rounds

## 💾 Match History

Completed matches are stored in browser `localStorage` under:

``` text
rps-history-v1
```

The project keeps up to the latest **50 completed matches**.

Each saved match includes information such as:

-   Date/time
-   Difficulty
-   Number of rounds
-   Player score
-   Computer score
-   Draw count
-   Match outcome

If `localStorage` is unavailable, the application falls back to
in-memory history for the current page session.

## ⌨️ Keyboard Controls

During a match, you can use:

  Key   Move
  ----- -------------
  `R`   ✊ Rock
  `P`   ✋ Paper
  `S`   ✌️ Scissors

This makes the game playable without always clicking the on-screen
buttons.

## 🎨 UI & UX

The interface uses a compact card-based layout with:

-   Responsive sizing
-   High-contrast buttons
-   Visual score states
-   Animated hand shake before each result
-   Clear round status
-   Accessible focus outlines
-   `aria-current`, `aria-pressed`, and `aria-live` attributes
-   Reduced-motion support for users who prefer less animation

The main game is constrained to a mobile-friendly maximum width while
remaining usable on larger screens.

## ♿ Accessibility

The project includes several accessibility-oriented features:

-   Semantic buttons for interactive controls
-   Visible keyboard focus states
-   `aria-current` for navigation tabs
-   `aria-pressed` for selected setup options
-   `aria-live="polite"` for round results
-   Reduced-motion behavior using:

``` css
@media (prefers-reduced-motion: reduce)
```

## 🔄 Application Flow

``` text
Open Game
   ↓
Choose Difficulty
   ↓
Choose Number of Rounds
   ↓
Start Match
   ↓
Choose Rock / Paper / Scissors
   ↓
Computer Selects Move
   ↓
Round Result
   ↓
Update Score + Round History
   ↓
More Rounds?
   ├── Yes → Continue
   └── No  → Match Result
                 ↓
              Save History
                 ↓
          Replay / Change Settings
```

## 📌 Important Implementation Details

### Random selection

The game uses a small helper function to randomly select an item from an
array:

``` javascript
const rand = arr => arr[Math.floor(Math.random() * arr.length)];
```

### Win detection

The winning relationships are represented with an object:

``` javascript
const BEATS = {
  rock: 'scissors',
  paper: 'rock',
  scissors: 'paper'
};
```

This makes the round result logic simple and easy to maintain.

### Counter moves

The application also defines the move that beats each move:

``` javascript
const COUNTER = {
  rock: 'paper',
  paper: 'scissors',
  scissors: 'rock'
};
```

This is used by the Medium and Hard difficulty logic.

## 🧪 Testing Checklist

Before publishing changes, test:

-   [ ] Start a 3-round match
-   [ ] Start a 5-round match
-   [ ] Start a 10-round match
-   [ ] Test Easy difficulty
-   [ ] Test Medium difficulty
-   [ ] Test Hard difficulty
-   [ ] Confirm wins are counted correctly
-   [ ] Confirm losses are counted correctly
-   [ ] Confirm draws are counted correctly
-   [ ] Confirm the final result appears after the selected number of
    rounds
-   [ ] Confirm completed matches appear in History
-   [ ] Refresh the browser and confirm saved history remains
-   [ ] Clear history and confirm it is removed
-   [ ] Test `R`, `P`, and `S` keyboard controls
-   [ ] Test the game on mobile-sized screens
-   [ ] Test with reduced-motion preferences enabled

## 🌐 Deployment

Because the project is a static HTML application, it can be hosted using
a static web hosting service.

Possible deployment options include:

-   GitHub Pages
-   Netlify
-   Vercel
-   Cloudflare Pages
-   Any standard static web server

No server-side code is required.

## 🔮 Possible Future Improvements

Some ideas for future versions:

-   Add sound effects with an on/off setting
-   Add player names
-   Add a best-of series mode
-   Add additional statistics such as win percentage
-   Add themes or dark mode
-   Add more advanced AI prediction
-   Add difficulty explanations directly in the UI
-   Split the project into separate HTML, CSS, and JavaScript files
-   Add automated tests for game logic
-   Add an online multiplayer mode
-   Add a shareable match result
-   Add a Progressive Web App (PWA) version

## 📄 License

You can add the license that matches how you want others to use the
project.

For a personal portfolio project, a common choice is the **MIT
License**.

If you choose MIT, add a `LICENSE` file containing the standard MIT
License text and replace the copyright placeholder with your name and
year.

## 👨‍💻 Project Purpose

This project demonstrates practical front-end development concepts
including:

-   DOM manipulation
-   Event-driven programming
-   JavaScript state management
-   Basic game logic
-   Rule-based and pattern-based AI
-   Browser storage
-   Responsive CSS
-   Accessibility
-   Keyboard interaction
-   UI state transitions

It is suitable as a beginner-to-intermediate JavaScript portfolio
project because it combines a simple game concept with real application
features such as persistence, multiple screens, adaptive behavior, and
accessibility.
