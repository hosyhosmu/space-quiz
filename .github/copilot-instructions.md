# Copilot Instructions for Space Quiz

## Architecture & Overview

- **Single-file Application**: The entire application lives inside `index.html`. It contains all HTML structure, responsive CSS styles, theme tokens, and vanilla JavaScript quiz logic without any build step, bundler, external libraries, or web server dependencies.
- **State Machine**:
  - `quizScreen` (`#quizScreen`): Displays the current question, answer options, educational feedback banner, and next-question action.
  - `resultsScreen` (`#resultsScreen`): Appears after Question 10, calculating total accuracy, assigning a tiered astronaut rank, and rendering score telemetry.
- **Design & Theming**:
  - Strict narrow-column layout (`max-width: 520px`) centered in viewport.
  - Native `prefers-color-scheme` implementation (`:root` dark by default, `@media (prefers-color-scheme: light)` override) using CSS custom properties for mission-control telemetry HUD styling, option states, and glowing accents.

## Testing & Preview

- **Running Locally**:
  - Open `index.html` directly in any web browser (`file:///` protocol) or the integrated browser canvas (`open_canvas` with `canvasId: "browser"`).
  - No build, compilation, or package manager scripts (`npm`, `yarn`, etc.) are needed.
- **Browser-level Smoke Testing**:
  - Use canvas action `evaluate_javascript` against the active browser instance to run automated assertions against DOM elements (`#scoreValue`, `#questionCounter`, `#feedbackBox`, keyboard event dispatches, and `#resultsScreen`).

## Key Conventions

- **Keep Dependencies at Zero**: Do not introduce node dependencies, package configs, or external CDN assets unless explicitly requested. Everything must remain self-contained within `index.html`.
- **Keyboard & Accessibility**:
  - All quiz choices support keyboard hotkeys (`1`–`4` or `A`–`D`).
  - Advancing questions or restarting the quiz supports the `Enter` key.
  - Maintain ARIA attributes on options (`role="radio"`, `aria-checked`) and live regions (`aria-live="polite"` on score telemetry and status indicators).
- **Question Structure**:
  - Questions are stored in the `questions` array in `index.html`. Each question object contains:
    - `category`: Short uppercase topic header.
    - `question`: Prompt text.
    - `options`: 4 multiple-choice options.
    - `answer`: Zero-based index of the correct option.
    - `fact`: Contextual educational explanation displayed in the animated feedback banner upon selection.
