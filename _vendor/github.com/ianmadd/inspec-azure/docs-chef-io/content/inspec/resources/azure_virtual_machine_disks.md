+++
title = "azure_virtual_machine_disks Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_virtual_machine_disks"
identifier = "inspec/resources/azure/azure_virtual_machine_disks Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_virtual_machine_disks.md">https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_virtual_machine_disks.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_virtual_machine_disks.md">https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_virtual_machine_disks.md</a></p>
</div>
</div>


Use the `azure_virtual_machine_disks` InSpec audit resource to test properties related to disks for a resource group or the entire subscription.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_virtual_machine_disks` resource block returns all disks, either within a Resource Group (if provided), or within an entire Subscription.
```ruby
describe azure_virtual_machine_disks do
  it { should exist }
end
```
or
```ruby
describe azure_virtual_machine_disks(resource_group: 'my-rg') do
  it { should exist }
end
```

## Parameters

- `resource_group` (Optional)

## Properties

`ids`
: A list of the unique resource ids.

: **Field**: `id`

`attached`
: Indicates whether the disk is currently mounted to a running VM.

: **Field**: `attached`

`resource_group`
: A list of resource groups for all the disks.

: **Field**: `resource_group`

`names`
: A list of names all the disks.

: **Field**: `name`

`locations`
: A list of locations of the disks.

: **Field**: `location`

`properties`
: A list of properties of the disks.

: **Field**: `properties`

`tags`
: A list of `tag:value` pairs defined on the resources.

: **Field**: `tags`

<superscript>*</superscript> For information on how to use filter criteria on plural resources refer to [FilterTable usage](https://github.com/inspec/inspec/blob/master/dev-docs/filtertable-usage.md).

## Examples

**Filter the Attached Disks.**

```ruby
describe azure_virtual_machine_disks(resource_group: 'MyResourceGroup').where(attached: true) do
  it { should exist }
  its('count') { should eq 3}
end
```   
**Loop through Disks by Their Ids  .**

```ruby
azure_virtual_machine_disks.ids.each do |id|
  describe azure_virtual_machine_disk(resource_id: id) do
    it { should exist }
  end
end  
``` 
**Test that There are Disks that Include a Certain String in their Names (Client Side Filtering)   .**

```ruby
describe azure_virtual_machine_disks(resource_group: 'MyResourceGroup').where { name.include?('Windows') } do
  it { should exist }
end
```    
**Test that There are Disks that Include a Certain String in their Names (Server Side Filtering via Generic Resource - Recommended)   .**

```ruby
describe azure_generic_resources(resource_provider: 'Microsoft.Compute/disks', substring_of_name: 'Windows') do
  it { should exist }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

```ruby
# Should not exist if no disks are in the resource group

describe azure_virtual_machine_disks(resource_group: 'MyResourceGroup') do
  it { should_not exist }
end

# Should exist if the filter returns a single virtual machine

describe azure_virtual_machine_disks.where(attached: true ) do
  it { should exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
