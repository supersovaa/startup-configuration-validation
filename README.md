# startup-configuration-validation

A lightweight skill for validating and finalizing application configuration supplied at process startup before dependent runtime work begins.

This skill targets a single-user AI-agent development workflow.

## When to use

Use this skill when an application uses environment variables or other startup-provided configuration and configuration problems should surface during startup.

## Responsibility

Create one startup configuration boundary that:

- loads the complete application-used startup configuration set;
- resolves declared defaults;
- validates startup-known constraints;
- reports all configuration failures found in that validation pass;
- produces validated configuration for application components.

The executable rules are in [`SKILL.md`](SKILL.md).

## Adjacent responsibilities

- [prefer-static-decisions](https://github.com/supersovaa/prefer-static-decisions) decides whether a value should be runtime configuration or a static implementation choice.
- Repository runtime and defense rules own operational failures that occur after valid startup configuration has been established.

## Installation

Place this repository's `SKILL.md` at `<skills-root>/startup-configuration-validation/SKILL.md` in the target agent's skill directory, or install the repository through that skill system's repository installation mechanism.

## Files

- `SKILL.md` — installable skill definition.
- `README.md` — overview, activation guidance, responsibility, and installation.
- `LICENSE` — MIT License.
