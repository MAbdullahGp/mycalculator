# MyCalculator

A minimalist pocket calculator that judges your math. Trivial calculations get a roast, while genuinely complex ones earn a grudging nod.

Built with plain HTML, CSS, and JavaScript—no frameworks, bundlers, or build step required.

## Features

- Basic arithmetic: addition, subtraction, multiplication, and division
- Decimal input and percentage conversion
- Clear and backspace controls
- Keyboard support for faster calculations
- Responsive, mobile-friendly layout
- Tactile button animations and calculator-style visual design
- Expression history shown above the current result
- Context-aware feedback after calculations:
  - Roasts for overly simple arithmetic
  - Error feedback for invalid operations such as division by zero
  - Encouragement for more involved calculations
- Randomized messages so repeated calculations do not always receive the same response

## Demo Behavior

The calculator intentionally comments on the calculation you enter. For example:

- `5 + 0` is recognized as unnecessary work
- `7 × 1` receives a multiplication-by-one roast
- `9 / 9` earns a division-by-itself message
- `125 × 48` may receive a respectful response for being more substantial

## Getting Started

### Run locally

No installation is needed.

1. Clone the repository:

   ```bash
   git clone https://github.com/MAbdullahGp/mycalculator.git
   ```

2. Open `index.html` in a modern web browser.

Alternatively, serve the directory with any static web server:

```bash
python3 -m http.server
```

Then open `http://localhost:8000` in your browser.

## Controls

### On-screen buttons

| Button | Action |
| --- | --- |
| `C` | Clear the current calculation |
| `⌫` | Remove the last character |
| `%` | Convert the current expression value to a percentage |
| `÷`, `×`, `−`, `+` | Add an arithmetic operator |
| `.` | Enter a decimal point |
| `=` | Evaluate the expression |

### Keyboard

The calculator also supports:

- Number keys: `0–9`
- Operators: `+`, `-`, `*`, `/`
- Decimal point: `.`
- Percentage: `%`
- Calculate: `Enter` or `=`
- Delete input: `Backspace`
- Clear: `Escape`, `C`, or `c`

## How It Works

The application is contained in a single `index.html` file.

### Interface

- Tailwind CSS is loaded from its CDN for utility classes and layout styling.
- Custom CSS creates the dark calculator chassis, recessed display, tactile buttons, and shake animation.
- Google Fonts provides Inter for interface text and JetBrains Mono for calculator values.

### Calculator state

The calculator maintains two pieces of state:

- `expression`: the current arithmetic expression or result
- `justEvaluated`: tracks whether the last action was a completed calculation, allowing the next digit to start a new expression

### Evaluation

Before evaluation, input is restricted to digits, decimal points, and the supported arithmetic operators. Results are rounded to a practical precision using `toPrecision(12)` and displayed in a friendlier format using multiplication, division, and minus symbols.

### Feedback engine

`analyzeCalculation()` classifies calculations into categories such as:

- Adding or subtracting zero
- Multiplying or dividing by one
- Multiplying by zero
- Simple one- and two-digit arithmetic
- Dividing a number by itself
- Dividing by zero
- Multi-step, decimal, or larger calculations

The matching message is selected randomly from the `ROASTS` collection and displayed in the calculator screen. Roasts trigger a shake animation, while errors and respectful responses use different colors.

## Project Structure

```text
mycalculator/
└── index.html    # Markup, styling, calculator logic, and feedback messages
```

## Dependencies

The project has no local dependencies. It uses these externally hosted resources:

- [Tailwind CSS CDN](https://cdn.tailwindcss.com)
- [Google Fonts](https://fonts.google.com/), using Inter and JetBrains Mono

An internet connection is required for those external styles and fonts. The calculator logic itself is self-contained in `index.html`.

## Browser Support

Use a modern browser with support for:

- ES6 JavaScript
- `new Function()`
- CSS Grid and custom properties
- `CSS.escape()`

## Security Note

The expression evaluator uses `new Function()` after applying a character whitelist. This is acceptable for the calculator's tightly controlled local input, but it should be replaced with a dedicated parser if expressions ever come from untrusted external sources or are expanded to support additional syntax.

## License

No license is currently specified for this repository. Add a license file if you plan to distribute or reuse the project publicly.
