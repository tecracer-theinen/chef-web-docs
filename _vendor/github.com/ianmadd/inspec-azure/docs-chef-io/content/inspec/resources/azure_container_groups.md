+++
title = "azure_container_groups Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_container_groups"
identifier = "inspec/resources/azure/azure_container_groups Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_container_groups.md">azure_container_groups.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_container_groups.md">azure_container_groups.md</a></p>
</div>
</div>



Use the `azure_container_groups` InSpec audit resource to test properties related to all Azure container groups within a subscription.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_container_groups` resource block returns all Azure container groups within a subscription.

```ruby
describe azure_container_groups do
  #...
end
```

## Parameters

This resource does not have any required parameters.

## Properties

`ids`
: A list of the unique resource IDs.

: **Field**: `id`

`names`
: A list of names for all the resources.

: **Field**: `name`

`types`
: A list of types for all the resources.

: **Field**: `type`

`locations`
: A list of the resource location for all the resources.

: **Field**: `location`

`tags`
: A list of tags for all the resources.

: **Field**: `tags`

`properties`
: A list of Properties all the resources.

: **Field**: `properties`

`containers`
: A list of containers within the container group.

: **Field**: `containers`

`init_containers`
: A list of init containers for a container group.

: **Field**: `init_containers`

`image_registry_credentials`
: A list of image registry credentials by which the container group is created from.

: **Field**: `image_registry_credentials`

`ip_address`
: A list of IP address type of the container group.

: **Field**: `ip_address`

`os_types`
: A list of operating system types required by the containers in the container group.

: **Field**: `os_type`

`provisioning_states`
: A list of provisioning states of the container group.

: **Field**: `provisioning_state`

`volumes`
: A list of volumes that can be mounted by containers in this container group.

: **Field**: `volumes`

`skus`
: A list SKU for a container group.

: **Field**: `sku`

`restart_policies`
: A list of restart policies for all containers within the container group.

: **Field**: `restart_policy`

<superscript>*</superscript> For information on how to use filter criteria on plural resources refer to [FilterTable usage](https://github.com/inspec/inspec/blob/master/dev-docs/filtertable-usage.md).

## Examples

**Loop through container groups by their names.**

```ruby
azure_container_groups.names.each do |name|
  describe azure_container_group(resource_group: 'RESOURCE_GROUP_NAME', name: 'CONTAINER_GROUP_NAME') do
    it { should exist }
  end
end
```

**Test that there are container groups with valid name.**

```ruby
describe azure_container_groups.where(name: 'CONTAINER_GROUP_NAME') do
  it { should exist }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

```ruby
# Should not exist if no container groups are present in the subscription

describe azure_container_groups do
  it { should_not exist }
end

# Should exist if the filter returns at least one container group in the subscription

describe azure_container_groups do
  it { should exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
