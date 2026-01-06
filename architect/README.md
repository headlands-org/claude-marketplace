# Architect Plugin

AI Architect & System Orchestrator for managing complex engineering projects with parallel execution, quality gates, and independent code review validation.

## Installation

```bash
/plugin install architect@headlands-plugin-marketplace
```

## Usage

```bash
/architect <your complex engineering goal>
```

## The 7-Phase Workflow

### Phase 1: Deconstruct the Goal
The architect breaks down your high-level request into core engineering objectives and restates the mission for confirmation.

### Phase 2: Parallel Research & Discovery
- Formulates specific research questions about your codebase
- Executes research in parallel using the Task tool
- Synthesizes findings into a Knowledge Brief

**Example research questions:**
- "What is the current data schema for Users?"
- "Which files handle API authentication?"
- "What are the existing testing patterns?"

### Phase 3: Strategic Execution Plan
Creates a `PLAN.md` file with:
- Sequential **Steps**
- Parallel **Tasks** within each step
- For each task:
  - **Goal**: Single clear outcome
  - **Success Criteria**: Verifiable conditions
  - **Sandbox**: Allowed files/directories
  - **Do Not Touch**: Forbidden areas

### Phase 4: Approval & Revisions
- Analyzes highest-risk areas
- Summarizes key architectural decisions (API, database, UX changes)
- Waits for human approval
- Iterates on plan as needed

### Phase 5: Delegate & Supervise
- Executes plan step-by-step
- Launches tasks in parallel within each step
- **Quality Gate Loop** (critical):
  - Switches to powerful model for review
  - Checks output against Success Criteria
  - Runs tests
  - Approves or creates fix-it tasks
  - Never proceeds until all tasks pass

### Phase 6: Independent Validation *(New)*
After implementation completes, spawns an **independent code reviewer** with fresh context:

1. **Discover Guidelines**: Searches for project-specific review criteria (`code-review-guidelines.md`, `AGENTS.md`, `CONTRIBUTING.md`, etc.)
2. **Generate Change Summary**: Creates neutral diff without explaining intent
3. **Spawn Reviewer**: Launches a fresh task that receives ONLY:
   - The code diff (no context about goals)
   - Generic review criteria (security, reliability, quality)
   - Any discovered project-specific guidelines
4. **Triage Issues**: Categorizes by severity (P0-P3)
5. **Fix & Repeat**: Addresses P0/P1 issues, repeats until clean

**Why this matters:**
- Eliminates confirmation bias (reviewer doesn't know intended behavior)
- Catches issues the implementation-aware architect might rationalize
- Respects project-specific conventions automatically
- Maximum 3 cycles before escalating unresolved issues

### Phase 7: Final Integration & Report
- Performs final integration test
- Runs project linters/tests
- Deletes PLAN.md
- Provides comprehensive report including:
  - Work completed
  - Issues found and fixed during validation
  - Any documented exceptions
  - Final codebase state

## When to Use

**Ideal for:**
- Large refactoring projects spanning multiple files
- Multi-component features requiring coordination
- Complex migrations (database, API, framework)
- Projects needing explicit quality checkpoints
- Work requiring clear scope boundaries
- Codebases with review guidelines you want enforced

**Not ideal for:**
- Single-file changes
- Trivial updates
- Exploratory coding
- Quick prototypes

## Example Scenarios

### Database Migration
```bash
/architect migrate user authentication from sessions to JWT tokens
```

The architect will:
1. Research current session implementation
2. Plan migration steps (schema, API, client)
3. Get your approval on the approach
4. Execute with quality gates at each phase
5. Run independent validation to catch security issues
6. Verify integration tests pass

### Multi-Service Refactoring
```bash
/architect extract payment processing into a separate microservice
```

The architect will:
1. Identify all payment-related code
2. Plan service boundaries and APIs
3. Review with you before changes
4. Implement with parallel tasks
5. Validate changes independently for security/reliability
6. Test end-to-end integration

## Tips

**Be specific about constraints:**
```bash
/architect add real-time notifications, but don't change the database schema
```

**Provide context:**
```bash
/architect implement caching for the API, we're using Redis already
```

**Set explicit goals:**
```bash
/architect reduce API response time by 50% through query optimization
```

## What Gets Created

During execution you'll see:
- **PLAN.md** - The complete execution plan (deleted after completion)
- **Task outputs** - Results from parallel research and implementation
- **Quality reports** - Reviews of each completed task
- **Validation reports** - Independent review findings and fixes
- **Final report** - Summary of all work done

## How Review Guidelines Are Discovered

The validation phase automatically searches for these files (in priority order):
- `**/code-review-guidelines.md`
- `**/code-review*.md`
- `**/review-guidelines*.md`
- `**/AGENTS.md`
- `**/CLAUDE.md`
- `**/CONTRIBUTING.md`
- `**/CODE_STYLE.md`
- `**/.github/PULL_REQUEST_TEMPLATE*`

If found, these are provided to the reviewer alongside generic criteria.

## Configuration

No configuration needed. The architect uses:
- Task tool for parallel execution
- Model switching (Haiku for research, Opus for review/validation)
- Your existing development tools and test infrastructure
- Auto-discovered review guidelines

## Limitations

- Requires Task tool access
- Works best with existing test suites
- Needs clear success criteria for quality gates
- Human approval adds time (but prevents mistakes)
- Validation limited to 3 cycles before escalation

## Support

Issues: https://github.com/headlands-org/plugin-marketplace/issues
Label: `plugin:architect`
