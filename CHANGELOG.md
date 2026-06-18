# Changelog

All notable changes to this project are documented here. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Added
- `discover-oci-instances.sh` — enumerate RUNNING OCI compute instances in a
  compartment (or whole tenancy subtree) and generate Prometheus scrape targets,
  with per-OS exporter ports (Linux 9100 / Windows 9182). Outputs a human table,
  a `discovered-targets.json` (Prometheus `file_sd_config`), or a non-destructive
  merge into `config.json` `TargetNodes`.
- `docs/KNOWLEDGE_BASE.md` — searchable troubleshooting KB (23 entries) derived
  from the end-to-end validation.
- Public-repo scaffolding: `LICENSE` (UPL-1.0), `CONTRIBUTING.md`, `SECURITY.md`,
  `CODE_OF_CONDUCT.md`, GitHub issue/PR templates, and a `lint.yml` CI workflow
  (shellcheck + PSScriptAnalyzer + `docker compose config`).

### Changed
- **OCI Monitoring is now optional.** New `OciMonitoringEnabled` config flag. The
  proxy can run as a pure OpenTelemetry / `remote_write` exporter to a non-OCI
  backend; the Management Agent zip/response-file prompts and install only happen
  when OCI Monitoring is enabled. The final summary reflects the active export
  paths, and the script warns if no export path is enabled.
- `otel-destination/docker-compose.yml` — Grafana admin password is now
  env-overridable (`GF_SECURITY_ADMIN_PASSWORD`).
- Hardened `.gitignore` (secrets, `.env*`, `*.pem`, `*.key`, `*.rsp`,
  `discovered-targets.json`).
- Removed a developer-specific local path from `PROJECT_REVIEW.md`.

## [0.1.0] — 2026-06-17

### Added
- Initial validated suite: Windows/Linux exporter installers, Windows Prometheus
  proxy, OCI Management Agent integration, optional GCP `stackdriver_exporter`,
  OpenTelemetry export path, `manage-oci-datasource.sh` lifecycle helper, and the
  `otel-destination/` test sink.
- `PROJECT_REVIEW.md` — end-to-end test report on real OCI infrastructure with 13
  documented bug fixes.
