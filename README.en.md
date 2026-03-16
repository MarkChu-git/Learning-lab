# Textbook Collection

> Language / 语言：[中文](README.md) | **English**

This repository is a growing textbook collection written for long-term learning.

It is not a temporary folder of scattered tutorials. The goal is to gradually turn worthwhile subjects into textbook-style materials that are readable, structured, and suitable for self-study over time. Each volume is meant to be more than a cheat sheet or a pile of notes. It should become something a learner can read from beginning to end, revisit later, and actually learn from.

## What this project is trying to do

You can think of this repository as a long-term textbook system. It is not trying to “host more tutorials.” It is trying to build real teaching materials volume by volume.

More specifically, the project aims to keep the following qualities:

- **Systematic**: prioritize coherent, structured learning materials instead of fragmented tips.
- **Evidence-based**: rely on stable sources, especially original documents, official references, specifications, and long-lived materials.
- **Explanatory**: answer not only “how,” but also “why,” “how this differs from alternatives,” and “where beginners usually get stuck.”
- **Built for long-term use**: each volume should support expansion, revision, and repeated reading.

## Current active volume

### 1. Typora and Markdown

This is the first volume currently under active expansion. Its focus includes:

- Why Markdown is suitable for long-term writing and knowledge management
- Why Typora is a strong entry tool for both beginners and long-term writing
- The relationship among Markdown, CommonMark, GitHub Flavored Markdown, and Typora’s supported feature set
- Real workflow issues such as images, tables of contents, relative paths, export behavior, YAML, and GitHub rendering differences

Entry points:

- [Volume introduction: Typora and Markdown](books/typora-and-markdown/README.en.md)
- [Chapter 1 overview (English entry)](books/typora-and-markdown/chapters/01-typora-and-markdown.en.md)
- [Original Chapter 1 in Chinese](books/typora-and-markdown/chapters/01-typora-and-markdown.md)

### 2. Git and GitHub

This is now the second officially started volume. Its focus includes:

- what problem version control is actually solving,
- how Git differs from ordinary backup or cloud sync habits,
- what Git is responsible for versus what GitHub is responsible for,
- and the basic logic of commits, branches, remotes, collaboration, and publishing.

Entry points:

- [Volume introduction: Git and GitHub](books/git-and-github/README.en.md)
- [Chapter 1 overview (English entry)](books/git-and-github/chapters/01-why-version-control-matters.en.md)
- [Original Chapter 1 in Chinese](books/git-and-github/chapters/01-why-version-control-matters.md)

## Repository structure

The collection is currently organized by volume. Each volume has its own introduction, chapter directory, and research directory.

This has two practical benefits:

- New volumes can be added later without creating structural chaos.
- Each volume can be maintained, expanded, and researched independently.

```text
textbook-collection/
├── README.md
├── README.en.md
├── CATALOG.md
├── CATALOG.en.md
└── books/
    └── typora-and-markdown/
        ├── README.md
        ├── README.en.md
        ├── chapters/
        ├── images/
        └── research/
```

As the collection grows, more volumes may be added, such as writing tools, knowledge management, research methods, programming foundations, engineering workflows, and algorithms. But the principle stays the same: **write each volume well before opening too many empty tracks.**

## Navigation

For the top-level catalog, see:

- [CATALOG.en.md](CATALOG.en.md)

## Writing method

This project follows a research-first workflow. That means checking documents, comparing standards, and verifying tool behavior before turning the result into textbook prose.

This matters especially for topics like:

- tool differences
- platform differences
- syntax compatibility
- export behavior
- workflow design

These areas should not be written from memory alone. They need to be checked against official documentation, specifications, and actual behavior.

That is why, whenever possible, each volume includes a research map or source index showing what the text is grounded in.

## Current status

The repository is still under construction. The highest-priority work right now is:

- to keep expanding the first volume, *Typora and Markdown*, into a real textbook,
- to stabilize its structure, pacing, and quality standard,
- and only then to replicate that method into future subjects.
