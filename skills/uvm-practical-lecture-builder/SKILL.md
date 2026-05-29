---
name: uvm-practical-lecture-builder
description: Use when creating or updating Korean HTML lecture materials for this Practical-UVM-Step-By-Step study repo. Produces source-grounded Day N workbook pages with local SystemVerilog highlighting, quizzes, checklists, and practice prompts.
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [uvm, systemverilog, learning, html, lecture-material]
    related_skills: [html-preview-server, waza-learn]
---

# UVM Practical Lecture Builder

## Overview

This project-local skill preserves the lecture format established by `lectures/day0_repo_orientation.html` and applies it to the rest of the Practical-UVM-Step-By-Step study repo.

The target output is a Korean interactive workbook page: source excerpts embedded directly in HTML, line-number gutters, local SystemVerilog/UVM highlighting, concept cards, trace steps, progress checklist, quiz, practice prompt, and an LLM question template.

## When to Use

Use this skill when:

- Adding, regenerating, or polishing `lectures/day*.html` UVM learning pages.
- Extending the curriculum to another UVM example in this repo.
- Updating source excerpts after line ranges or source files change.
- Improving code readability, syntax highlighting, quiz quality, or study prompts.

Do not use it for:

- Editing DUT/UVM source behavior.
- Installing or running commercial simulators.
- Generic UVM answers that do not need this repo's source excerpts.

## Current Curriculum

See `references/curriculum.md` for the Day 0-21 map.

The generated index is:

- `lectures/index.html`

## Page Contract

Each Day page should contain:

1. Korean title, goal, and completion criterion.
2. Three mental-model cards.
3. Ordered trace steps.
4. Source cards with real repo path and line range.
5. Local syntax highlighting for `.sv`, `.svh`, and `.incl` only.
6. Checklist with localStorage progress.
7. Quiz card.
8. Practice or thought experiment.
9. LLM prompt box.

## Workflow

1. Read the live source file and line range before changing a page.
2. Prefer Part 2 as the baseline, then explain advanced examples as deltas from Part 2.
3. Keep pages self-contained. Do not add CDN CSS/JS.
4. Validate inline scripts with `node --check` after edits.
5. Serve from repo root and verify `http://127.0.0.1:8765/lectures/index.html` returns HTTP 200.

## Common Pitfalls

1. Reading every repeated self-contained file. The repo itself says most examples repeat code. Teach changed files first.
2. Claiming simulator behavior from this host. This machine lacks VCS/Questa/Xcelium, so the lectures are code-reading artifacts unless an EDA environment is provided.
3. Highlighting README/Makefile as SystemVerilog. Detect language from source path.
4. Making explanations without source evidence. Important claims should point to a source excerpt.
5. Forgetting mobile layout. The workbook should remain single-column readable on narrow screens.

## Verification Checklist

- [ ] `lectures/index.html` links every day.
- [ ] Every generated Day page contains `highlightSystemVerilog` and source excerpts.
- [ ] Inline JavaScript passes `node --check`.
- [ ] No remote CSS/JS asset references exist.
- [ ] Preview URL returns HTTP 200.
