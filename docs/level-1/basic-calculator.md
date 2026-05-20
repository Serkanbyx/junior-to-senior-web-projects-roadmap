# Basic Calculator

> A modern calculator with expression parsing, calculation history, memory functions, sound effects, and swipe gestures.

**Level:** 1 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://basic-calculatorrrr.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/basic-calculator)

---

## Purpose

This project teaches you how to handle complex user input and parse mathematical expressions
safely. Unlike a naive `eval()` approach, it uses the Shunting-yard algorithm for expression
evaluation — a real CS concept you'll encounter in compilers and interpreters. It also
introduces UI polish: animations, sound feedback, and touch gestures that make a simple tool
feel professional.

## Tech Stack

- **Frontend:** HTML, CSS, vanilla JavaScript
- **Backend:** none
- **Database:** none
- **Key libraries / tools:** Web Audio API (sound effects), CSS3 animations (ripple effect)
- **Deployment:** Netlify (static hosting)

## Build Steps

1. **Design the layout.** Build a calculator grid with CSS Grid — number keys, operator keys, and a display area. Use CSS custom properties for theming so colors are easy to adjust later.
2. **Handle input.** Each button click appends to an expression string displayed in the screen area. Support chaining operators and parentheses without allowing invalid sequences (e.g. two operators in a row).
3. **Parse and evaluate.** Implement the Shunting-yard algorithm: convert the infix expression to postfix (Reverse Polish Notation), then evaluate the postfix stack. This avoids `eval()` entirely and handles operator precedence correctly.
4. **Add memory functions.** Implement MC (memory clear), MR (memory recall), M+ (add to memory), and M- (subtract from memory) using a single stored value. Show a subtle indicator when memory is active.
5. **Build calculation history.** Store each completed calculation (expression + result) in an array. Render a scrollable history panel that the user can toggle open.
6. **Add micro-interactions.** Use the Web Audio API to generate short click sounds on key press. Add CSS ripple animations on button tap for tactile feedback. Implement a swipe gesture (touch events) to clear the display.
7. **Sanitize and secure.** Validate all input before evaluation — reject anything that isn't a number, operator, or parenthesis. Never pass raw strings to `eval()`.

## Deployment

Push the three static files (`index.html`, `style.css`, `script.js`) to a GitHub repo and
connect it to Netlify. No build step or environment variables required — drag-and-drop deploy works.

## Tips

- The Shunting-yard algorithm sounds intimidating but it's just two data structures (an output queue and an operator stack) with four rules. Draw it on paper first.
- Web Audio API's `OscillatorNode` can generate click sounds without loading audio files — keeps the project dependency-free.
- Extension: add keyboard support so users can type expressions without clicking buttons.

## README Guidance

The project repo's README should include a short description, a screenshot of the calculator UI,
the live demo link, the tech stack, a "features" list (history, memory, sounds), and a one-step
local run instruction.
