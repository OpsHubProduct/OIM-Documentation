**OpsHub-GitBook Help Guide**

**Complete Workflow Guide: Creating, Committing, and Publishing Markdown Files to GitBook via GitHub**

This guide explains, step by step, how to edit, commit, and publish Markdown files (`.md`) in GitHub so that they appear correctly in GitBook.

# Understanding the Basics

## What is GitHub?
- Think of GitHub as an online folder where your documentation files live.
- Multiple people can edit these files.

## What is GitBook?
- GitBook reads your Markdown files from GitHub and displays them as a website.

## What is Markdown (.md)?
- A simple text format used for writing documentation.
- GitBook fully supports Markdown.

# Creating and Editing Pages in GitBook

## How to Edit an Existing Page
1. Locate the page in the folder hierarchy.  
   Each page in GitBook maps directly to a file in the GitHub repository.
   <p align="center">
   <img src="../assets/ContributorGuide_Images/repo-structure-gitbook.png"/>
   </p>
2. Make required changes (content, formatting, links, images, etc.).
3. Commit the changes.

## When You Add a New Page

{% stepper %}  
{% step %}
### Use the correct file name
- Use lowercase letters.
- Do not use spaces.
    - Use dashes (`-`) between words.

      Example:
      `database-configuration.md`
      {% endstep %}  
      {% step %}
### Add the page to `SUMMARY.md`
- GitBook only shows pages listed in `SUMMARY.md`.
  Example:
   ```markdown
      - [Database Configuration](docs/integrate/database-configuration.md)
   ```
{% endstep %}  
{% step %}
### Commit both files together
- Make sure that:
    - Your new .md file and the update summary.md file are committed in the same commit.
      <p align="center">
        <img src="../assets/ContributorGuide_Images/summary-file.png" />
   </p>
{% endstep %}  
{% endstepper %}

# How to Add a New Connector Entry

To list a new connector in the documentation, follow the steps below. These steps ensure the connector appears correctly in the Connectors list, Supported Connectors table, and the GitBook sidebar.

{% stepper %}    
{% step %}
## Add Connector Documentation Page
- Create a new markdown file inside the `connectors` folder.
  > **Example:** connectors/snow-quick-connect.md

{% endstep %}   
{% step %}
## Add Logo in Assets Folder
- Place the connector logo in: `assets/connector/` directory.
- **Logo requirements**
    - Background color: `#EDF4FD`
    - Background box: **536px × 161px**
    - Logo size: **72px × 72px**
  > **Example file:** `assets/connector/servicenow.png`

{% endstep %}  
{% step %}

## Add Entry in `connectors.md`
- Use the table/card layout format.
  > **Example:**
  > ```html
    > <tr>
    > <td align="center"><mark style="color:#555555"><strong>ServiceNow Quick Connect</strong></mark></td>
    > <td><a href="../assets/connector/70_servicenow.png">ServiceNow Quick Connect</a></td>
    > <td><a href="servicenow-quick-connect.md">servicenow-quick-connect.md</a></td>
    > </tr>
    > ```  

{% endstep %}  
{% step %}
## Add Entry in `supported-connectors.md`
- Include supported versions and entities in the table format.

{% endstep %}  
{% step %}
## Add Entry in `SUMMARY.md`
- Include the connector under the Connectors section for sidebar navigation.
  > **Example:**
  > ```markdown
    > * [Connectors](connectors/connectors.md)
    >   * [ServiceNow Quick Connect](docs/connectors/servicenow-quick-connect.md)
    > ```

{% endstep %}  
{% endstepper %}

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
`![](../assets/image-name.png)`

### Example
`![](../assets/integration-configuration.png)`

### Centered Image
`<p align="center">
<img src="../assets/default-image-1.png" width="700">
</p>`

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
## YouTube Video Embed
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

## Markdown Table

| Column 1 | Column 2 |
|----------|----------|
| Value 1  | Value 2  |

## Card View HTML Table
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

## Variable File (`vars.yaml`)
```
SITENAME: "OpsHub Integration Manager"
```

## Usage
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
