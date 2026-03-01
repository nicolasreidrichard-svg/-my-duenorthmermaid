# Security Policy

## Supported Versions

This repository is a documentation showcase for [Mermaid](https://mermaid.js.org/) diagram types.
It contains no executable application code or dependencies of its own.

## Reporting a Vulnerability

If you discover a security issue in the **code examples** contained in this repository
(e.g., an unsafe practice demonstrated in a snippet), please open a
[GitHub Issue](https://github.com/nicolasreidrichard-svg/-my-duenorthmermaid/issues) or submit a pull request with the fix.

## Best Practices for Code Examples

The code examples in this repository follow these security guidelines:

- **Pin dependency versions** – CDN and npm imports are pinned to specific versions
  (e.g., `mermaid@11.4.1`) to prevent supply-chain attacks from unintended upgrades.
- **Use `npx` over global installs** – `npx @mermaid-js/mermaid-cli` is recommended
  over `npm install -g` to isolate tool execution and reduce attack surface.
- **No secrets or credentials** – No tokens, keys, or passwords are stored anywhere
  in this repository.

## Upstream Security

For vulnerabilities in Mermaid itself, please report them to the upstream project:
[https://github.com/mermaid-js/mermaid/security](https://github.com/mermaid-js/mermaid/security)
