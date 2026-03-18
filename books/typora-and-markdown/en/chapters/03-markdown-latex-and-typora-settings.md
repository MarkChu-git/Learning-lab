# Chapter 3: Markdown Basics, LaTeX Formula Syntax, and Typora Settings

> Language / 语言：[中文](../../zh/chapters/03-markdown-latex-and-typora-settings.md) | **English**

This chapter connects three things beginners often learn separately:

1. Markdown writing syntax,
2. LaTeX-style formulas in Typora,
3. Typora settings that directly affect real writing workflow.

The point is practical:

> do not become a syntax collector — become someone who can produce stable documents quickly.

---

## 1. The right learning order

Use this order:

1. master Markdown skeleton syntax,
2. add formula basics,
3. tune Typora settings to support your workflow.

If you reverse the order (settings first, endless customization first), learning becomes noisy and slow.

---

## 2. Markdown basics you should actually master

### 2.1 Headings = structure, not visual decoration

```markdown
# Title
## Section
### Subsection
```

Headings define document hierarchy, outline behavior, and navigation.

### 2.2 Paragraphs and line breaks

- use paragraphs for complete idea units,
- use forced line breaks only when truly needed.

### 2.3 Lists

Unordered list:

```markdown
- item A
- item B
```

Ordered list:

```markdown
1. step one
2. step two
```

Nested list indentation represents hierarchy.

### 2.4 Blockquotes

```markdown
> This is a note block.
```

Use blockquotes for notes, warnings, side explanations, or extracted statements.

### 2.5 Code blocks

````markdown
```bash
git status
git add .
```
````

Language labels improve readability and syntax highlighting.

### 2.6 Links

```markdown
[Typora](https://typora.io)
```

### 2.7 Images

```markdown
![Workflow Diagram](../images/chapter-03-figure-01.png)
```

Prefer relative paths and stable naming.

### 2.8 Tables

```markdown
| Syntax | Purpose |
| --- | --- |
| `#` | heading |
| `-` | list item |
```

Tables are great for comparisons, not long prose.

### 2.9 Inline emphasis

```markdown
**bold**
*italic*
~~strikethrough~~
```

Use emphasis to support structure, not replace it.

---

## 3. A practical Markdown quick template

```markdown
# Document Title

## 1. Problem
Briefly state what this document solves.

## 2. Prerequisites
- Tool A
- Tool B

## 3. Steps
### 3.1 Step one
### 3.2 Step two

## 4. Common pitfalls
> Put high-frequency mistakes here.

## 5. Summary
List key takeaways.
```

This template is simple, but highly reusable.

---

## 4. Formula basics in Typora (LaTeX subset)

Most beginners only need a practical subset.

### 4.1 Inline formula

```markdown
$f = \frac{1}{T}$
```

### 4.2 Display formula

```markdown
$$
E = mc^2
$$
```

### 4.3 Fractions

```markdown
$\frac{a+b}{c}$
```

### 4.4 Superscripts and subscripts

```markdown
$x^2$
$a_1$
```

### 4.5 Square root

```markdown
$\sqrt{x^2+y^2}$
```

### 4.6 Summation and integral

```markdown
$\sum_{i=1}^{n} i$
$\int_a^b f(x)\,dx$
```

### 4.7 Multi-line aligned formulas

```markdown
$$
\begin{align}
a+b &= c \\
d &= e+f
\end{align}
$$
```

This is enough for most beginner and intermediate technical documents.

---

## 5. Typora settings that matter most

You do not need every setting. Prioritize the ones that directly affect writing quality.

### 5.1 Markdown behavior settings

Check:

- inline math support,
- heading and outline behavior,
- file tree visibility,
- markdown syntax display preferences.

### 5.2 Image handling settings

Prefer a fixed policy:

- copy images into a dedicated folder,
- generate stable filenames,
- keep paths relative.

### 5.3 Workflow-friendly display choices

Turn on the views that reduce cognitive load:

- outline panel,
- file tree,
- clear heading hierarchy visibility.

---

## 6. Typora + Markdown + Git: the practical loop

A reliable daily loop for technical writing:

1. `git pull` before writing,
2. draft in Typora with clear heading structure,
3. add images with relative paths,
4. check formulas render correctly,
5. `git status` / `git diff` before commit,
6. `git add .` + `git commit -m "docs: ..."`,
7. `git push` when done.

This loop turns random drafting into a maintainable workflow.

---

## 7. Frequent beginner mistakes in this stage

1. spending hours on themes before mastering headings and paragraphs,
2. mixing absolute and relative image paths,
3. using formulas without checking rendering in actual target platform,
4. overusing tables for long explanatory text,
5. writing huge commits that combine many unrelated edits.

Fixing these early improves both writing speed and repository quality.

---

## 8. Chapter summary

This chapter’s core message is straightforward:

- Markdown basics build your document skeleton,
- formula basics extend technical expression,
- Typora settings make the workflow sustainable.

When these three layers work together, technical writing becomes faster, clearer, and easier to maintain.

---

## Practice task

Create one chapter file that includes all of the following:

- one heading hierarchy (`#`, `##`, `###`),
- one unordered list,
- one ordered list,
- one blockquote,
- one code block,
- one table,
- one inline formula,
- one display formula,
- one image using a relative path.

Then commit it with a meaningful message.

---

## Next step

After this chapter, continue with the Git volume fast-track:

- [Git and GitHub — Chapter 0 Practical Quick Start](../../git-and-github/chapters/00-practical-quickstart.en.md)
