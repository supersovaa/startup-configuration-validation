---
name: startup-configuration-validation
description: Validate and finalize application startup configuration from environment variables and other startup-provided inputs before dependent runtime work begins.
---

# Startup Configuration Validation

Use this skill when an application depends on configuration supplied at process startup and those settings should be validated before dependent runtime work begins.

This skill targets a single-user AI-agent development workflow.

## Responsibility

Establish one startup boundary that turns raw startup-provided configuration into validated application configuration.

Use environment variables, startup arguments, configuration files, secret providers, or equivalent startup inputs according to the repository's requirements.
Treat values available before dependent runtime work begins as startup configuration.

## Define the startup configuration set

Identify the complete set of startup-provided settings used by the application.

Represent that set through one configuration schema, constructor, loader, or equivalent entry point.
Keep the source and validation rule for each setting discoverable from that boundary.

Resolve defaults at this boundary when defaults are part of the application contract.

## Validate before dependent work begins

Load every declared startup setting during application startup.

Validate all constraints whose required inputs are available at startup, including:

- required presence;
- parsing and type conversion;
- allowed values;
- numeric or structural ranges;
- format constraints;
- relationships between settings;
- repository-defined startup configuration requirements.

Complete startup configuration validation before starting application work that depends on those settings, including network listeners, background workers, scheduled work, or equivalent runtime components.

## Produce validated configuration

Convert successfully validated values into one validated configuration representation.

Pass that validated representation inward as the application's source of startup configuration.
Application components consume the validated representation rather than independently re-reading startup configuration sources.

Use constrained internal representations when validation establishes a narrower domain than the raw input representation.

## Report configuration failures at startup

Evaluate the declared startup configuration set as one validation pass.

When the pass finds configuration failures, end startup with a configuration error.
Report every setting or startup-known constraint failure detected during that pass.
Identify the affected setting or relationship and the violated requirement directly.

Keep secrets and sensitive values out of diagnostic output while still identifying the affected setting.

## Boundaries

This skill owns validation and finalization of configuration whose required values are available during startup.

Runtime information that becomes available only after startup remains owned by the component or workflow that receives that information.

Implementation-time constants and choices belong in code or static data; use `prefer-static-decisions` when deciding whether a value should be runtime configuration at all.

Operational failure handling after valid configuration has been established belongs to the relevant runtime responsibility and repository defense policy.

## Review guidance

During implementation or review, confirm that:

- application-used startup settings are discoverable from one startup configuration boundary;
- startup-known validation is completed before dependent runtime work begins;
- application components receive validated configuration rather than raw startup inputs;
- configuration failures surface as startup configuration errors;
- one validation pass reports all configuration failures it can determine from the supplied startup inputs;
- diagnostics identify settings and violated constraints while protecting sensitive values;
- runtime-only information remains outside the startup configuration boundary.

Keep the implementation language-appropriate and minimal.
