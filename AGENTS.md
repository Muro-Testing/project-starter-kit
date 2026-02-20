# AGENTS Instructions

## Phase 1: Discovery - Ask Questions First

**Before ANY planning or coding, you MUST understand the data!**

A project built without understanding data is like building a house without knowing what's going inside. Ask these questions:

### Data Discovery Questions

Ask the user (in natural conversation):
1. **What data will you work with?** (inputs)
   - Where does data come from? (API, files, user input, database, external services?)
   - What format is it in? (JSON, CSV, databases, real-time streams?)

2. **What should the output be?** (results)
   - What does the end result look like?
   - Who is the end user?

3. **Processing needs**
   - What needs to happen to the data? (transform, analyze, aggregate?)
   - Any specific rules or business logic?

4. **Constraints**
   - Any limits? (real-time? offline? specific tech requirements?)

### Example
```
Agent: Cool, you want a dashboard! Before I plan anything, I need to understand the data:
- What data will feed this dashboard?
- Will it come from APIs, files, or will users manually input it?
- What do you want to see in the final dashboard?
- Any specific metrics or insights you need?

User: [answers...]

Agent: Perfect! Now I understand. Let me search for skills and create a plan.
```

---

## Phase 2: Skill Loader - Find Relevant Skills

**Always search for relevant skills first!**

Before beginning any task, feature, or project work, you must check if there's a relevant skill in the Antigravity Awesome Skills catalog that can help improve quality and efficiency.

### How to Find Skills

1. **Activate the skill-loader skill** - Say: "I need to use the skill-loader skill"
2. **Describe what you're working on** - Tell the skill what kind of task you're doing in plain language
3. **Review the suggestions** - Look at matching skills and their descriptions
4. **Install relevant skills** - Install the skills that match your needs
5. **Activate and use** - Use the installed skill to guide your work

### Example
```
User: "I want to build a React app with authentication"
Agent: [searches catalog, finds matching skills]
Found: react-best-practices, auth-implementation-patterns, clerk-auth
```

---

## Required Workflow - Project Management

### 1. Task Execution
- When asked to make changes, especially multiple changes at once, create a file with time/date
- Write down the plan as a checklist
- **Only do ONE task at a time**
- After finishing a task, ask the user should you continue with the next task
- This avoids context window issues

### 2. Before Pushing
- Summarize changes in plain English
- Confirm which files are included/excluded from the push

### 3. After Pushing
- Append to `docs/CHANGELOG_CUSTOM.md` with:
  - Date (YYYY-MM-DD)
  - Bullet list of changes
  - Files touched
  - **Do not push this file**

### 4. Log Format Example
```markdown
## 2026-02-20
- Added user authentication flow
- Fixed login validation bug

Files touched
- App.tsx
- components/Auth.tsx
```

### 5. Error Fixes
- Remember what and how errors were fixed
- If confirmed fixed, add to project context to prevent future issues

---

## Project Context

- Start every new session by reading `PROJECT_CONTEXT.md`
- If no context doc after couple of iterations, build and update it
- Scan top-level repo structure before making changes
- Review all existing plan documents in `docs/` (e.g., `docs/plan-*.md`)
- Check `CHANGELOG_CUSTOM.md` for latest changes

---

## Notes
- Keep changelog entries concise and factual
- Use English only in log entries
- If no push happened, do not update the changelog
