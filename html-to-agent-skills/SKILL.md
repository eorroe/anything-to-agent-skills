---
name: html-to-agent-skills
description: Create Skills Based Of HTML Content
---

# Requirements / Mandatory
1. Always no exception prioritize the users latest recent words (input / prompts) over own thinking.

## Tool Calls
1. Avoid any use of '&&' when running shell commands as it usually fails. Just execute commands sequentially.
2. Always no exception ask for permission to delete files or use git reset or git restore or git checkout to restore files to avoid losing untracked changes.
3. Always use web_fetch tool call to fetch raw HTML content to use to create SKILL.md file.
4. Must use sub agents for every tool call when executing skill behavior.

## Using Agents
1. All tool calls must run using sub agents.
2. Each agent must only write to 1 file (multiple writes but only ever 1 file).
3. Agents may read from multiple files but never write to more than 1 file.
4. Must never with no exception perform any tool call like reads, edits or updates on Main agent.
5. Even small edits like 1 line of code changes must run on sub agent separate from Main Agent.
6. Only use Main Agent for communicating and orchestrating with sub agents and communicating with user.

## Created Skill.md Files
1. All Skills must follow and have a minium of all sections of the "skill-template.md" file. Use the provided template exactly as provided. Never create own template.
2. All Skills must include and follow "Using Agents" section.
3. All Skills must start off with explicit behavior instructions to ask user using ask_user or question tool to grill user of explicit desired goal to achieve when using and executing skill until derive at desired goal.
4. All Skills after asking user for goal must have explicit behavior instructions to ask user using ask_user or question tool to grill user for a clear way to verify the desired goal from results of executed skill.
5. All Skills must have explicit behavior instructions to always create a directory and files of metrics (SKILLNAME-Execution-Metrics.md) of every execution of the skill for the skill to analyze before executing user provided goal. Therefore all skills must check for existing metrics created by skill before actually executing skill behavior after user provides goal of skill output results.
6. All Skills must have explicit behavior instructions to check if the session context is at 50% or more. If session context skill is executed in is below 50% proceed to execute skill behavior in session. If context is at 50% or more provide option to execute skill behavior in new session.

# Expected Prompt Arguments
1. Single Web Link URL That Returns HTML
2. Sitemap.xml file

# Naming Skill Directory
1. Use Website Origin Title Case Initials as prefix
2. Use actionable text derived from content for 2nd part / rest of skill name (suffix) using "TEXT-TEXT-TEXT" convention

Examples:

When Site URL: TitleCasedOrigin.com

Final Skill Name: TCO-TEXT-TEXT-TEXT

When Site URL: Titlecasedorigin.com

Final Skill Name: Titlecasedorigin-TEXT-TEXT-TEXT

When Site URL: lowercaseorigin.com

Final Skill Name: lowercaseorigin-TEXT-TEXT-TEXT


# Identifying and Verifying Skill Execution Goal
1. In laymens terms from user experience perspective explain in detail what is understood from user prompt in skill execution.

2. Analyze the prompt.

3. Explain in detail what is understood from the prompt.

4. Explain the goals from what is understood from the prompt.

5. Explain the non goals from what is understood from the prompt.

6. Explain the plan of action from the understood prompt.

7. Explicitely and in detail explain how the prompt could be improved, list out what is ambiguius and implicit then how could be without ambiguity and be explicit.

8. Use ask_user or question tool to ask whether correct or ask for feedback from user on goals, non goals, and implicit ambiguity.

9. Ask for confirmation to proceed with updated goals, non goals and optimized prompt.

10. Use ask_user or question tool repeatedly until derive at a clear understanding of how to confirm and validate whether goals are achieved before moving to next step. Use suggested options.



# Creating Skills

Single Web Link URL That Returns HTML

1. Identify origin URL name (follow "Naming Skill Directory" instructions)

2. Create folder directory following "Naming Skill Directory" above.

4. Analyze full HTML content.

5. Identify every and all actionable parts of the full HTML content.

6. From every identified actionable parts synthesis the behavior and intent of what is being taught in the full HTML content into 1 sentence to use as Skill "Description".

7. Identify step by step instructions from the full HTML content.

8. Read the "skill-template.md" file completely to use as reference for creating "SKILL.md" file in next steps. Document required sections and verify them before file creation.

9. Create a SKILL.md file using template "skill-template.md" file in directory populated with step by step instructions of what is taught in full HTML content.

10. Update SKILL.md file with duplicate parts of the template that make sense to have duplicate sections for different parts of the actionable identified parts of full HTML content.

11. Update SKILL.md behavior instructions to always start of using ask_user or questions tool to ask user of desired goal results output when using skill. (Include Instructions  "Identifying and Verifying Skill Execution Goal" above)

12. If SKILL.md file does not already have a way to verify user goal with skill execution based of full HTML content update SKILL.md behavior instructions to always use ask_user or questions tool to ask user how to verify whether goal has been achieved.

13. Update SKILL.md behavior instructions to always check for existing "SKILLNAME-Execution-Metrics.md" file for previous results of skill executed to analyze before executing skill behavior instructions in order to avoid any previous mistakes made from executing skill.

14. Update SKILL.md behavior instructions to always end with creating "SKILLNAME-Execution-Metrics.md" populating or appending results from skill execution with timestamp and prompt provided to skill use execution.


Sitemap.xml file

1. Run parallel sub agents for every URL in the provided sitemap xml URL to follow the above "Single Web Link URL That Returns HTML" instructions.


# Verifying Skills (Loop)
1. Scan created SKILL.md file and compare it section-by-section against the template file, update file to make sure has all sections from "skill-template.md" file. Only proceed when created file has all sections and follows template with 0 discrepancies.
2. Scan created SKILL.md file and find all ambiguious text.
3. Update SKILL.md files with rewrite of found ambiguious text to be explicit.
4. Loop scanning and updating SKILL.md until find 0 ambiguious text upon each scan execution. Report 0 ambiguity found after reapeatedly scanning and updating the SKILL.md file.

# Identifying Duplicate Skills
1. Check for existing "Duplicate-Skills.md" markdown file.
2. Create or append to markdown file "Duplicate-Skills.md" populated with list of skills that have similar functionality to other created SKILL.md files.
3. Populate the "Duplicate-Skills.md" file with table formatted group of duplicate skills with their differences so user can easily decide whether to keep duplicates or remove duplicate skills.

# Behavior
1. Analyze prompt arguments
2. Identify prompt arguments for Expected Prompt Arguments.
3. For every skill creating run parallel agents to follow "Creating Skills Instructions" above.
4. For every skill created run parallel agents to follow "Verifying Skills Loop" Instructions.
5. Follow Identifying Duplicate Skills.
6. Report To User and Standby For Instructions.