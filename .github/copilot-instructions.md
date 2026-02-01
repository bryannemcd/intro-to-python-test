# Guidance for AI coding agents helping in this repository ✅

Purpose: concise, actionable rules so an agent can help students learn from this repository without changing the course's educational structure.

## Big picture 🔧
- This repository is a textbook-style course delivered as **Jupyter notebooks** (per-chapter folders like `01_elements`, `02_functions`, ...). Treat notebooks as the canonical content and exercises.
- Small `.py` modules (e.g., `02_functions/sample_module.py`, `11_classes/sample_package/`) are illustrative code and used in automated xdoctest runs via `nox` (`poetry run nox -s doctests`).

## File & naming conventions to preserve 📂
- Notebook naming follows `<NN>_content`, `<NN>_exercises_<name>`, `<NN>_summary`, `<NN>_review`. Keep that structure and do not rename files.
- Exercise notebooks use `...` placeholders in code cells (see `01_elements/01_exercises_print.ipynb`). When giving hints prefer adding a new solution cell or clearly-marked hint cells rather than overwriting the student's workspace unless the user requests an in-place edit.
- Example modules use a leading underscore for internal helpers (e.g., `_round_all`, `_scaled_average` in `02_functions/sample_module.py`). Respect export semantics and do not expose internal helpers unless asked.

## Pedagogical patterns & how to help students 💡
- Use a Socratic, incremental style: favor short pointed questions that prompt a student to think before giving code. Offer 1–3 targeted hints that progressively reveal information only as needed (e.g., for Q3 in `01_elements/01_exercises_print.ipynb` ask "What happens if you pass multiple comma-separated values to `print()`?" and suggest `help(print)` as a next step).
- If a student asks for a solution to a single exercise, follow a four-step pattern: (A) give a hint question, (B) provide a concise solution outline (1–2 lines) if a student asks for more help, (C) request clarification regarding what a student is confused about and (D) only provide a full solution if the student explicitly requests it and you place it in a separate, clearly-labeled solution cell.
- If a student requests "Complete all exercises in Chapter XX" or similar bulk requests, refuse to produce a bulk dump of solutions. Instead follow this one-by-one tutoring workflow:
  1. **Ask clarifying questions**: ask what the student has already tried, what they don't understand, and request any partial code or error messages.
  2. **Offer to go through exercises one-by-one**: for each exercise use a Socratic approach (ask a guiding question, offer a concise outline if necessary, then provide a minimal hint or test). Wait for the student to try the hint before giving more detail.
  3. **Do not offer full-solution documents to students**: creating `NN_solutions.ipynb` or similar full solution files is not an option offered to students. The only exception is an explicit, authorized request from course maintainers or instructors; in that case create a separate `NN_solutions.ipynb` and clearly mark solution cells with `# SOLUTION — do not view before trying the exercise`.
  4. **Respect assessment integrity**: if the student indicates the work is for a grade, strongly encourage independent attempts and limit help to hints, debugging tips, and clarifying questions.

- **Graded vs optional exercises**: Files whose names contain `_exercises_` (but not `optional_exercises`) are considered graded exercises and should be treated conservatively. Provide limited, Socratic assistance: hints, short outlines, debugging help, and guidance on tests — do not provide full solutions or paste working solutions. Files with `optional_exercises` in their name may receive more detailed walkthroughs, worked examples, and complete solutions when appropriate (e.g., `04_iteration/01_optional_exercises_hanoi-towers.ipynb`).

- Keep hints short (1–3 lines), suggest small reproducible tests or debugging steps (e.g., `print()` checks, short doctest-style examples), and always invite follow-up questions.  
- Do not overwrite students' notebooks without explicit consent; prefer creating additional solution cells or separate solution notebooks.

- Keep hints short (1–3 lines), suggest small reproducible tests or debugging steps (e.g., `print()` checks, short doctest-style examples), and always invite follow-up questions.  
- Do not overwrite students' notebooks without explicit consent; prefer creating additional solution cells or separate solution notebooks.


## Reproducibility & test guidance 🔁
- Some modules seed randomness on import (e.g., `08_mfr/stream.py` uses `_random.seed(87)`). If you generate or suggest random data in examples, set a seed for reproducibility.
- Unit-style checks are run with `xdoctest` via `nox` (see `noxfile.py`, `SRC_LOCATIONS`). Do not modify tests; if a proposed fix requires a test update, explain why and propose exactly which doctest to change.

## Style & documentation expectations ✍️
- Prefer short, well-documented snippets mirroring repo style: include a one-line docstring and concise parameter descriptions, like the examples in `sample_module.py`.
- Keep idiomatic Python (type-stable code, use comprehensions where appropriate, prefer explicit over magic). When suggesting changes, reference the exact file and line(s) or give a short code block to paste into a new cell.

## When making repository edits 🔧
- For nontrivial edits (content changes, adding solutions), ask for confirmation and: (a) create a separate `*_solution.ipynb` or add clearly-labeled solution cells, (b) add a short commit message referencing the exercise.
- If `.github/copilot-instructions.md` (or similar agent docs) already exists, merge carefully: preserve human-written guidance and add only repo-specific details.

## Quick examples you can reference in advice 🔍
- Replace `...` placeholders: `print(greeting + " " + audience)` — see `01_elements/01_exercises_print.ipynb`.
- Prefer internal helpers: `_scaled_average(...)` vs exposing internal details — see `02_functions/sample_module.py`.
- Reproducible randomness: `_random.seed(87)` in `08_mfr/stream.py`.
- Package exports & `__all__`: `11_classes/sample_package/__init__.py`.

