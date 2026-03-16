# Chapter 2: Writing Documents That Can Survive Long-Term Maintenance

> Language / 语言：[中文原文](02-structure-images-and-paths.md) | **English entry**

## Status

This is currently an **English entry page**, not yet the full translated body of the Chinese chapter.

For now:

- the Chinese chapter remains the complete main text;
- this page explains the chapter’s purpose, scope, and structure in English;
- the complete English version can be expanded progressively later.

## What this chapter is about

If Chapter 1 explains why Markdown and Typora matter as writing tools, Chapter 2 moves to the next level:

> How do you organize documents so that they remain stable, readable, and maintainable over time?

This chapter shifts the focus from single-document writing to multi-document structure.

Its central claim is that long-term stability usually depends less on isolated syntax and more on:

- directory structure,
- image management,
- relative paths,
- naming discipline,
- and the overall organization of a textbook repository.

## Core themes covered in the Chinese chapter

The original Chinese chapter currently develops the following themes in detail:

1. **Syntax alone does not make a document system durable**
   - Long-term document life depends on structure.
   - A textbook project must be designed as a system, not as a pile of files.

2. **Directory structure is not decoration**
   - It helps separate responsibilities across levels.
   - It reduces future confusion before confusion starts.

3. **Images are usually the first thing that breaks**
   - Markdown files are stable text.
   - Images are external resources and fail as soon as references become unstable.

4. **Relative paths are the lifeline of a repository-based writing workflow**
   - They move with the repository structure.
   - They are far more robust than machine-specific absolute paths.

5. **Typora helps with more than just dragging images in**
   - It can support image copying into a stable folder.
   - It can help preserve cleaner relative references.

6. **Naming discipline matters early**
   - chapter files should use stable numbering;
   - image names should reflect chapter relationships;
   - future maintenance becomes much easier when naming is predictable.

7. **A textbook repository should have layer-specific responsibilities**
   - root README,
   - top-level catalog,
   - per-volume README,
   - chapter directory,
   - image directory,
   - research directory.

8. **Practical actions matter more than abstract understanding**
   - build the directory before writing,
   - treat images as first-class document resources,
   - keep relative relationships stable,
   - treat README and catalog files as part of the teaching path.

## Recommended way to read this chapter

If you are reading in English at this stage, use this page as a structural guide first.

Then:

- move into the Chinese original for the full explanatory body,
- pay special attention to the sections on relative paths and image management,
- and use the repository structure examples as concrete workflow references.

## Next step for the English version

The next expansion pass for this chapter should translate and refine the full body, especially the parts on:

- repository structure logic,
- image failure patterns,
- relative path discipline,
- naming strategy,
- and the recommended textbook repository layout.
