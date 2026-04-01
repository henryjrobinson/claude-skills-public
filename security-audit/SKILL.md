---
name: security-audit
description: >
  Run a comprehensive security audit on any codebase. Scans for common
  vulnerabilities (OWASP Top 10), dependency issues, hardcoded secrets, auth
  bypass patterns, and AI-generated code risks. Produces a structured report
  with severity classifications and actionable remediation steps.
---

# Security Audit

Run a comprehensive security audit on the current codebase.

## Trigger
`/security-audit` or `/security-audit [focus-area]`

Focus areas: `auth`, `api`, `data`, `dependencies`, `infrastructure`, `full`

## Instructions

When this skill is invoked:

### 1. Discover Project Structure

Before scanning, understand what you're working with:

```bash
# Identify language/framework
ls package.json requirements.txt Gemfile go.mod Cargo.toml pyproject.toml 2>/dev/null

# Find source directories
find . -type d -name "src" -o -name "app" -o -name "lib" -o -name "server" -o -name "api" | head -10

# Find config files
find . -name ".env*" -o -name "*.config.*" -o -name "docker-compose*" | head -10
```

Adapt all subsequent scan commands to the project's language, framework, and directory structure.

### 2. Run Automated Scans

#### Dependency vulnerabilities
```bash
# Node.js
npm audit --audit-level=high 2>/dev/null

# Python
pip audit 2>/dev/null || safety check 2>/dev/null

# Go
govulncheck ./... 2>/dev/null

# Ruby
bundle audit check 2>/dev/null
```

#### Outdated packages
```bash
# Node.js
npm outdated --depth=0 2>/dev/null

# Python
pip list --outdated 2>/dev/null
```

### 3. Code Security Pattern Scan

Adapt grep patterns to the project's source directories. Replace `src/` below with the actual source paths found in Step 1.

```bash
# ============================================================================
# CRITICAL ISSUES
# ============================================================================

# Hardcoded secrets (CRITICAL)
grep -rn "sk-ant\|sk-proj\|sk_live\|sk_test\|AKIA[A-Z0-9]\|ghp_\|glpat-" src/
grep -rn "password\s*=\|api_key\s*=" src/ | grep -v ".env\|example\|test\|spec"

# SQL injection risk (CRITICAL)
grep -rn "\${.*}" src/ | grep -i "query\|select\|insert\|update\|delete"

# Auth bypass patterns (CRITICAL)
grep -rn "TEST_BYPASS\|skipAuth\|isAdmin.*true\|DISABLE_AUTH" src/

# Hardcoded env var fallbacks (CRITICAL)
# Fallbacks mask config errors in production — env vars should fail loudly
grep -rn "process.env\.[A-Z_]*\s*\|\|" src/ | grep -v "NODE_ENV\|LOG_LEVEL"
grep -rn "os.getenv.*," src/ | grep -v "None\|default.*test"  # Python

# Service account keys in repo (CRITICAL)
find . -name "*service-account*.json" -o -name "*credentials*.json" -o -name "*.pem" | grep -v node_modules

# ============================================================================
# HIGH SEVERITY ISSUES
# ============================================================================

# Dangerous functions (HIGH)
grep -rn "eval(\|exec(\|new Function(\|dangerouslySetInnerHTML\|__import__\|subprocess.call" src/

# Unparameterized queries (HIGH)
grep -rn "pool.query.*\`\|cursor.execute.*%" src/

# Frontend token storage in localStorage (HIGH)
# Should use HttpOnly cookies — localStorage is vulnerable to XSS
grep -rn "localStorage.setItem.*token\|sessionStorage.setItem.*token" src/

# HTTPS enforcement (HIGH)
grep -rn 'http://' src/ | grep -v "localhost\|127.0.0.1\|example.com\|test\|spec\|mock"

# CORS misconfiguration (HIGH)
grep -rn "cors()\|Access-Control-Allow-Origin.*\*" src/

# Rate limiting (HIGH) — check if it exists
grep -rn "rateLimit\|rate.limit\|throttle\|RateLimiter" src/

# ============================================================================
# MEDIUM SEVERITY ISSUES
# ============================================================================

# Debug/test code in production (MEDIUM)
grep -rn "console.log\|debugger\|binding.pry\|import pdb" src/ | head -20

# Error exposure — stack traces sent to users (MEDIUM)
grep -rn "res.status(500).*err\|traceback\|stack.*trace" src/ | grep -v "log\|logger"

# Incomplete security TODOs (MEDIUM)
grep -rn "TODO.*security\|FIXME.*validation\|TODO.*auth\|HACK.*" src/
```

### 4. Security Checklist

Check each area relevant to the project:

#### Authentication & Authorization
- [ ] All mutating endpoints require authentication
- [ ] JWT/session tokens validated on every request
- [ ] No test auth bypasses in production code
- [ ] User data isolated — queries filter by authenticated user
- [ ] Rate limiting on auth endpoints (prevent brute force)
- [ ] Password/token storage uses proper hashing (bcrypt, argon2)

