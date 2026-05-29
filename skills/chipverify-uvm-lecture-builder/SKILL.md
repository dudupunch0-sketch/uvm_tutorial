---
name: chipverify-uvm-lecture-builder
description: Use when creating or updating Korean HTML workbook pages under lectures_chipverify_uvm/ based on ChipVerify UVM tutorial source URLs. Produces URL-attributed, re-authored learning pages without mirroring source articles.
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [uvm, systemverilog, chipverify, learning, html, lecture-material]
    related_skills: [html-preview-server, waza-learn, waza-read]
---

# ChipVerify UVM Lecture Builder

## Overview

This project-local skill preserves the workbook format used by `lectures/` while targeting a separate ChipVerify-source-guided lecture set under `lectures_chipverify_uvm/`.

The output is a Korean interactive workbook page: source URL cards, mental-model cards, reading trace, directly authored compact SystemVerilog/UVM mini examples, progress checklist, quiz, practice prompt, and LLM question template.

## Source and copyright guardrail

- Use ChipVerify pages as source URLs and topic anchors.
- Do not mirror or bulk-copy full article bodies.
- Do not paste long original code blocks from ChipVerify.
- Prefer short, directly authored mini examples that teach the same UVM concept.
- Every Day page should link to the original ChipVerify URLs used for attribution and manual reading.

## Current Curriculum

See `references/curriculum.md` for the Day 0-30 map.

Generated index:

- `lectures_chipverify_uvm/index.html`

## Page Contract

Each Day page should contain:

1. Korean title, goal, and completion criterion.
2. ChipVerify source URL cards.
3. Three mental-model cards.
4. Ordered reading trace.
5. Directly authored SystemVerilog/UVM mini example.
6. Source question card that maps the page back to original topics.
7. Checklist with localStorage progress.
8. Quiz card.
9. Practice or thought experiment.
10. LLM prompt box.

## Verification Checklist

- [ ] `lectures_chipverify_uvm/index.html` links every day.
- [ ] Every Day page contains source URL cards, checklist, quiz, prompt, and `highlightSystemVerilog`.
- [ ] Inline JavaScript passes `node --check`.
- [ ] No remote CSS/JS assets are referenced.
- [ ] Internal links resolve.
- [ ] Preview URL returns HTTP 200.
