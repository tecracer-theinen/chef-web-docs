+++
title = "azure_container_group Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_container_group"
identifier = "inspec/resources/azure/azure_container_group Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_container_group.md">https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_container_group.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_container_group.md">https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_container_group.md</a></p>
</div>
</div>


Use the `azure_container_group` InSpec audit resource to test properties related to an Azure container group.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

`name` is a required parameter and `resource_group` could be provided as an optional parameter.

```ruby
describe azure_container_group(resource_group: 'RESOURCE_GROUP_NAME', name: 'CONTAINER_GROUP_NAME') do
  it                                      { should exist }
  its('name')                             { should cmp 'demo1' }
  its('type')                             { should cmp 'Microsoft.ContainerInstance/containerGroups' }
  its('location')                         { should cmp 'WestUs'}
end
```

```ruby
describe azure_container_group(resource_group: 'RESOURCE_GROUP_NAME', name: 'CONTAINER_GROUP_NAME') do
  it  { should exist }
end
```

## Parameters

`name`
: Name of the Azure container group to test.

`resource_group`
: Azure resource group that the targeted resource resides in. `MyResourceGroup`.

The parameter set should be provided for a valid query:
- `resource_group` and `name`

## Properties

`id`
: The resource ID.

`name`
: The container group name.

`type`
: The resource type.

`location`
: The resource location.

`properties`
: The properties of the resource.


For properties applicable to all resources, such as `type`, `name`, `id`, `properties`, refer to [`azure_generic_resource`]({{< relref "azure_generic_resource.md#properties" >}}).

Also, refer to [Azure documentation](https://docs.microsoft.com/en-us/rest/api/container-instances/container-groups/get) for other properties available.
Any attribute in the response may be accessed with the key names separated by dots (`.`).

## Examples

**Test that the container group has a public IP address.**

```ruby
describe azure_container_group(resource_group: 'RESOURCE_GROUP_NAME', name: 'CONTAINER_GROUP_NAME') do
  its('properties.ipAddress.type') { should eq 'Public'}
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](/inspec/matchers/).

### exists

```ruby
# If a container group is found it will exist

describe azure_container_group(resource_group: 'RESOURCE_GROUP_NAME', name: 'CONTAINER_GROUP_NAME') do
  it { should exist }
end

# container groups that aren't found will not exist
describe azure_container_group(resource_group: 'RESOURCE_GROUP_NAME', name: 'CONTAINER_GROUP_NAME') do
  it { should_not exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
