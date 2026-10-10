# ubi10-httpd Constitution

> **Version:** 1.1.0
> **Ratified:** 2026-03-10
> **Amended:** 2026-10-02
> **Status:** Active
> **Inherits:** [crunchtools/constitution](https://github.com/crunchtools/constitution) v1.22.0
> **Profile:** Container Image

This file holds what is specific to ubi10-httpd. The fleet rules and the Container
Image profile (license, versioning, LABELs, the RHSM secret-mount pattern,
systemd conventions, registry, testing and quality gates) apply at the
inherited version and are checked against this repo's files by
`constitution.yml`. They are not restated here.

## Purpose

Tier 1 of the layered UBI 10 image tree: Apache httpd on ubi10-core, the
foundation for every web-serving crunchtools image. Published as
`quay.io/crunchtools/ubi10-httpd`.

## Parent Image

`quay.io/crunchtools/ubi10-core:latest`. It inherits the troubleshooting
tools, rsyslog forwarding, masked services, `STOPSIGNAL` and `/sbin/init`
entrypoint. httpd is in the UBI repos; no RHSM registration.

## Packages and Services

- **Packages:** httpd.
- **Enabled:** httpd, with a `Restart=on-failure` drop-in
  (`config/httpd-restart.conf`).
- **Port:** 80 (`EXPOSE 80`).

## Smoke Test Coverage

`tests/smoke-test.sh` asserts httpd is active and serves content on port 80, and that the
inherited ubi10-core packages and masked services are still in place.

## Downstream Images

Build dispatches `parent-image-updated` to ubi10-httpd-php, ubi10-httpd-perl,
proxy and nagios.

## History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-03-10 | Initial constitution, tier 1 of the layered image tree |
| 1.0.1 | 2026-09-25 | Gatehouse review, triage and pre-commit gates |
| 1.1.0 | 2026-10-02 | Manifest under constitution v1.18.0: profile restatement removed, image specifics kept |
