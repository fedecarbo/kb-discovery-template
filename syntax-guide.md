# Markdown syntax guide

A reference of allowed markdown constructs. When writing markdown, anything in this document is fair game. Anything in **Avoid** at the bottom is not.

## Headings

Six levels. `h1` is normally the document title and appears once. Every heading is given an automatic anchor based on its text.

# Level 1 — page title
## Level 2 — major section
### Level 3 — subsection
#### Level 4 — topic
##### Level 5 — eyebrow (uppercase)
###### Level 6 — eyebrow (uppercase)

## Paragraphs and inline formatting

A regular paragraph. Wrap text naturally — line breaks inside a paragraph become spaces.

Leave a blank line for a new paragraph.

**Bold text** with `**double asterisks**`. *Italic text* with `*single asterisks*`. ***Both*** with `***triple***`. ~~Strikethrough~~ with `~~tildes~~`. `Inline code` with single backticks. <mark>Highlighted text</mark> via raw `<mark>` HTML. Press <kbd>⌘</kbd> + <kbd>K</kbd> using raw `<kbd>` HTML. Footnote reference like this[^one]. Superscript via raw HTML: E = mc<sup>2</sup>. Subscript: H<sub>2</sub>O.

## Links

Inline link: [external site](https://example.com).

In-page link: [jump to footnotes](#footnotes) — uses a heading's auto-generated `id`.

Autolink: <https://example.com>.

## Lists

Bullet list:

- First item
- Second item
  - Nested bullet
  - Another nested item
- Third item

Ordered list:

1. Step one
2. Step two
3. Step three

Mixed nesting works too:

1. Outer step
   - Inner bullet
   - Another inner
2. Next outer step

## Task lists

Use `- [ ]` and `- [x]`.

- [x] Completed item
- [x] Another completed item
- [ ] Open item
- [ ] Another open item

## Tables

Pipes and dashes. Header alignment is set in the divider row: `:--` left, `:-:` centre, `--:` right.

| Column A           | Column B   | Column C                          |
| ------------------ | :--------: | --------------------------------: |
| Left-aligned       |  Centred   |                    Right-aligned |
| Short              |  Medium    |              Some longer content |
| Another row        |  More      |                       Final cell |

## Blockquotes

> Plain blockquote. Use a `>` at the start of each line.
>
> Add more lines for multiple paragraphs.
>
> — Attribution in italics looks good at the end.

## Alerts

GitHub-flavoured alerts. Five types: `NOTE`, `TIP`, `IMPORTANT`, `WARNING`, `CAUTION`. Put `> [!TYPE]` on its own line, then the body lines below.

> [!NOTE]
> Highlights useful information the reader should notice even when skimming.

> [!TIP]
> Optional suggestions that improve the outcome.

> [!IMPORTANT]
> Crucial information needed to succeed.

> [!WARNING]
> Urgent info that needs immediate attention to avoid problems.

> [!CAUTION]
> Negative potential consequences of an action.

## Code

Inline: `const greeting = "hello"`.

Fenced block with a language hint:

```js
function debounce(fn, wait = 200) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), wait);
  };
}
```

```python
from dataclasses import dataclass

@dataclass
class Note:
    title: str
    body: str
```

```bash
# Open the viewer
open index.html
```

A fenced block with no language hint:

```
SELECT id, title FROM notes WHERE archived = false;
```

## Images

Plain image:

![A placeholder](https://images.unsplash.com/photo-1499951360447-b19be8fe80f5?w=800&q=80)

Image with a title — title becomes the caption:

![Iceberg](https://images.unsplash.com/photo-1531366936337-7c912a4589a7?w=800&q=80 "An iceberg in calm water")

## Horizontal rule

Three dashes on their own line. Use as a major section break.

---

## Collapsible sections

Use raw HTML `<details>` and `<summary>`. The summary is the always-visible label; the rest expands on click.

<details>
<summary>Click to expand</summary>

The body can contain any markdown — paragraphs, lists, code blocks, even nested `<details>`.

- Inline `code`
- **Bold** and *italics*

</details>

## Footnotes

Reference a footnote inline with `[^id]`, then define it anywhere in the document. Definitions collect themselves into a section at the bottom.

Here's a sentence with a reference[^example] and another one[^bringhurst].

[^one]: This is the footnote that the very first reference up top points to.
[^example]: Footnote definitions can be written on a single line.
[^bringhurst]: They can also span multiple paragraphs if you indent the body — useful for fuller citations.

## Avoid

These constructs will either render incorrectly or as raw text — don't use them:

- **LaTeX / math** — no KaTeX or MathJax. Write equations as plain text or code.
- **Mermaid diagrams** — fenced `mermaid` blocks render as plain code.
- **Definition lists** (`term : definition`) — not parsed; use a bullet list instead.
- **Custom admonition syntax** (`!!! note`, `::: warn`) — not parsed. Use the alert syntax above (`> [!NOTE]`) instead.
- **YAML / TOML frontmatter** — appears as raw text at the top of the document.
- **Wiki-style links** (`[[page]]`) — render as literal characters.
- **Inline HTML beyond the safelist** — `<details>`, `<summary>`, `<kbd>`, `<mark>`, `<sub>`, `<sup>` are safe; other raw HTML may not render as expected.
