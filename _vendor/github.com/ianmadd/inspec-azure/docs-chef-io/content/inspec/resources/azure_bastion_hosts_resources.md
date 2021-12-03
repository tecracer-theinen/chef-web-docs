+++
title = "azure_bastion_hosts_resource Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_bastion_hosts_resource"
identifier = "inspec/resources/azure/azure_bastion_hosts_resource Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_bastion_hosts_resources.md">azure_bastion_hosts_resources.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_bastion_hosts_resources.md">azure_bastion_hosts_resources.md</a></p>
</div>
</div>



Use the `azure_bastion_hosts_resource` InSpec audit resource to test properties related to bastion hots for a resource group or the entire subscription.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_bastion_hosts_resource` resource block returns all Azure bastion hots, either within a Resource Group (if provided)
```ruby
describe azure_bastion_hosts_resource(resource_group: 'my-rg') do

end
```

## Properties

`name`
: A list of the unique resource names.

: **Field**: `name`

`ids`
: A list of bastion hosts ids .

: **Field**: `id`

`tags`
: A list of `tag:value` pairs defined on the resources.

: **Field**: `tags`

`provisioning_states`
: State of BastionHosts creation.

: **Field**: `provisioningState`

`types`
: Types of all the bastion hosts.

: **Field**: `type`

`properties`
: Types of all the bastion hosts.

: **Field**: `properties`

<superscript>*</superscript> For information on how to use filter criteria on plural resources refer to [FilterTable usage](https://github.com/inspec/inspec/blob/master/dev-docs/filtertable-usage.md).

## Examples

**Ensure that the bastion hosts resource has is from same type.**

```ruby
describe azure_bastion_hosts_resource(resource_group: 'MyResourceGroup', name: 'bastion_name') do
  its('type') { should eq 'Microsoft.Network/bastionHosts' }
end
```
**Ensure that the bastion hosts resource is in successful state.**

```ruby
describe azure_bastion_hosts_resource(resource_group: 'MyResourceGroup') do
  its('provisioning_states') { should include('Succeeded') }
end
```

**Ensure that the bastion hosts resource is from same location.**

```ruby
describe azure_bastion_hosts_resource(resource_group: 'MyResourceGroup') do
  its('location') { should include df_location }
end
```
**Test If Any bastion hots Exist in the Resource Group.**

```ruby
describe azure_bastion_hosts_resource(resource_group: 'MyResourceGroup') do
  it { should exist }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

```ruby
# Should not exist if no bastion hots are in the resource group

describe azure_bastion_hosts_resource(resource_group: 'MyResourceGroup') do
  it { should_not exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
