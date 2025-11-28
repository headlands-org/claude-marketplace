# Apple Plugin

App Store Review Guidelines compliance checker for iOS/macOS applications. Analyzes your app against Apple's official guidelines and produces a detailed A-F grading report.

## Installation

```bash
/plugin install apple@headlands-claude-marketplace
```

## Usage

```bash
/apple review
```

## The Review Workflow

### Phase 1: Load Guidelines
Fetches the current Apple App Store Review Guidelines directly from Apple's developer documentation.

### Phase 2: Identify Your App
Scans your codebase to detect:
- Xcode project structure
- App capabilities and entitlements
- Third-party SDKs and dependencies
- Sensitive API usage (HealthKit, payments, etc.)
- Privacy-related implementations

### Phase 3: Confirm Target
Presents a summary of the detected app and asks for confirmation before proceeding.

### Phase 4: Parallel Analysis
Spawns multiple analysis tasks simultaneously to check:

| Task | Guideline Section | Focus Areas |
|------|-------------------|-------------|
| Safety | Section 1 | Content moderation, kids safety, data security |
| Performance | Section 2 | App completeness, metadata accuracy, compatibility |
| Business | Section 3 | IAP compliance, subscriptions, payments |
| Design | Section 4 | Originality, functionality, Apple services |
| Legal | Section 5 | Privacy, IP, gambling, VPN rules |
| Privacy Labels | App Store Connect | Privacy manifest, data collection |

### Phase 5: Grading Report
Compiles findings into a comprehensive report with:
- Overall grade (A-F)
- Per-section grades with risk levels
- Detailed findings for each guideline subsection
- Priority fix list organized by severity
- Human verification checklist

## Grading Scale

| Grade | Meaning | Submission Risk |
|-------|---------|-----------------|
| **A** | Fully compliant | Ready to submit |
| **B** | Minor issues | Low rejection risk |
| **C** | Moderate issues | Needs attention |
| **D** | Significant issues | High rejection risk |
| **F** | Critical violations | Will be rejected |

## What Gets Checked

### Section 1: Safety
- Objectionable content handling
- User-generated content moderation
- Kids category compliance (COPPA)
- Physical harm disclaimers
- Developer information
- Data security practices

### Section 2: Performance
- App completeness (no placeholders)
- Beta/debug code removal
- Metadata accuracy
- Hardware compatibility
- API deprecation issues

### Section 3: Business
- In-app purchase implementation
- Subscription handling and disclosure
- External payment compliance
- Advertising practices

### Section 4: Design
- Originality (no copycats)
- Minimum functionality
- Extension guidelines
- Sign in with Apple compliance
- Third-party SDK safety

### Section 5: Legal
- Privacy policy and data handling
- App Tracking Transparency
- HealthKit compliance
- Location services justification
- Intellectual property
- Gambling/contest rules

### Privacy Labels
- PrivacyInfo.xcprivacy manifest
- Required reason APIs
- Data collection categorization
- Tracking disclosure

## Example Output

```
# App Store Review Compliance Report
## MyApp - 2025-01-15

---

## Executive Summary

**Overall Grade: C**

App has solid core functionality but privacy implementation needs work.
Missing App Tracking Transparency prompt and incomplete privacy manifest.

**Submission Readiness:** Needs Work

---

## Section Grades

| Section | Grade | Risk Level | Key Issues |
|---------|-------|------------|------------|
| 1. Safety | B | Low | Minor content moderation gaps |
| 2. Performance | A | Low | None |
| 3. Business | A | Low | IAP properly implemented |
| 4. Design | B | Low | Consider Sign in with Apple |
| 5. Legal | D | High | ATT not implemented |
| Privacy Labels | C | Med | Incomplete manifest |
```

## When to Use

**Before App Store submission:**
- First-time submissions
- Major updates with new features
- After adding sensitive APIs
- Post-rejection to identify issues

**During development:**
- When adding payments/subscriptions
- When implementing user-generated content
- When integrating third-party SDKs
- When targeting kids category

## Tips

**Run early, run often:**
Don't wait until submission day. Run the review during development to catch issues early.

**Focus on F and D grades:**
These are rejection risks. Fix them first.

**Check the human verification list:**
Code analysis can't verify everything. Screenshots, descriptions, and legal agreements need manual review.

**Keep guidelines fresh:**
Apple updates guidelines regularly. The plugin fetches current guidelines each run.

## Limitations

- Code analysis only - can't verify runtime behavior
- Can't check App Store Connect metadata directly
- Some guidelines require human judgment
- Regional requirements vary
- Screenshots and descriptions need manual review

## Support

Issues: https://github.com/headlands-org/claude-marketplace/issues
Label: `plugin:apple`
