---
name: pr-reviewer
description: Critical code review of pull requests or current branch against base branch. Use when asked to review PRs, code changes, diffs, or branch comparisons. Provides thorough assessment of correctness, bugs, security, performance, database impact, scalability, and code quality.
---

# PR Review Skill

Review code changes with brutal honesty. Find bugs before production does. Check beyond the diff.

## Review Process

1. Understand the intent: What is this PR trying to accomplish?
2. Review the diff line by line
3. Trace impact to other parts of the codebase
4. Check for what's missing, not just what's present

## Review Categories

### 1. Logical Correctness
- Does the code do what it claims to do?
- Off-by-one errors, boundary conditions
- Null/undefined handling
- Boolean logic errors (inverted conditions, missing cases)
- Loop termination, state mutations, return value handling

### 2. Bug Detection
- Race conditions and timing issues
- Memory leaks (unclosed resources, event listeners)
- Exception paths that leave state inconsistent
- Input validation gaps
- Timezone handling

### 3. Database Impact
- N+1 query patterns
- Missing indexes for new query patterns
- Large table scans on production data
- Transaction scope - too broad or too narrow?
- Locking behavior - deadlock potential?
- Migration safety - reversible? data loss risk?
- Connection pool exhaustion potential

### 4. Security Concerns
- SQL injection, XSS, CSRF
- Authentication/authorization gaps
- Sensitive data exposure in logs/errors
- Secrets in code or config files
- Input sanitization gaps
- Mass assignment vulnerabilities

### 5. Scalability Issues
- O(n²) or worse algorithms on growing data
- Unbounded memory consumption
- Missing pagination
- Cache stampede potential
- Blocking operations in async contexts

### 6. Performance
- Unnecessary database calls
- Missing caching opportunities
- Redundant computations
- Synchronous operations that should be async

### 7. Error Handling
- Missing try/catch where needed
- Swallowed exceptions
- Generic error messages
- Missing retry logic for transient failures

### 8. Code Quality
- Naming clarity
- Function length and complexity
- Duplication that should be extracted
- Dead code, unused imports
- Hardcoded values that should be config

### 9. Testing
- Tests for happy path and edge cases?
- Error paths tested?
- Flaky test potential?

### 10. API & Contract Changes
- Breaking changes to public interfaces?
- Backwards compatibility?
- Documentation updated?

### 11. Concurrency
- Shared state modifications without locks
- Race conditions between read and write
- Cache invalidation timing

### 12. Observability
- Logging added? Log levels appropriate?
- Metrics for monitoring?
- Distributed tracing maintained?

### 13. Dependencies
- New dependency justified and pinned?
- License compatibility?
- Security vulnerabilities?

### 14. Deployment
- Feature flags for gradual rollout?
- Rollback plan?
- Migration timing relative to code deploy?

### 15. Broader Impact
- What other code calls the modified functions?
- Does this affect background jobs, cron tasks?
- Cache invalidation needed elsewhere?
- Event consumers affected?

## Output Format

**Summary:** 2-3 sentences on what the PR does and merge readiness.

**Critical Issues (Block Merge):** Bugs, security issues, data loss risks.

**Major Concerns:** Significant problems to address.

**Minor Issues:** Style, naming, small improvements.

**Database Impact:** Query analysis, migration concerns.

**Security Review:** Vulnerabilities or confirmation of security.

**Testing Gaps:** What tests are missing.

**Broader Impact:** Effects on other system parts.

**Questions for Author:** Clarifications needed.

**Verdict:** Ready to merge / Ready after minor fixes / Needs significant changes / Needs architectural discussion

## Tone

- Be direct: "This will cause N+1 queries" not "You might want to consider..."
- Be specific: Quote problematic code with line numbers
- Be constructive: Say what's wrong AND suggest a fix
- Prioritize: Critical issues first, nitpicks last
