# GitBook Markdown Basics

Reference: https://gitbook.com/docs/creating-content/formatting

## 1. Headings (Titles and Sections)
Use the `#` symbol to create headings.

```
# H1 – Main Page Heading
## H2 – Section Heading
### H3 – Subsection Heading
```

✔ GitBook only shows **H1 and H2** in the left Table of Contents  
✔ Do **not skip levels** (H1 → H2 → H3 in order)

## 2. Text Styling

| Formatting Type | How to Write It        | Example Output |
|-----------------|------------------------|----------------|
| **Bold** | `**Bold text**`        | **Bold text** |
| *Italic* | `*Italic text*`        | *Italic text* |
| Inline Code | ``` `OIM_HOME/bin` ``` | `OIM_HOME/bin` |
| Strikethrough | `~~Incorrect text~~`   | ~~Incorrect text~~ |

## 3. Lists

### Bullet List

`* First point`  
`* Second point`  
> **Outcome:**
> * First point  
> * Second point

or

`- First point`  
`- Second point`  
> **Outcome:**
> - First point
> - Second point

### Numbered List

1. Step one
2. Step two
3. Step three

## 4. Notes and Warnings

> **Note:** Restart service after configuration.

> **Warning:** Do not delete this folder.

## 5. Angle Brackets `<` and `>`

| Purpose | How to Write It | Correct Output |
|---------|------------------|----------------|
| Escape `<` and `>` | `&lt;tag&gt;` instead of `<tag>` | `<tag>` |

## 6. Code Blocks (Multiple Lines)

### JSON Example
```json
{
  "name": "OpsHub",
  "version": "1.0"
}
```

### XML Example
```xml
<configuration>
  <setting key="timeout">30</setting>
</configuration>
```

### Bash Example
```bash
echo "Hello, OpsHub"
```

# Images

## Image Storage

- All images must be placed inside the **assets** folder.
- Each project folder must reference images from this central directory.

## Image Reference Syntax

### Basic Image
![](../assets/image-name.png)

### Example
![](../assets/integration-configuration.png)

### Centered Image
<p align="center">
  <img src="../assets/default-image-1.png" width="700">
</p>

## Image Naming Rules

- No spaces  
- Use lowercase  
- Use dashes or underscores  

## Image Path Guidelines

| Page Location | Correct File Path | Markdown Example |
|---------------|-------------------|------------------|
| integrate/advanced-scenario/source-delete-sync.md | `../../assets/x.png` | `![Source Delete Example](../../assets/x.png)` |
| help-center/error.md | `../assets/x.png` | `![Error Handling](../assets/x.png)` |

# Embedding Videos

### YouTube Video Embed
```
{% embed url="https://youtu.be/Po6K9_UXrfM" %}
```

# Reusable Content

Reusable files live in `.gitbook/includes`.

Include using:
```
{% include "../.gitbook/includes/windows-specific-configuration.md" %}
```

# Links

| Type | Example |
|------|---------|
| Internal | `[Integration Setup](../integrate/setup.md)` |
| External | `[OpsHub Website](https://www.opshub.com)` |
| Anchor | `[Go to Configuration](#configuration)` |

# Tables

### Markdown Table

| Column 1 | Column 2 |
|----------|----------|
| Value 1  | Value 2  |

### Card View HTML Table
```html
<table data-view="cards" data-full-width="false">
  <thead>
    <tr>
      <th align="center" data-card-cover></th>
      <th data-hidden data-card-target data-type="content-ref"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center"><strong>Example Title</strong></td>
      <td><a href="path/to/doc.md">Example Link</a></td>
    </tr>
  </tbody>
</table>
```

# Conditional Blocks

```
{% if "OpsHub Integration Manager" === space.vars.SITENAME %}
... content
{% endif %}
```

### Variable File (`vars.yaml`)
```
SITENAME: "OpsHub Integration Manager"
```

### Usage
This site describes <code class="expression">space.vars.SITENAME</code> features.

# Troubleshooting

1. **Page not visible?**  
   - Added to SUMMARY.md?  
   - Correct indentation?  
   - Correct filename?

2. **Broken internal links?**  
   - File exists?  
   - Path correct?  
   - Heading anchor correct?

3. **Images not loading?**  
   - Inside assets folder?  
   - Lowercase name?  
   - Path correct?

4. **Table issues?**  
   - Aligned pipes?  
   - Equal columns?

5. **Code block issues?**  
   - Triple backticks correct?

6. **Layout issues?**  
   - Remove extra blank lines  
   - Maintain heading hierarchy

7. **Anchor link issues?**  
   - Unique headings  
   - Avoid symbols
