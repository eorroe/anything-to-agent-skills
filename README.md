# Anything to Agent Skills

Convert anything into AI agent skills.

## Overview

This repository contains generator skills that transform content from various sources into standardized agent skill definitions (`SKILL.md`). Each skill follows a common template and produces machine-readable, executable skill specifications that agents can load and use.

## Creator Recommendation

The creator recommends letting the AI generate the skills automatically, then manually review and remove any instructions that do not make sense for the AI to follow. After generation, clean up the `SKILL.md` using either another AI pass or a text editor so the final skill is practical and executable.

Even if a generated skill is not executable by AI, or is impossible for AI to execute, the generated skills are still useful for humans to read and follow as structured guidance.

## Priming AI Sessions for MCP Skill Execution

Before executing any generated skill, prime the AI session by loading a corresponding relevant MCP skill into context first. Once the MCP skill is loaded, the AI will use that primed context to properly execute the generated `SKILL.md`.

**Recommended workflow:**

1. Generate a skill using one of the generator skills in this repository.
2. Before running or using that generated skill, load its MCP skill definition into the AI session context.
3. With the MCP skill primed, instruct the AI to execute the generated skill. The AI will follow the primed MCP skill instructions to carry out the generated skill correctly.

This ensures the AI understands the exact execution contract for each English-based, non-code skill before running it.

## Directory Structure

```
anything-to-agent-skills/
├── text-to-agent-skills/        # Create skills from text content
│   ├── SKILL.md
│   └── skill-template.md
├── html-to-agent-skills/        # Create skills from HTML content
│   ├── SKILL.md
│   └── skill-template.md
├── youtube-to-agent-skills/     # Create skills from YouTube content
│   ├── SKILL.md
│   └── skill-template.md
└── github-repo-to-agent-skills/ # Create skills from GitHub repos
    ├── SKILL.md
    └── skill-template.md
```

## Skills

### 1. text-to-agent-skills

**Description:** Create Skills Based Of Text Content

**Expected Prompt Arguments:**
- Text Based File
- Directory of Text Based Files
- Raw Text

**How to Use:**

| Input Type | Example Prompt |
|------------|----------------|
| Text Based File | Provide a local text file containing instructions, methodology, or workflow to convert into a skill. |
| Directory of Text Based Files | Provide a directory path containing multiple text files to convert into multiple skills. |
| Raw Text | Paste raw text content directly into the prompt to convert into a skill. |

**Skill Directory Naming Convention:**

- **Text Based File:** Use the Text File Title Case Initials as prefix + actionable text derived from content (e.g., `TFN-TEXT-TEXT-TEXT`)
- **Directory of Text Based Files:** Use the Directory Name Title Case Initials as prefix + actionable text derived from content (e.g., `DN-TEXT-TEXT-TEXT`)
- **Raw Text:** Analyze the raw text for intent and use actionable text derived from content (e.g., `TEXT-TEXT-TEXT`)

---

### 2. html-to-agent-skills

**Description:** Create Skills Based Of HTML Content

**Expected Prompt Arguments:**
- Single Web Link URL That Returns HTML
- Sitemap.xml file

**How to Use:**

| Input Type | Example Prompt |
|------------|----------------|
| Single Web Link URL That Returns HTML | Provide a URL that returns HTML content to convert into a skill (e.g., `https://example.com/guide`). |
| Sitemap.xml file | Provide a sitemap.xml URL to generate multiple skills from each page in the sitemap (e.g., `https://example.com/sitemap.xml`). |

**Skill Directory Naming Convention:**

- Use the Website Origin Title Case Initials as prefix + actionable text derived from content (e.g., `TCO-TEXT-TEXT-TEXT` for `TitleCasedOrigin.com`)

**Note:** The skill uses `web_fetch` to retrieve raw HTML content. Ensure the URL is accessible and returns HTML.

---

### 3. youtube-to-agent-skills

**Description:** Create Skills Based Of YouTube Content

**Expected Prompt Arguments:**
- Single YouTube Video Link URL
- YouTube Videos Playlist Link URL
- YouTube Channel Link URL (Channel Videos URL)

**How to Use:**

