# Issuify

Review all changed files since upstream branch. Include work we're aware of. Ask about unexpected changes.

## Step 1: Confirm GitHub access

Call `mcp__github__get_me` before anything else. This:
1. Tests that authentication works
2. Shows who you're authenticated as (ground truth for the user)
3. If it fails, authentication isn't configured - see "In case of failure" below

## Step 2: Understand the changes

Review the diff and summarize what this work accomplishes. Identify key terms/concepts.

## Step 3: Search for existing issues

Use `mcp__github__search_issues` to find open issues that might relate to this work:
- Search using key terms from the changes (component names, feature areas, bug descriptions)
- Filter to open issues in this repo
- Look for issues that this PR would fully or partially address

**If related issues found:**
- Show the user which issues look relevant (title + number)
- Ask: "Should this PR close any of these issues?"
- If yes → skip to Step 5, PR will reference "Closes #X, #Y"
- If no → proceed to Step 4

**If no related issues found:**
- Proceed to Step 4

## Step 4: Create an issue (if needed)

Use `mcp__github__issue_write` with method "create"

Write casual, precise language. No fluff. Focus on bottom line.

- **Problem**: What's broken or missing (1-2 sentences max)
- **Value**: Why it matters (1 sentence)
- **Solution**: What we're doing (2-3 bullets, not exhaustive)

Target 3-5 sentences total. Skip obvious details.

## Step 5: Create the PR

Use `mcp__github__create_pull_request`

**Important:** Include "Closes #X" (or "Closes #X, #Y" for multiple) in the PR body to auto-link issues.

Write casual, precise language. No frilly technical jargon.

- **Summary**: What changed (2-3 bullets max, technical but simple)
- **Why**: How it solves the issue (1 sentence linking back)
- **Test**: What to check (2-3 bullets, just key things)
- **Closes**: #issue_number (or multiple)

Target 4-6 sentences total. Cut anything that doesn't add value.

## Style
- Casual but exact (like talking to a teammate)
- No fake technical voice, no marketing speak
- Skip words like "comprehensive", "robust", "ensure", "carefully"
- Bottom line first, skip exhaustive details

## In case of failure

If `mcp__github__get_me` fails, report:

```
GitHub authentication failed.

The issuify plugin requires a GitHub PAT configured in the GitHub MCP server.

Setup instructions:

1. Create a GitHub PAT at https://github.com/settings/tokens
   Required scope: repo

2. Configure the GitHub MCP server with your token
   (see your Claude Code MCP settings)

3. Restart Claude Code after configuring

Then run /issuify again.
```

Do NOT try to check environment variables via bash - the sandbox doesn't inherit shell env vars.
