# Copilot instructions

## Project shape

The project is a single-file, dependency-free browser quiz. `quiz.html` owns the entire experience: markup and accessibility hooks, responsive/light-dark/reduced-motion styling, the question data, and the quiz state machine. There is no build pipeline or server layer.

The `questions` array is the source of truth for quiz content. `renderQuestion()` draws the current question and progress, `chooseAnswer()` locks the answers and updates score/feedback, and `showResults()` switches to the final screen. The restart handler resets state and renders the first question again. Keep question count, answer indices, score, progress, and result thresholds consistent when changing the dataset or flow.

## Commands and checks

- Run the app: open `quiz.html` directly in a browser; it does not require a server.
- Build, automated tests, and lint: no commands or tooling are configured in this repository.
- Focused manual check: open the page, use Tab and Enter to select a correct answer and a wrong answer, verify feedback and score, then advance to the results screen and use “Play again” to confirm the reset.

## Code conventions

- Keep the app self-contained in `quiz.html`; use no external runtime or asset dependencies unless the project is deliberately restructured.
- Keep quiz data declarative in `questions`. Each answer's zero-based position must match its `correct` index.
- JavaScript is a strict-mode IIFE with DOM elements cached near the state; preserve the existing `renderQuestion` → `chooseAnswer` → `showResults` flow and guard against answering more than once per question.
- Generate answer controls as buttons and populate dynamic content with `textContent`; preserve the current keyboard focus handling, live feedback, and progress-bar ARIA values.
- Use the existing CSS custom properties for theme colors and maintain the `prefers-color-scheme`, small-screen, and `prefers-reduced-motion` behavior when changing styles.