| Input Type | Example Prompt |
|------------|----------------|
| Single YouTube Video Link URL | Provide a YouTube video URL to convert the transcript and content into a skill (e.g., `https://www.youtube.com/watch?v=abc123`). |
| YouTube Videos Playlist Link URL | Provide a YouTube playlist URL to create skills from every video in the playlist. |
| YouTube Channel Link URL | Provide a YouTube channel `/videos` URL to create skills from all videos in the channel. |

**Skill Directory Naming Convention:**

- Use Channel Name Title Case Initials as prefix (e.g., `UCN` for `UserChannelName`)
- Use program name if found in video transcript as the 2nd part
- Use actionable text derived from video title or description for the suffix (e.g., `UCN-PROGRAMENAME-TEXT-TEXT-TEXT`)

**Note:** The skill uses `yt-dlp` to extract transcripts and metadata. No YouTube API is required.

**yt-dlp Command Reference:**
```bash
yt-dlp --skip-download --write-sub --write-auto-sub --sub-lang en --sub-format json3 <youtube video URL>
```

---

### 4. github-repo-to-agent-skills

**Description:** Create Skills Based Of GitHub Repo Content

**Expected Prompt Arguments:**
- GitHub Repository Link URL
- GitHub Repository Tree Directory Folder URL
- GitHub Repository File URL

**How to Use:**

| Input Type | Example Prompt |
|------------|----------------|
| GitHub Repository Link URL | Provide a GitHub repository URL to analyze the full repo and convert it into a skill (e.g., `https://github.com/owner/repo`). |
| GitHub Repository Tree Directory Folder URL | Provide a GitHub directory URL to analyze all files in that directory and their dependencies. |
| GitHub Repository File URL | Provide a GitHub file URL to analyze the file and its imported dependencies. |

**Skill Directory Naming Convention:**

- Use GitHub Account Name Title Case Initials as prefix (e.g., `GAN` for `GithubAccountName`)
- Use GitHub Repository Name Title Case Initials as the 2nd part (e.g., `RN` for `RepoName`)
- Use actionable text derived from the GitHub URL content for the suffix (e.g., `GAN-RN-TEXT-TEXT-TEXT`)

**Note:** The skill clones the repository to the local filesystem for analysis, then deletes it after creating the `SKILL.md` file.

---

## Skill Template

All generated skills must follow the `skill-template.md` format. The template includes these required sections:

1. **Frontmatter** (YAML) - name, description, category, risk, source, source_repo, source_type, date_added, author, tags, tools
2. **Skill Title**
3. **Overview** - Brief explanation of what the skill does
4. **When to Use This Skill** - Scenarios and use cases
5. **How It Works** - Step-by-step instructions
6. **Examples** - Code examples and use cases
7. **Best Practices** - Do's and don'ts
8. **Limitations** - What the skill does not cover
9. **Security & Safety Notes** - Preconditions, caveats, and safety gates
10. **Common Pitfalls** - Known issues and solutions
11. **Related Skills** - Complementary or alternative skills

## Common Behavior

All generator skills share these mandatory behaviors:

1. **Prioritize User Input:** Always prioritize the user's latest words over own thinking.
2. **Goal Verification:** Use `ask_user` or `question` tool to grill the user for an explicit desired goal, then repeatedly ask for feedback on goals, non-goals, and ambiguities until a clear understanding is achieved. Ask for confirmation to proceed.
3. **Context Check:** If session context is at 50% or more, offer to execute in a new session.
4. **Metrics Logging:** Always create or update `SKILLNAME-Execution-Metrics.md` after execution, and check for existing metrics before executing to avoid repeating previous mistakes.
5. **Template Compliance:** All created skills must match `skill-template.md` exactly with 0 discrepancies.
6. **Avoid `&&` in Shell Commands:** Execute shell commands sequentially to avoid failures.
7. **File Deletion Permission:** Always ask for permission before deleting files or using `git reset`, `git restore`, or `git checkout`.
8. **Sub Agent Requirement:** All tool calls must run using sub agents. Each agent must only write to 1 file. The Main Agent must never perform reads, edits, or updates.
9. **Verification Loop:** Scan created `SKILL.md` against the template, rewrite ambiguous text to be explicit, and loop until 0 ambiguity is found.
10. **Duplicate Skills Tracking:** Check for and maintain a `Duplicate-Skills.md` file listing skills with similar functionality.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```text
MIT License

Copyright <YEAR> <COPYRIGHT HOLDER>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
