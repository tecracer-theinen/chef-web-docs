+++
title = "azure_resource_groups Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_resource_groups"
identifier = "inspec/resources/azure/azure_resource_groups Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_resource_groups.md">azure_resource_groups.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_resource_groups.md">azure_resource_groups.md</a></p>
</div>
</div>



Use the `azure_resource_groups` InSpec audit resource to test properties and configuration of multiple Azure resource groups.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_resource_groups` resource block returns all resource groups within a subscription.
```ruby
describe azure_resource_groups do
  it { should exist }
end
```

## Parameters

- None required.

## Properties

`ids`
: A list of the unique resource group ids.

: **Field**: `id`

`names`
: A list of names of all the resource groups.

: **Field**: `name`

`tags`
: A list of `tag:value` pairs defined on the resource groups.

: **Field**: `tags`

`locations`
: A list of locations of all the resource groups.

: **Field**: `location`

<superscript>*</superscript> For information on how to use filter criteria on plural resources refer to [FilterTable usage](https://github.com/inspec/inspec/blob/master/dev-docs/filtertable-usage.md).

## Examples

**Check a Specific Resource Group is Present.**

```ruby
describe azure_resource_groups do
  its('names')  { should include 'my-resource-group' }
end
```
**Filters the Results to Include Only Those Resource Groups which Include the Given Name.**

```ruby
describe azure_resource_groups.where{ name.include?('my-resource-group') } do
  it { should exist }
end
```
**Filters the Results to Include Only The Resource Groups that Have Certain Tag.**

```ruby
describe azure_resource_groups.where{ tags.has_key?('owner') && tags['owner'] == "InSpec" } do
  it { should exist }
  its('count') { should be 15 }
end
```    

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

The control will pass if the filter returns at least one result. Use `should_not` if you expect zero matches.
```ruby
describe azure_resource_groups do
  it { should exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