#### Input Validation
- [ ] All POST/PUT endpoints validate input
- [ ] File uploads validated (type, size limits)
- [ ] JSON/request payload size limits configured
- [ ] No string concatenation in SQL queries (parameterized only)
- [ ] User input sanitized before any template rendering
- [ ] File type validation checks MIME type AND extension

#### API Security
- [ ] Rate limiting on all public endpoints
- [ ] CORS configured with specific origins (not wildcard)
- [ ] Request size limits set
- [ ] HTTPS enforced — no http:// in production
- [ ] API keys rotated regularly

#### Data Protection
- [ ] Sensitive data encrypted at rest
- [ ] No secrets in code (only in env vars / secret manager)
- [ ] Database connections use SSL
- [ ] Auth tokens in HttpOnly cookies (not localStorage)
- [ ] Service account keys never committed to git
- [ ] .env files in .gitignore

#### Error Handling
- [ ] No stack traces sent to users
- [ ] Errors logged server-side with context
- [ ] Sensitive data not included in logs
- [ ] Generic error messages in API responses

#### AI/LLM Integration (if applicable)
- [ ] User input sanitized before inclusion in prompts
- [ ] System prompts don't contain user-controlled content
- [ ] LLM API keys stored securely (not in frontend)
- [ ] Response validation for injection attempts
- [ ] Rate limiting on AI endpoints

#### Third-Party Integrations
For each integration (payment providers, auth providers, etc.):
- [ ] Webhook signatures verified
- [ ] API keys scoped to minimum required permissions
- [ ] SDK kept up to date
- [ ] Test/sandbox keys not in production

### 5. AI-Generated Code Review

With most developers using AI code generation, perform this specialized review:

```bash
# Find AI-generated code markers
grep -rn "// Generated by\|# Generated by\|// AI-generated\|// Claude\|// Copilot" src/

# Common AI code mistakes
grep -rn "eval(\|new Function(" src/
grep -rn "TODO.*security\|FIXME.*auth" src/
```

For each AI-generated section, verify:
1. **Input validation** — does it validate ALL inputs, or assume they're safe?
2. **Error handling** — does it handle failures, or crash silently?
3. **Auth checks** — does it verify permissions, or assume auth happened elsewhere?
4. **Hardcoded values** — are there fallback values that should fail loudly?
5. **Overly permissive** — wildcards or broad access checks?

### 6. Severity Classification

| Severity | Response Time | Examples |
|----------|---------------|----------|
| **CRITICAL** | Immediate | Auth bypass, SQL injection, exposed secrets, RCE |
| **HIGH** | 24 hours | IDOR, XSS, missing rate limits, token storage issues |
| **MEDIUM** | 1-2 weeks | Missing validation, info disclosure, debug code |
| **LOW** | Next release | Outdated deps (no known exploits), minor leaks |

### 7. Output Report

Generate a report in this format:

```markdown
# Security Audit Report — [Date]

## Executive Summary
- **Audit Type**: [Quick/Full]
- **Overall Rating**: [CRITICAL/HIGH/MEDIUM/LOW/PASS]
- **Project**: [name and framework]

## Automated Scan Results

### Dependency Audit
[Results or "No vulnerabilities found"]

## Code Review Findings

### CRITICAL Issues
| Issue | Location | Description |
|-------|----------|-------------|
| [Type] | `file:line` | [What and why it's dangerous] |

### HIGH Issues
| Issue | Location | Description |
|-------|----------|-------------|

### MEDIUM Issues
| Issue | Location | Description |
|-------|----------|-------------|

### LOW Issues
| Issue | Location | Description |
|-------|----------|-------------|

## Checklist Results

### Authentication & Authorization
- [x] All routes require auth middleware
- [ ] ISSUE: [description]
...

## Recommendations

### Immediate (Fix Now)
1. [Action item with specific file/line]

### Short-term (This Sprint)
1. [Action item]

### Long-term (Backlog)
1. [Action item]
```

### 8. Save Report

Save the report to: `docs/security/SECURITY_AUDIT_[DATE].md`

If the directory doesn't exist, create it.

## Quick Audit Mode

For `/security-audit quick`:
- Run dependency audit only
- Check for hardcoded secrets
- Check for hardcoded env var fallbacks
- Verify CORS configuration
- Check auth on mutating endpoints
- ~5 minutes instead of full audit

## Reference

Severity definitions:
- **CRITICAL**: Auth bypass, RCE, SQL injection, exposed credentials, hardcoded fallbacks
- **HIGH**: Authorization failures, XSS, CSRF, IDOR, prompt injection, localStorage tokens
- **MEDIUM**: Missing validation, info disclosure, weak crypto, unreviewed AI-generated code
- **LOW**: Outdated deps, minor leaks, documentation gaps

### 2026 Threat Landscape Context

- 50%+ of Node.js incidents from compromised dependencies
- 62% of AI-generated code contains known vulnerabilities
- 40% missing input sanitization (most common AI code flaw)
- Prompt injection attacks increased 300% in 2026
- 85% of developers now using AI code generation tools
