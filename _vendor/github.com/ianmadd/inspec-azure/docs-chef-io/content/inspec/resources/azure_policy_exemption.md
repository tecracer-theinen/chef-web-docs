+++
title = "azure_policy_exemption Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_policy_exemption"
identifier = "inspec/resources/azure/azure_policy_exemption Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_policy_exemption.md">azure_policy_exemption.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_policy_exemption.md">azure_policy_exemption.md</a></p>
</div>
</div>



Use the `azure_policy_exemption` InSpec audit resource to test properties related to a Azure Policy Exemption.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

`name` must be given as a parameter and `resource_group` could be provided as an optional parameter
```ruby
describe azure_policy_exemption(resource_group: 'MyResourceGroup', name: '3b8b3f3bbec24cd6af583694') do
  it                                      { should exist }
  its('name')                             { should cmp '3b8b3f3bbec24cd6af583694' }
  its('type')                             { should cmp 'Microsoft.Authorization/policyExemptions' }
  its('properties.exemptionCategory')     { should cmp 'Waiver' }
  its('properties.policyAssignmentId')    { should cmp '/subscriptions/ae640e6b-ba3e-4256-9d62-2993eecfa6f2/providers/Microsoft.Authorization/policyAssignments/CostManagement' }
  its('systemData.createdByType')         { should cmp 'User' }
end
```
```ruby
describe azure_policy_exemption(name: '3b8b3f3bbec24cd6af583694') do
  it  { should exist }
end
```

## Parameters

`name`
: Name of the Azure Policy Exemption to test.

`resource_group`
: This is an optional parameter. Azure resource group that the targeted resource resides in. `MyResourceGroup`.

The parameter set should be provided for a valid query:
- `name`
- `resource_group` (optional) and `name` 

## Properties

`id`
: Resource ID.

`name`
: Policy Exemption Name.

`type`
: Resource type.

`properties.policyAssignmentId`
: The ID of the policy assignment that is being exempted.

`properties.policyDefinitionReferenceIds`
: The policy definition reference ID list when the associated policy assignment is an assignment of a policy set definition.

`properties.exemptionCategory`
: The policy exemption category. Possible values are Waiver and Mitigated.

`properties.displayName`
: The display name of the policy exemption.

`properties.description`
: The description of the policy exemption.

`systemData.createdBy`
: The identity that created the resource.

For properties applicable to all resources, such as `type`, `name`, `id`, `properties`, refer to [`azure_generic_resource`]({{< relref "azure_generic_resource.md#properties" >}}).

Also, refer to [Azure documentation](https://docs.microsoft.com/en-us/rest/api/policy/policy-exemptions/get) for other properties available.
Any attribute in the response may be accessed with the key names separated by dots (`.`).

## Examples

**Test <>.**

```ruby
describe azure_policy_exemption(name: '3b8b3f3bbec24cd6af583694') do
  its('properties.exemptionCategory') { should eq 'Waiver' }
end
```
**Test <>.**

```ruby
describe azure_policy_exemption(resource_group: 'MyResourceGroup', name: '3b8b3f3bbec24cd6af583694') do
  its('properties.policyDefinitionReferenceIds') { should include 'Limit_Skus' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](/inspec/matchers/).

### exists

```ruby
# If a policy exemption is found it will exist

describe azure_policy_exemption(name: '3b8b3f3bbec24cd6af583694') do
  it { should exist }
end

# policy exemptions that aren't found will not exist
describe azure_policy_exemption('3b8b3f3bbec24cd6af583694') do
  it { should_not exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
