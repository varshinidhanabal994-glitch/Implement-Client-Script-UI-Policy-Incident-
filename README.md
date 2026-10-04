# Implement Client Script & UI Policy (Incident)

ServiceNow micro-project based on the provided project documentation.

## Project objective

This project demonstrates client-side controls on the ServiceNow **Incident** table using:

- UI Policy
- UI Policy Action
- onChange Client Script
- onSubmit Client Script
- onCellEdit Client Script

The configuration controls Incident field behavior when **Impact = High**, validates **Assigned To**, automatically sets **Urgency**, and blocks direct State changes from list editing.

## Project configuration

### 1. UI Policy

| Property | Value |
|---|---|
| Name | High Impact Control |
| Table | Incident |
| Active | true |
| Condition | Impact is High |

### 2. UI Policy Action

| Property | Value |
|---|---|
| UI Policy | High Impact Control |
| Field | Urgency |
| Read only | true |
| Visible | unchanged |

When Impact is High, Urgency becomes read-only.

### 3. onChange Client Script

| Property | Value |
|---|---|
| Name | Auto set urgency for high impact |
| Table | Incident |
| Type | onChange |
| Field name | Impact |
| Active | true |

When Impact becomes High, Urgency is set automatically.

### 4. onSubmit Client Script

| Property | Value |
|---|---|
| Name | Prevent save if Assigned To missing |
| Table | Incident |
| Type | onSubmit |
| Active | true |

When Impact is High and Assigned To is empty, the Incident cannot be saved.

### 5. onCellEdit Client Script

| Property | Value |
|---|---|
| Name | Prevent state change via list edit |
| Table | Incident |
| Type | onCellEdit |
| Field | State |
| Active | true |

Direct State editing from the Incident list is blocked.

## Folder structure

```text
implement_client_script_ui_policy_incident/
│
├── README.md
├── .gitignore
│
├── client_scripts/
│   ├── auto_set_urgency_high_impact.js
│   ├── prevent_save_assigned_to_missing.js
│   └── prevent_state_change_list_edit.js
│
├── ui_policy/
│   ├── high_impact_control.md
│   └── urgency_ui_policy_action.md
│
└── documentation/
    ├── configuration_steps.md
    └── test_cases.md
```

## How to implement in ServiceNow

The `.js` files are source-code copies for GitHub/documentation. They are not executed from GitHub.

In ServiceNow:

1. Go to **System UI > UI Policies**.
2. Create the `High Impact Control` UI Policy for the Incident table.
3. Set the condition to `Impact is High`.
4. Add a UI Policy Action for `Urgency`.
5. Set `Read only = true`.
6. Go to **System UI > Client Scripts**.
7. Create the three Client Scripts using the properties and code in this repository.
8. Test each configuration using the test cases in `documentation/test_cases.md`.

## Important

Do not upload ServiceNow usernames, passwords, session cookies, API keys, or other secrets to GitHub.

If you want to upload the actual ServiceNow configuration as an importable package, first create an **Update Set** in your ServiceNow instance, add these records to it, complete it, and export the generated XML. The XML contains instance-specific record information and should be exported from the actual instance rather than invented manually.
