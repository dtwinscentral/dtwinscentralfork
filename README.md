# Security Documentation

The secure-version baseline for this fork is documented here:

- [Deployment Security Checklist](docs/DEPLOYMENT_SECURITY_CHECKLIST.md)
- [Secure Runtime Setup](docs/SECURE_RUNTIME_SETUP.md)
- [Project Import Validation](docs/PROJECT_IMPORT_VALIDATION.md)
- [Symbol Library Security](docs/SYMBOL_LIBRARY_SECURITY.md)

## Quick summary

This fork should be treated as a safety-sensitive browser editor. The secure default is:

- deny remote code execution by default
- validate every project import
- sanitize every symbol library entry
- require explicit trust for advanced scripting or external assets

## Recommended deployment posture

- HTTPS only
- strict CSP
- no remote scripting by default
- no unsafe eval paths in production
- curated library model for public deployments
