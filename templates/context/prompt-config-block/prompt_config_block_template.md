---
id: "allzy.framework.templates.context.prompt-config-block"
title: "Prompt Config Block Template"
artifact_type: "Template"
template_family: "context.prompt-config-block"
status: "Draft"
version: "0.2.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - template
  - prompt-config
  - context
---

## Template Body

Copy the YAML block below.

---

```yaml
config:
  config_version: "1.0.0"

  mode: "" # preconfigured | manual_config | assistant | fallback
  workflow: "" # genesis | triage | workspace_context | retrieval | metadata_enrichment | specification | custom
  output_mode: "" # depends on workflow

  user_intent: ""
  task_goal: ""
  task_scope: ""
  requested_output: ""

  target_model: ""
  target_platform: ""
  model_reference_available: false
  platform_reference_available: false
  model_optimization_allowed: false
  platform_optimization_allowed: false

  fallback:
    allow_universal_markdown_fallback: true
    fallback_label_required: true
    explain_fallback_limitations: true

  assistant_mode:
    ask_if_required_config_missing: true
    ask_one_question_at_a_time: true
    proceed_if_only_optional_details_missing: true
    include_optional_clarifications_block: true

  files:
    allow_file_creation: false
    allow_file_updates: false
    allowed_create_paths: []
    allowed_update_paths: []
    required_inputs: []
    optional_inputs: []

  retrieval:
    use_deterministic_retrieval: true
    require_retrieval_initialization_check: true
    context_retrieval_file: "context_retrieval.md"
    use_metadata_index_if_available: true
    include_search_log: true
    output_context_package: false

  metadata:
    use_frontmatter: true
    preserve_existing_metadata: true
    mark_inferred_fields: true
    mark_missing_context: true

  privacy:
    reject_real_secrets: true
    allow_placeholders_for_secrets: true
    secret_placeholder_style: "$ENV_SECRET_NAME"

  quality:
    preserve_scope_boundaries: true
    do_not_invent_missing_rules: true
    mark_open_questions: true
    mark_contract_gaps: true
```

# Prompt Config Block Template

Use this template as the standard config block for operational prompts.

## Purpose

Prompt config controls prompt execution.

It does not describe a permanent document artifact.

## Core Modes

| Mode | Meaning |
|---|---|
| `preconfigured` | Website or prompt builder filled the config |
| `manual_config` | User manually filled the config |
| `assistant` | Required config is missing; assistant asks targeted questions |
| `fallback` | Prompt can proceed generically but must label limitations |

## Rules

- If config is filled, execute according to config.
- If required config is missing, switch to Assistant Mode.
- If only non-critical details are missing, proceed and list optional clarifications.
- Do not claim model/platform optimization without reference content.
- Do not treat prompt config as document frontmatter.
