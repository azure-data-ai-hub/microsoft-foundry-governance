# Deny creation of Azure AI Foundry Hub

## Description

This policy denies the creation of **Azure AI Foundry Hub** workspaces in Azure. It targets resources of type `Microsoft.MachineLearningServices/workspaces` that have a `kind` of `Hub`.

## Policy Rule

| Property | Value |
|---|---|
| Resource type | `Microsoft.MachineLearningServices/workspaces` |
| Kind | `Hub` |
| Default effect | `Deny` |

## Parameters

| Parameter | Type | Allowed values | Default |
|---|---|---|---|
| `effect` | String | `Deny`, `Audit`, `Disabled` | `Deny` |

## Files

| File | Description |
|---|---|
| `azurepolicy.json` | Full policy definition (name, properties, parameters, and rule) |
| `azurepolicy.parameters.json` | Policy parameters only |
| `azurepolicy.rules.json` | Policy rule only |

## Deployment

### Azure CLI

```bash
# Create the policy definition
az policy definition create \
  --name "deny-foundry-hub" \
  --display-name "Deny creation of Azure AI Foundry Hub" \
  --description "Denies the creation of Azure AI Foundry Hub workspaces." \
  --rules policies/deny-foundry-hub/azurepolicy.rules.json \
  --params policies/deny-foundry-hub/azurepolicy.parameters.json \
  --mode All

# Assign the policy to a subscription
az policy assignment create \
  --name "deny-foundry-hub-assignment" \
  --policy "deny-foundry-hub" \
  --scope "/subscriptions/<subscription-id>"
```

### Azure PowerShell

```powershell
# Create the policy definition
$definition = New-AzPolicyDefinition `
  -Name "deny-foundry-hub" `
  -DisplayName "Deny creation of Azure AI Foundry Hub" `
  -Description "Denies the creation of Azure AI Foundry Hub workspaces." `
  -Policy "policies/deny-foundry-hub/azurepolicy.rules.json" `
  -Parameter "policies/deny-foundry-hub/azurepolicy.parameters.json" `
  -Mode All

# Assign the policy to a subscription
New-AzPolicyAssignment `
  -Name "deny-foundry-hub-assignment" `
  -PolicyDefinition $definition `
  -Scope "/subscriptions/<subscription-id>"
```
