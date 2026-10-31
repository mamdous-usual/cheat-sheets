# Markdown Cheat Sheet

## 1. Headings

```markdown
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
```

## 2. Text Formatting

```markdown
**Bold text**
*Italic text*
~~Strikethrough~~
`Inline code`
```

## 3. Paragraphs and Line Breaks

```markdown
First paragraph.

Second paragraph.

Line one  
Line two
```

## 4. Lists

**Unordered list**
```markdown
- Item
- Item
  - Nested item
```

**Ordered list**
```markdown
1. First
2. Second
3. Third
```

**Task list (GitHub)**
```markdown
- [x] Completed
- [ ] Not completed
```

## 5. Links

```markdown
[OpenAI](https://openai.com)
<https://example.com>
```

## 6. Images

```markdown
![Alt text](image.png)
```

## 7. Blockquotes

```markdown
> This is a quote.
>
> > Nested quote.
```

## 8. Code

**Inline code**
```markdown
Use `print()` to display output.
```

**Code block**
````markdown
```python
print("Hello, world!")
```
````

## 9. Horizontal Rule

```markdown
---
```

## 10. Tables

```markdown
| Name | Age |
|---|---:|
| Alex | 20 |
| Sam | 22 |
```

Use `:---` for left alignment, `:---:` for center, and `---:` for right.

## 11. Escaping Characters

Add `\` before a Markdown character to display it literally.

```markdown
\*Not italic\*
\# Not a heading
```

## 12. Useful GitHub Markdown

**Alerts**
```markdown
> [!NOTE]
> Useful information.

> [!TIP]
> A helpful suggestion.

> [!WARNING]
> Important warning.
```

**Collapsible section**
```html
<details>
<summary>Show details</summary>

Hidden content goes here.

</details>
```

**Mention a user**
```markdown
@username
```

**Reference an issue or pull request**
```markdown
#123
```

## Quick Reference

| Syntax | Result |
|---|---|
| `# Heading` | Heading |
| `**text**` | **Bold** |
| `*text*` | *Italic* |
| `~~text~~` | ~~Strikethrough~~ |
| `` `code` `` | `code` |
| `> quote` | Blockquote |
| `---` | Horizontal rule |
| `[text](url)` | Link |
| `![alt](url)` | Image |
| `- item` | Bullet list |
| `1. item` | Numbered list |
| `- [ ] task` | Task list |
