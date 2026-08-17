<!--
  AGENT INSTRUCTIONS
  ==================
  This document is machine-maintained. Follow these rules on every update:

  1. PLACEHOLDERS: All fields use {{FIELD_NAME}} tokens. Replace the token
     with the actual value. Never leave a {{...}} token in a published page.

  2. REPEATABLE BLOCKS: Sections marked with:
       <!-- REPEAT-BLOCK: <name> -->  ...  <!-- /REPEAT-BLOCK: <name> -->
     represent one entry in a list. To add an entry, copy the block and
     append it. To remove, delete the whole block. Never renumber headings —
     use the block label only.

  3. SYNC REQUIREMENT: Any change to section 2.3 (Components) MUST also
     update 2.1 (System Architecture diagram + External integrations table)
     and vice versa. These three artefacts must always be consistent.

  4. OPTIONAL SECTIONS: Sections marked <!-- OPTIONAL: omit if not applicable -->
     should be removed entirely when not relevant. Do not leave them blank.

  5. AGENT AUDIT: Update the metadata block below on every write.

  6. PROSE FIELDS: Fields marked {{PROSE: <instruction>}} expect a short
     paragraph. Write concisely; do not copy placeholder text verbatim.
-->

# {{APP_NAME}}

> **Page owner:** {{OWNER_NAME}} | **Last reviewed:** {{LAST_REVIEWED_DATE: YYYY-MM-DD}} | **Status:** {{STATUS: Active | Deprecated | Beta}} | **Last updated by agent:** {{AGENT_LAST_UPDATED: YYYY-MM-DD}}

---

## 1. Description

{{PROSE: 1–3 sentences. What the application does, its primary purpose, and who it serves.}}

| Field | Value |
|-------|-------|
| Type | {{TYPE: Service \| Library \| CLI \| Web App \| Worker}} |
| Domain | {{DOMAIN: Corporate Finance \| Equities \| Research \| FICC \| Equities Risk Trading}} |
| Language(s) | {{LANGUAGES: e.g. Python 3.11, TypeScript}} |

---

## 2. Architecture

### 2.1 System Architecture

{{PROSE: How this application fits into the broader system. Cover what provisions it (e.g. Terraform), what platform services it uses (e.g. Azure Service Bus, Key Vault), and upstream/downstream application relationships.}}

```
{{ARCHITECTURE_DIAGRAM: Replace this entire block with an ASCII diagram showing
infrastructure, platform services, and application relationships. Example shape:

[Terraform (IaC)]
      │ provisions
      ▼
[Azure App Service] ──── [Azure Key Vault]
                                │ secrets
                                ▼
                         [{{APP_NAME}}]
                                │
              ┌─────────────────┴──────────────────┐
              ▼                                     ▼
   [Azure Service Bus]                    [Azure SQL / Cosmos DB]
        ▲
        │
[Upstream App]
}}
```

**External integrations:**

<!-- AGENT: Keep this table in sync with section 2.3 components. One row per external system. -->

| System | Type | Direction | Purpose |
|--------|------|-----------|---------|
| {{SYSTEM_NAME}} | {{SYSTEM_TYPE: Platform service \| Messaging \| Internal service \| Database \| Third-party}} | {{DIRECTION: Inbound \| Outbound \| In/Out}} | {{SYSTEM_PURPOSE}} |

---

### 2.2 Internal Architecture

{{PROSE: How the application is structured internally. Layers, modules, workers, schedulers. What a developer needs to understand to navigate the codebase.}}

| Component | Description |
|-----------|-------------|
| {{INTERNAL_COMPONENT_NAME}} | {{INTERNAL_COMPONENT_DESCRIPTION}} |

---

### 2.3 Components

<!-- AGENT: Every component block here must have a matching row in the
     External integrations table (2.1) and appear in the architecture diagram.
     Add blocks by copying a REPEAT-BLOCK. Delete blocks entirely when removing
     a component. Do not renumber — use the component label as the identifier. -->

<!-- REPEAT-BLOCK: component -->
#### Component: {{COMPONENT_LABEL}}

| Field | Value |
|-------|-------|
| Description | {{COMPONENT_DESCRIPTION}} |
| Source (GitHub) | [{{GITHUB_REPO}}]({{GITHUB_URL}}) |
| Monorepo path | {{MONOREPO_PATH: path/to/module or N/A}} |

| Environment | URL | Notes |
|-------------|-----|-------|
| Production | [{{PROD_URL}}]({{PROD_URL}}) | |
| {{ENV_NAME: Staging \| Dev \| Test \| Sandbox}} | [{{ENV_URL}}]({{ENV_URL}}) | {{ENV_NOTES: omit row if not applicable}} |

<!-- /REPEAT-BLOCK: component -->

<!-- REPEAT-BLOCK: infrastructure -->
#### Component: {{INFRA_LABEL}}

| Field | Value |
|-------|-------|
| Description | {{INFRA_DESCRIPTION}} |
| Source (GitHub) | [{{GITHUB_REPO}}]({{GITHUB_URL}}) |
| Monorepo path | {{MONOREPO_PATH: path/to/module or N/A}} |

