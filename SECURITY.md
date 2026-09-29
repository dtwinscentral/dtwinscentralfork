# Security Hardening Guide

This fork is intended to be a safer default for browser-based animation and scripting workflows. The goal is to reduce attack surface while keeping the editor usable.

## Security objectives

- Disable unsafe script execution paths by default
- Use Content Security Policy (CSP) headers for embedded use
- Sanitize imported assets and project payloads
- Validate all user-supplied data before execution
- Avoid remote code loading unless explicitly enabled
- Keep project files portable and deterministic

## Recommended hardening baseline

### 1. Browser runtime protections

- Use a strict CSP in deployed builds:
  - `default-src 'self'`
  - `script-src 'self' 'unsafe-eval'` only if absolutely required by the editor runtime
  - `connect-src 'self' https://api.github.com https://editor.wickeditor.com`
  - `img-src 'self' data: blob: https:`
  - `style-src 'self' 'unsafe-inline'`
  - `font-src 'self' data:`

- Remove or gate remote script injection features.
- Disallow untrusted project imports by default unless user explicitly opts in.
- Restrict file uploads to expected media types and size limits.

### 2. Project and asset validation

- Validate JSON project payloads against a schema
- Reject malformed project files before load
- Strip unexpected fields from imported project metadata
- Limit symbol and asset size before insertion
- Scan uploaded media for dangerous file types or oversized payloads

### 3. Script execution safety

- Prefer a sandboxed execution environment for user scripts
- Disallow `eval`, `Function`, `setTimeout(String)`, and `setInterval(String)` in restricted environments
- Validate script access based on project trust level
- Keep code execution behind explicit user consent in shared/public deployments

### 4. Network hardening

- Do not fetch remote scripts or media by default
- Require user approval for external asset loading
- Use HTTPS-only endpoints
- Keep API calls pinned to known hosts

### 5. Storage and persistence

- Store project data in browser-managed storage only when necessary
- Prevent automatic loading of untrusted saved projects
- Encrypt sensitive local data where supported
- Use secure cookie/credential policies if auth is added later

## Security checklist for this fork

- [ ] CSP implemented for production builds
- [ ] Strict asset validation enabled
- [ ] Unsafe code execution disabled in default mode
- [ ] External script loading blocked by default
- [ ] Project import validation enabled
- [ ] File upload limits enforced
- [ ] Sanitized symbol library import pipeline
- [ ] Audit logs for admin/review workflows

## Production recommendation

For a secure public deployment, this fork should run in a restricted, trusted environment with:

- no arbitrary remote code execution
- no automatic import of untrusted projects
- limited file system access
- explicit user authorization for networked assets

## Security notes

This fork is a developer-oriented tool. Any interactive scripting environment is inherently sensitive. The safest configuration is to run scripts in a restricted environment or require a trust flag from the user before enabling advanced script features.
