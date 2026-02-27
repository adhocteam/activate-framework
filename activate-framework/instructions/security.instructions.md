---
description: 'Security guardrails for all code changes'
applyTo: '**'
excludeAgent: []
---
# Security Instructions

Security-first guidance that applies to all code contributions. These guardrails help prevent common vulnerabilities and protect sensitive data.

## When To Use

- Writing or reviewing any code that handles user input
- Working with authentication, authorization, or session management
- Handling secrets, API keys, or credentials
- Processing data from external sources
- Modifying infrastructure or deployment configurations

## Guidance

### Secrets and Credentials

- Never commit secrets, API keys, passwords, or tokens to version control
- Use environment variables or secret management systems for sensitive values
- Add patterns to `.gitignore` to prevent accidental commits (e.g., `.env`, `*.pem`)
- Rotate any credentials that may have been exposed in commit history
- Use placeholder values in documentation and examples (e.g., `YOUR_API_KEY_HERE`)

### Input Validation

- Validate and sanitize all user input before processing
- Use allowlists over denylists when validating input formats
- Never trust client-side validation alone; always validate server-side
- Parameterize database queries to prevent SQL injection
- Escape output appropriately for the context (HTML, URL, JavaScript)

### Authentication and Authorization

- Use established authentication libraries rather than rolling your own
- Implement proper session management with secure, HTTP-only cookies
- Apply the principle of least privilege for all access controls
- Verify authorization on every request, not just at login
- Use strong, unique tokens for password reset and email verification flows

### Command Execution

- Avoid shell commands when language-native alternatives exist
- Never pass unsanitized user input to shell commands
- Use parameterized command execution (e.g., subprocess with arrays, not strings)
- Validate file paths to prevent directory traversal attacks
- Log command execution for audit purposes

### Dependency Management

- Keep dependencies updated to patch known vulnerabilities
- Review new dependencies before adding them (check maintenance status, security history)
- Use lock files to ensure reproducible builds
- Run dependency audits regularly (`npm audit`, `pip-audit`, etc.)
- Prefer well-maintained packages with active security response processes

### Data Protection

- Encrypt sensitive data at rest and in transit
- Use HTTPS for all external communications
- Minimize data collection to what's strictly necessary
- Implement proper data retention and deletion policies
- Mask or redact sensitive data in logs and error messages

### Error Handling

- Never expose stack traces or internal errors to end users
- Log detailed errors server-side for debugging
- Return generic error messages to clients
- Handle authentication failures without revealing whether the user exists
- Fail securely—deny access when in doubt

### GitHub Actions Permissions

- Default to least privilege: set workflow-level `permissions` to the minimum required (e.g., `contents: read`).
- Grant job-specific `permissions` only where needed; avoid blanket write scopes.
- Do not grant write access to `GITHUB_TOKEN` for builds triggered from forked PRs.
- Use `actions/checkout@v4` with `persist-credentials: false` when write is not needed.
- Prefer OIDC for cloud provider credentials; avoid long-lived secrets in workflows.
- Avoid `pull_request_target` for running untrusted code; use `pull_request` and restrict dangerous steps.
- Limit `workflow_call` and `workflow_dispatch` to trusted callers; review inherited secrets usage.

## Federal Compliance

### Regulatory Frameworks

- Align security controls with NIST 800-53 and agency-specific overlays
- Follow FedRAMP requirements for cloud services; verify provider authorization status
- Maintain documentation for Authority to Operate (ATO) boundary considerations
- Reference FISMA requirements for continuous monitoring and risk management

### Encryption Standards

- Use FIPS 140-2/3 validated cryptographic modules for sensitive operations
- Enforce TLS 1.2 minimum (prefer 1.3) for all communications
- Use AES-256 for data at rest; disable weak ciphers (SSLv3, TLS 1.0/1.1, RC4, 3DES)
- Verify key management practices meet NIST 800-57 guidelines

### Audit Logging

- Generate immutable, tamper-evident audit logs for all security-relevant events
- Retain logs per agency policy (typically 1-3 years per NIST guidelines)
- Include actor, action, timestamp, source IP, resource, and success/failure status
- Forward logs to centralized SIEM for correlation and alerting

### Zero Trust Principles

- Verify explicitly on every request; do not trust based on network location alone
- Assume breach; limit blast radius with microsegmentation and least privilege
- Continuously verify user and device posture before granting access
- Encrypt all traffic, including east-west within the network

### Supply Chain Security (EO 14028)

- Generate and publish SBOM (Software Bill of Materials) for all releases
- Attest to secure development practices with SLSA provenance where feasible
- Verify third-party software integrity and signatures before deployment
- Track and remediate vulnerabilities in transitive dependencies

### CUI and Sensitive Data Handling

- Mark and handle Controlled Unclassified Information (CUI) per NIST 800-171
- Encrypt CUI in transit and at rest; restrict access to authorized personnel
- Apply data loss prevention controls to prevent unauthorized exfiltration
- Follow agency-specific handling procedures for PII and PHI

### Incident Response

- Report security incidents to CISA within required timelines (72 hours for significant incidents)
- Maintain incident response runbooks with current escalation contacts
- Preserve evidence for forensic analysis; document containment and remediation steps
- Conduct post-incident reviews and update controls based on lessons learned

### Data Residency and Sovereignty

- Keep data within FedRAMP-authorized boundaries and approved regions
- Verify cloud services meet federal data sovereignty requirements
- Prohibit processing or storage in unauthorized geographic locations
- Document data flows across system boundaries for ATO packages

## Validation Checklist

- [ ] No secrets or credentials in code or version control
- [ ] All user input is validated and sanitized
- [ ] Database queries are parameterized
- [ ] Shell commands avoid string interpolation with user input
- [ ] Dependencies are up-to-date and audited
- [ ] Sensitive data is encrypted and properly handled in logs
- [ ] Error messages don't leak implementation details
- [ ] GitHub Actions workflows declare minimal `permissions`; OIDC used for cloud credentials
- [ ] Encryption uses FIPS 140-2/3 validated modules; TLS 1.2+ enforced
- [ ] Audit logs are immutable, complete, and forwarded to SIEM
- [ ] SBOM generated for releases; third-party integrity verified
- [ ] CUI and PII handled per NIST 800-171 and agency policy
- [ ] Incident response runbooks current; CISA reporting timelines understood
