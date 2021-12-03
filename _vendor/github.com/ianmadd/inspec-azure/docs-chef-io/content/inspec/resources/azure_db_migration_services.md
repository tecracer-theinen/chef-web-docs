+++
title = "azure_db_migration_services Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_db_migration_services"
identifier = "inspec/resources/azure/azure_db_migration_services Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_db_migration_services.md">azure_db_migration_services.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_db_migration_services.md">azure_db_migration_services.md</a></p>
</div>
</div>



Use the `azure_db_migration_services` InSpec audit resource to test properties related to Azure DB Migration Service for a resource group or the entire subscription.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_db_migration_services` resource block returns all Azure DB Migration Services within a Resource Group.
```ruby
describe azure_db_migration_services(resource_group: 'my-rg') do
  #...
end
```
or
```ruby
describe azure_db_migration_services(resource_group: 'my-rg') do
  #...
end
```

## Parameters

- `resource_group`

## Properties

`ids`
: A list of the unique resource ids.

: **Field**: `id`

`names`
: A list of name for all the Resource names.

: **Field**: `name`

`types`
: A list of types for all the resources.

: **Field**: `type`

`locations`
: A list of locations for all the resources.

: **Field**: `location`

`kinds`
: A list of kinds for all the resources.

: **Field**: `kind`

`etags`
: A list of HTTP strong entity tag value.

: **Field**: `etag`

`tags`
: A list of resource tags.

: **Field**: `tags`

`sku_names`
: A list of SKU names.

: **Field**: `sku_name`

`sku_sizes`
: A list of SKU sizes.

: **Field**: `sku_sizes`

`sku_tiers`
: A list of SKU tiers.

: **Field**: `sku_tiers`

`provisioning_states`
: A list of provisioning_states from the properties.

: **Field**: `provisioning_state`

`virtual_nic_ids`
: A list of virtual nic IDs from the properties.

: **Field**: `virtual_nic_id`

`virtual_subnet_ids`
: A list of vitual subnet IDs from the properties.

: **Field**: `virtual_subnet_id`

<superscript>*</superscript> For information on how to use filter criteria on plural resources refer to [FilterTable usage](https://github.com/inspec/inspec/blob/master/dev-docs/filtertable-usage.md).

## Examples

**Loop through DB Migration Services by Their Names.**

```ruby
azure_db_migration_services(resource_group: 'my-rg').names.each do |name|
  describe azure_db_migration_service(service_name: name) do
    it { should exist }
  end
end  
```     
**Test that There are DB migration services that Includes a Certain String in their Names (Client Side Filtering).**

```ruby
describe azure_db_migration_services(resource_group: 'my-rg').where { name.include?('UAT') } do
  it { should exist }
end
```    

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

```ruby
# Should not exist if no db migration service are in the resource group

describe azure_db_migration_services(resource_group: 'my-rg') do
  it { should_not exist }
end

# Should exist if the filter returns at least one db migration service

describe azure_db_migration_services(resource_group: 'my-rg') do
  it { should exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
