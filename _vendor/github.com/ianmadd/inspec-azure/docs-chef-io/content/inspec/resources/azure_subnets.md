+++
title = "azure_subnets Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_subnets"
identifier = "inspec/resources/azure/azure_subnets Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_subnets.md">https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_subnets.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_subnets.md">https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_subnets.md</a></p>
</div>
</div>


Use the `azure_subnets` InSpec audit resource to test properties related to subnets of a virtual network.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

The `resource_group` and `vnet` must be given as a parameter.
```ruby
describe azure_subnets(resource_group: 'MyResourceGroup', vnet: 'MyVnetName') do
  #...
end
```

## Parameters

`resource_group`
: Azure resource group that the targeted resource resides in. `MyResourceGroup`.

`vnet`
: The virtual network that the subnet that you wish to test is a part of.

## Properties

`ids`
: A list of the unique resource ids.

: **Field**: `id`

`names`
: A list of all the resources being interrogated.

: **Field**: `name`

`etags`
: A list of etags defined on the resources.

: **Field**: `etag`

{{% inspec_filter_table %}}

## Examples

**Exists if Any Subnets Exist for a Given Virtual Network in the Resource Group.**

```ruby
describe azure_subnets(resource_group: 'MyResourceGroup', vnet: 'MyVnetName') do
  it { should exist }
end
```
**Filters the Results to Only Those that Match the Given Name.**

```ruby
describe azure_subnets(resource_group: 'MyResourceGroup', vnet: 'MyVnetName')
  .where(name: 'MySubnet') do
  it { should exist }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

```ruby
# Should not exist if no subnets are in the virtual network

describe azure_subnets(resource_group: 'MyResourceGroup', vnet: 'MyVnetName') do
  it { should_not exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
