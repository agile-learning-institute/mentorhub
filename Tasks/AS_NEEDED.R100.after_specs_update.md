# R100 – Update files after architecture.yaml changes

**Status**: Shipped  
**Task Type**: Updates
**Run Mode**: Run as needed

## Goal

Update the Developer Edition docker-compose.yaml, and the welcome page index.html with changes after the architecture.yaml file has been updated with new services.

## Context / Input files

These files must be treated as **inputs** and read before implementation:

- `Specifications/architecture.yaml`

**Target files** (to be updated):

- `DeveloperEdition/docker-compose.yaml`
- `index.html` (welcome page)

## Requirements

Update `DeveloperEdition/docker-compose.yaml` and the welcome page `index.html` to match the services defined in `Specifications/architecture.yaml`.

### docker-compose.yaml

- Add or update service definitions for each domain in the architecture (runbook, schema/mongodb, profile, mentor, member, etc.).
- **For each microservice domain, define two profiles:**
  - `{domain}-api` – API service only (e.g. `profile-api` → profile_api)
  - `{domain}` – API + SPA (e.g. `profile` → profile_api + profile_spa)
- Ensure backing services (e.g. mongodb) are included in the profiles of any service that depends on them.

### index.html

- Add links for each service SPA (with correct ports from the architecture).
- Add an API Explorer link for each backing API (e.g. `/docs/index.html` or `/docs/explorer.html` as appropriate for each service type).

## Testing expectations

- **None**

## Packaging / build checks

Before marking this task as completed:
- Run ``make container`` and ensure that the container builds cleanly.

## Dependencies / Ordering

- Should run **after**:
  - **None**
- Should run **before**:
  - **None**

## Implementation notes (to be updated by the agent)

**Summary of changes**
- **docker-compose.yaml**: Renamed sample_api/sample_spa → profile_api/profile_spa; added mentor_api, mentor_spa, member_api, member_spa; updated profiles (runbook-api, runbook, schema-api, schema, profile-api, profile, mentor-api, mentor, member-api, member); updated welcome service profiles; aligned mongodb/mongodb_api/mongodb_spa profiles with schema domain naming.
- **index.html**: Replaced placeholder with links for Runbook, Schema Configuration, Profile, Mentor, Member (SPA + API Explorer for each); reordered links; updated script to set hrefs for all services.

**Testing results**
- Packaging/build: `make container` completed successfully; image `ghcr.io/agile-learning-institute/mentorhub:latest` built.

**Follow‑up tasks**
- Publish updated container image when ready.
- Ensure profile, mentor, member API/SPA images exist at ghcr.io (mentorhub_profile_api, mentorhub_profile_spa, mentorhub_mentor_api, mentorhub_mentor_spa, mentorhub_member_api, mentorhub_member_spa).

