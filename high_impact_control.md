# UI Policy: High Impact Control

## ServiceNow record

- Table: Incident
- Name: High Impact Control
- Active: true
- Condition: Impact is High

## Purpose

When an Incident has High Impact, the policy applies additional field controls.

## Condition

```text
Impact is High
```

## Expected behavior

The UI Policy triggers when the Incident's Impact is High and controls the Urgency field through its UI Policy Action.
