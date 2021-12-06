+++
title = "azure_key_vaults Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_key_vaults"
identifier = "inspec/resources/azure/azure_key_vaults Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_key_vaults.md">https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_key_vaults.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_key_vaults.md">https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_key_vaults.md</a></p>
</div>
</div>


Use the `azure_key_vaults` InSpec audit resource to test properties related to key vaults for a resource group or the entire subscription.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_key_vaults` resource block returns all Azure key vaults, either within a Resource Group (if provided), or within an entire Subscription.
```ruby
describe azure_key_vaults do
  #...
end
```
or
```ruby
describe azure_key_vaults(resource_group: 'my-rg') do
  #...
end
```

## Parameters

- `resource_group` (Optional)

## Properties

`ids`
: A list of the unique resource ids.

: **Field**: `id`

`names`
: A list of all the key vault names.

: **Field**: `name`

`tags`
: A list of `tag:value` pairs defined on the resources.

: **Field**: `tags`

`types`
: A list of types of all the key vaults.

: **Field**: `type`

`locations`
: A list of locations for all the key vaults.

: **Field**: `location`

`properties`
: A list of properties for all the key vaults.

: **Field**: `properties`

<superscript>*</superscript> For information on how to use filter criteria on plural resources refer to [FilterTable usage](https://github.com/inspec/inspec/blob/master/dev-docs/filtertable-usage.md).

## Examples

**Loop through Key Vaults by Their Ids  .**

```ruby
azure_key_vaults.ids.each do |id|
  describe azure_key_vault(resource_id: id) do
    it { should exist }
  end
end  
```     
**Test that There are Key Vaults that Includes a Certain String in their Names (Client Side Filtering)   .**

```ruby
describe azure_key_vaults.where { name.include?('deployment') } do
  it { should exist }
end
```    
**Test that There are Key Vaults that Includes a Certain String in their Names (Server Side Filtering via Generic Resource - Recommended)   .**

```ruby
describe azure_generic_resources(resource_provider: 'Microsoft.KeyVault/vaults', substring_of_name: 'deployment') do
  it { should exist }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

```ruby
# Should not exist if no key vaults are in the resource group

describe azure_key_vaults(resource_group: 'MyResourceGroup') do
  it { should_not exist }
end

# Should exist if the filter returns at least one key vault

describe azure_key_vaults(resource_group: 'MyResourceGroup') do
  it { should exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
