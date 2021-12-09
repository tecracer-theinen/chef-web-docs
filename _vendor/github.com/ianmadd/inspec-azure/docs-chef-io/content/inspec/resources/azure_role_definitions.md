+++
title = "azure_role_definitions Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_role_definitions"
identifier = "inspec/resources/azure/azure_role_definitions Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_role_definitions.md">https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_role_definitions.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_role_definitions.md">https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_role_definitions.md</a></p>
</div>
</div>


Use the `azure_role_definitions` InSpec audit resource to test properties and configuration of multiple Azure role definitions.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_role_definitions` resource block returns all role definitions within a subscription.
```ruby
describe azure_role_definitions do
  it { should exist }
end
```

## Parameters

This resource does not require any parameters.

## Properties

`ids`
: A list of the unique resource ids.

: **Field**: `id`

`names`
: A list of names of all the resources being interrogated.

: **Field**: `name`

`role_names`
: A list of role names of all the role definitions being interrogated.

: **Field**: `role_name`

`types`
: A list of role type of all the role definitions being interrogated.

: **Field**: `type`

`properties`
: A list of properties for all the resources being interrogated.

: **Field**: `properties`

{{% inspec_filter_table %}}

## Examples

**Check a Specific Role Definition is Present.**

```ruby
describe azure_role_definitions do
  its('names')  { should include 'my-role' }
end
```
**Filter the Results to Include Only Those Role Definitions which Include the Given Name.**

```ruby
describe azure_role_definitions.where{ name.include?('my-role') } do
  it { should exist }
end
```
**Filter the Results to Include Only The Built-in Role Definitions.**

```ruby
describe azure_role_definitions.where{ type == "BuiltInRole" } do
  it { should exist }
  its('count') { should be 15 }
end
``` 
**Filter the Results to Include Only the Role Definitions that Contain `Kubernetes` in the Role Name.**

```ruby
describe azure_role_definitions.where{ role_name.include?('Kubernetes') } do
  it { should exist }
  its('count') { should be 15 }
end
```    

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

The control will pass if the filter returns at least one result. Use `should_not` if you expect zero matches.
```ruby
describe azure_role_definitions do
  it { should exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
