# Issuify

Review all changed files since upstream branch. Include work we're aware of. Ask about unexpected changes.

Use the **GitHub Copilot MCP server** tools to create both the issue and PR:
- `mcp__github__create_issue` - Create the GitHub issue
- `mcp__github__create_pull_request` - Create the pull request

## Issue (what & why)
Write casual, precise language. No fluff. Focus on bottom line.

- **Problem**: What's broken or missing (1-2 sentences max)
- **Value**: Why it matters (1 sentence)
- **Solution**: What we're doing (2-3 bullets, not exhaustive)

Target 3-5 sentences total. Skip obvious details.

## PR (how)
Write casual, precise language. No frilly technical jargon.

- **Summary**: What changed (2-3 bullets max, technical but simple)
- **Why**: How it solves the issue (1 sentence linking back)
- **Test**: What to check (2-3 bullets, just key things)

Target 4-6 sentences total. Cut anything that doesn't add value.

## Style
- Casual but exact (like talking to a teammate)
- No fake technical voice, no marketing speak
- Skip words like "comprehensive", "robust", "ensure", "carefully"
- Bottom line first, skip exhaustive details
