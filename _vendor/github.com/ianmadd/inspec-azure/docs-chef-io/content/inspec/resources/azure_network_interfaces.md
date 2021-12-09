+++
title = "azure_network_interfaces Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_network_interfaces"
identifier = "inspec/resources/azure/azure_network_interfaces Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_network_interfaces.md">https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_network_interfaces.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_network_interfaces.md">https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_network_interfaces.md</a></p>
</div>
</div>


Use the `azure_network_interfaces` InSpec audit resource to test properties and configuration of Azure Network Interfaces.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_network_interfaces` resource block returns all Azure Network Interfaces, either within a Resource Group (if provided), or within an entire Subscription.
```ruby
describe azure_network_interfaces do
  #...
end
```
or
```ruby
describe azure_network_interfaces(resource_group: 'my-rg') do
  #...
end
```

## Parameters

`resource_group` _(optional)_

: The name of the resource group.

## Properties

`ids`
: A list of the unique resource ids.

: **Field**: `id`

`locations`
: A list of locations for all the resources being interrogated.

: **Field**: `location`

`names`
: A list of names of all the resources being interrogated.

: **Field**: `name`

`tags`
: A list of `tag:value` pairs defined on the resources being interrogated.

: **Field**: `tags`

`types`
: A list of the types of resources being interrogated.

: **Field**: `type`

`properties`
: A list of properties for all the resources being interrogated.

: **Field**: `properties`

{{% inspec_filter_table %}}

## Examples

**Check Network Interfaces are Present.**

```ruby
describe azure_network_interfaces do
  it            { should exist }
  its('names')  { should include 'my-network-interface' }
end
```
**Filter the Results to Include Only those with Names Match the Given String Value.**

```ruby
describe azure_network_interfaces.where{ name.include?('my-network') } do
  its('count') { should > 3 }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

The control will pass if the filter returns at least one result. Use `should_not` if you expect zero matches.
```ruby
# If we expect 'ExampleGroup' Resource Group to have Network Interfaces
describe azure_network_interfaces(resource_group: 'ExampleGroup') do
  it { should exist }
end

# If we expect 'EmptyExampleGroup' Resource Group to not have Network Interfaces
describe azure_network_interfaces(resource_group: 'EmptyExampleGroup') do
  it { should_not exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}

