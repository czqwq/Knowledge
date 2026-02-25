# Copilot Instructions

## Repository Overview

This repository is a GTNewHorizons (GTNH) knowledge base — a collection of Markdown documentation files covering the GT5-Unofficial modpack ecosystem, including its Java APIs, Mixin system, recipe system, machine architecture, item registries, and more.

## Repository Structure

- All content is Markdown (`.md`) files at the repository root.
- There is no build system, test suite, or source code to compile.
- Documentation is bilingual (Chinese primary, English secondary).

## Documentation Standards

- Use Markdown format for all documents.
- Section headings should follow the existing bilingual style (Chinese headings with English technical terms inline).
- Code snippets must be verified against the actual GT5-Unofficial source before inclusion. Do **not** fabricate method names, class names, constants, or API calls.
- Always cite the source file path and line numbers when including code from GT5-Unofficial (e.g., `gregtech/api/enums/GTValues.java:42-50`).
- Documents that include extracted upstream source snippets should start with a notice and the upstream GitHub URL as the code source.

## Key Conventions

- GT5-Unofficial lives at https://github.com/GTNewHorizons/GT5-Unofficial — clone it to `/tmp/GT5-Unofficial` when you need to verify code snippets.
- Use `VP[]` (not `V[]`) for recipe EU/t values. `VP` = `V * 30/32`. `TierEU.RECIPE_*` constants use `VP[]`.
- Item registration is module-specific: GregTech uses `ItemList` enum, GT++ uses `GregtechItemList`, TecTech uses `CustomItemList`, GoodGenerator uses static fields, BartWorks uses static arrays.
- The `README.md` is the master index — update it when adding or significantly changing a document.

## Editing Guidelines

- Make minimal, targeted changes. Preserve existing content and structure unless explicitly asked to change it.
- When adding a new document, follow the existing table format in `README.md` to register it in the index.
- Do not delete or rename existing files without a clear reason.
- All new documentation should follow the existing style: structured Markdown, Chinese section headings, inline English technical terms, code examples with file-path citations.
