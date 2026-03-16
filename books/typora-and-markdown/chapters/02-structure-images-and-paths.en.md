# Chapter 2: Build Documents That Survive Long-Term Maintenance

> Language / 语言：[中文](02-structure-images-and-paths.md) | **English**

Chapter 1 established the writing mindset.

Chapter 2 answers the next practical question:

> how do you organize files so your documents remain stable after weeks and months of revision?

This chapter is less about fancy syntax and more about system durability.

---

## 1. Why syntax alone is not enough

A lot of Markdown beginners can already write headings and lists, but still suffer from:

- broken image links,
- messy folder growth,
- duplicated files with unclear ownership,
- exports that fail unpredictably,
- difficult handoff to collaborators.

The root cause is usually not syntax. It is structure.

---

## 2. The core principle: repository-first thinking

Treat your document project as a repository system, not as isolated files.

A practical baseline layout:

```text
project/
├── README.md
├── chapters/
│   ├── 01-intro.md
│   └── 02-setup.md
├── images/
│   ├── chapter-01-figure-01.png
│   └── chapter-02-figure-01.png
└── references/
    └── source-map.md
```

This layout helps you separate content, media, and evidence.

---

## 3. Why images break first

Markdown files are plain text and usually stable.

Images are external resources. They break when:

- paths depend on one machine,
- files are moved without updating references,
- naming is inconsistent,
- images are copied into random folders.

So image discipline is one of the highest-leverage habits in long-term writing.

---

## 4. Relative paths are the default for maintainable writing

Prefer:

```markdown
![Figure](../images/chapter-01-figure-01.png)
```

Avoid machine-specific absolute paths.

Relative paths travel with the repository and keep documents portable across machines and collaborators.

---

## 5. Typora image behavior: configure once, benefit for months

Set Typora so image handling is predictable:

- images go into a dedicated folder,
- naming stays consistent,
- links remain relative,
- folder structure does not drift over time.

This single setup decision prevents a large class of future maintenance pain.

---

## 6. Naming strategy that actually scales

Use names that encode context and order.

For chapters:

- `01-...md`
- `02-...md`
- `03-...md`

For figures:

- `chapter-01-figure-01.png`
- `chapter-01-figure-02.png`
- `chapter-02-figure-01.png`

Avoid vague names like:

- `image1.png`
- `final.png`
- `new-new.png`

Good naming makes search, diff review, and collaboration much easier.

---

## 7. A practical “insert image” checklist

Before inserting a new screenshot or diagram, check:

- [ ] is the image in the right folder?
- [ ] does the filename include chapter context?
- [ ] is the path relative?
- [ ] does the alt text describe the image purpose?
- [ ] will this still make sense to another person after one month?

That last question catches many hidden problems.

---

## 8. Document hierarchy: who owns what

In a textbook-style repository, each level should have a clear responsibility.

- root `README.md`: project overview and navigation
- top-level `CATALOG.md`: volume map
- per-volume `README.md`: scope and reading path for that volume
- `chapters/`: the real chapter body
- `images/`: local media assets
- `research/` or `references/`: source traceability

When responsibilities are clear, expansion stays clean.

---

## 9. Common failure patterns and quick fixes

### Pattern A: chapter file moved, links broke

Fix: update relative paths in batch and keep chapter/image proximity rules stable.

### Pattern B: duplicate image assets with tiny naming differences

Fix: define one naming standard and refactor old files gradually.

### Pattern C: everyone inserts images in different places

Fix: adopt one shared image policy and write it in volume README.

### Pattern D: “works on my machine only” paths

Fix: ban absolute paths in committed Markdown files.

---

## 10. A minimum maintainability workflow

For every new chapter:

1. create chapter file with numeric prefix,
2. prepare related image names before writing,
3. write with relative links only,
4. run one review pass for path integrity,
5. commit as a coherent change set.

This routine keeps long-term maintenance manageable.

---

## 11. Why this chapter matters even more than it looks

Beginners often underestimate structural work because it feels “non-content.”

In practice, this chapter is one of the biggest quality multipliers in the whole volume.

Strong structure gives you:

- lower breakage rate,
- easier expansion,
- smoother collaboration,
- cleaner Git history,
- and much higher confidence during revision.

---

## 12. Chapter summary

Chapter 2 teaches one central lesson:

> durable writing depends on durable structure.

The key practices are:

- repository-first organization,
- strict relative paths,
- predictable naming,
- clear directory responsibilities,
- and explicit image management discipline.

Master these, and your Markdown workflow stops feeling fragile.

---

## Next step

Continue to Chapter 3:

- [Chapter 3: Markdown Basics, LaTeX Formula Syntax, and Typora Settings](03-markdown-latex-and-typora-settings.en.md)