| Resource | Deployed Link | Notes |
|----------|---------------|-------|
| {{RESOURCE_NAME}} | [{{DEPLOYED_SYSTEM_NAME}}]({{DEPLOYED_SYSTEM_URL}}) | {{RESOURCE_NOTES}} |

<!-- /REPEAT-BLOCK: infrastructure -->

<!-- REPEAT-BLOCK: external-service -->
#### Component: {{EXTERNAL_LABEL}}

| Field | Value |
|-------|-------|
| Description | {{EXTERNAL_DESCRIPTION}} |
| Source (GitHub) | N/A — external service |

| Resource | Link | Notes |
|----------|------|-------|
| {{RESOURCE_NAME}} | [{{RESOURCE_LINK_LABEL}}]({{RESOURCE_URL}}) | {{RESOURCE_NOTES}} |

<!-- /REPEAT-BLOCK: external-service -->

---

## 3. Getting Started

### Prerequisites

<!-- REPEAT-BLOCK: prerequisite -->
- {{PREREQUISITE: Tool, runtime, CLI, or access requirement with minimum version if applicable}}
<!-- /REPEAT-BLOCK: prerequisite -->

### Setup

```bash
# Clone
git clone {{GITHUB_URL}}

# Install dependencies
{{INSTALL_COMMAND}}

# Configure environment
{{ENV_SETUP_COMMAND: e.g. cp .env.example .env}}

# Run locally
{{RUN_COMMAND}}
```

> Full setup detail: `README.md` in {{GITHUB_REPO}}

---

## 4. Configuration & Access

### 4.1 Configuration

| Variable | Required | Description | Default |
|----------|----------|-------------|---------|
| {{ENV_VAR_NAME}} | {{REQUIRED: Yes \| No}} | {{ENV_VAR_DESCRIPTION}} | {{ENV_VAR_DEFAULT: value or none}} |

**Secrets managed via:** {{SECRETS_MANAGER: e.g. Azure Key Vault, AWS Secrets Manager, SSM Parameter Store}}

---

### 4.2 Access Management

| Resource | How to request | Approver |
|----------|----------------|----------|
| Repo access | {{REPO_ACCESS_PROCESS}} | {{REPO_ACCESS_APPROVER}} |
| Production environment | {{PROD_ACCESS_PROCESS}} | {{PROD_ACCESS_APPROVER}} |
| {{ENV_NAME: Staging \| Dev \| Test}} environment | {{ENV_ACCESS_PROCESS}} | {{ENV_ACCESS_APPROVER}} |
| Secrets / credentials | {{SECRETS_ACCESS_PROCESS}} | {{SECRETS_ACCESS_APPROVER}} |

---

## 5. CI/CD Pipeline

| Stage | Tool | Trigger | Notes |
|-------|------|---------|-------|
| Build | {{BUILD_TOOL}} | {{BUILD_TRIGGER}} | {{BUILD_NOTES}} |
| Deploy to production | {{DEPLOY_TOOL}} | {{DEPLOY_TRIGGER}} | {{DEPLOY_NOTES}} |
| {{STAGE_NAME: Deploy to Staging \| Deploy to Dev}} | {{STAGE_TOOL}} | {{STAGE_TRIGGER}} | {{STAGE_NOTES}} |

**Pipeline config:** `{{PIPELINE_CONFIG_PATH: e.g. .github/workflows/deploy.yml}}`

---

## 6. API Reference

<!-- OPTIONAL: omit this entire section if the application has no API -->

| Field | Value |
|-------|-------|
| API Docs | [Swagger / OpenAPI]({{API_DOCS_URL}}) |
| Base URL | `{{API_BASE_URL}}` |
| Authentication | {{API_AUTH: e.g. Bearer JWT, API key, mTLS}} |

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/health` | Health check |
| {{HTTP_METHOD}} | {{API_PATH}} | {{API_ENDPOINT_DESCRIPTION}} |

---

## 7. Runbook

| Field | Value |
|-------|-------|
| Runbook | [{{APP_NAME}} Runbook]({{RUNBOOK_URL}}) |
| Alerts | [{{MONITORING_TOOL}} Dashboard]({{ALERTS_URL}}) |
| Logs | [{{LOG_TOOL}}]({{LOGS_URL}}) |
| On-call | [{{ONCALL_TOOL}}]({{ONCALL_URL}}) |

| Task | Command / Steps |
|------|-----------------|
| Restart service | `{{RESTART_COMMAND}}` |
| Force re-deploy | `{{REDEPLOY_COMMAND}}` |
| Run DB migrations | `{{MIGRATION_COMMAND}}` |

---

## 8. Ownership & Contacts

| Role | Name / Team | Contact |
|------|-------------|---------|
| Tech Lead | {{TECH_LEAD_NAME}} | {{TECH_LEAD_CONTACT: Teams handle or email}} |
| Engineering Team | {{ENGINEERING_TEAM_NAME}} | {{ENGINEERING_TEAM_CONTACT: Teams channel}} |
| Product Owner | {{PRODUCT_OWNER_NAME}} | {{PRODUCT_OWNER_CONTACT: Teams handle or email}} |

**Teams channel:** `{{TEAMS_CHANNEL}}`
**Incident channel:** `{{INCIDENT_CHANNEL}}`
