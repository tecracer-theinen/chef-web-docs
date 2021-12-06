+++
title = "azure_resource_health_availability_status Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_resource_health_availability_status"
identifier = "inspec/resources/azure/azure_resource_health_availability_status Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_resource_health_availability_status.md">https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_resource_health_availability_status.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_resource_health_availability_status.md">https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_resource_health_availability_status.md</a></p>
</div>
</div>


Use the `azure_resource_health_availability_status` InSpec audit resource to test properties related to a Azure Resource Health availability status.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

`resource_group`, `resource_type` and `name` are required parameters.

```ruby
describe azure_resource_health_availability_status(resource_group: 'AZURE_RESOURCE_GROUP', resource_type: 'AZURE_RESOURCE_TYPE', name: 'RESOURCE_NAME') do
  it                                      { should exist }
  its('name')                             { should cmp 'current' }
  its('type')                             { should cmp 'Microsoft.ResourceHealth/AvailabilityStatuses' }
  its('location')                         { should cmp 'ukwest' }
  its('properties.availabilityState')     { should cmp 'Available' }
  its('properties.reasonChronicity')      { should cmp 'Persistent' }
end
```

## Parameters

`name`
: Name of the Azure resource to test.

`resource_group`
: Azure resource group that the targeted resource resides in.

`resource_type`
: Azure resource type of the targeted resource.

The parameter set should be provided for a valid query:
- `resource_group`, `resource_type` and `name`

## Properties

`id`
: Azure Resource Manager Identity for the availabilityStatuses resource.

`name`
: current.

`type`
: `Microsoft.ResourceHealth/AvailabilityStatuses`.

`location`
: Azure Resource Manager geo location of the resource.

`properties`
: Properties of availability state.

For properties applicable to all resources, such as `type`, `name`, `id`, `properties`, refer to [`azure_generic_resource`]({{< relref "azure_generic_resource.md#properties" >}}).

Also, refer to [Azure documentation](https://docs.microsoft.com/en-us/rest/api/resourcehealth/availability-statuses/get-by-resource) for other properties available.
Any attribute in the response may be accessed with the key names separated by dots (`.`).

## Examples

**Test availability status of a resource.**

```ruby
describe azure_resource_health_availability_status(resource_group: 'AZURE_RESOURCE_GROUP', resource_type: 'AZURE_RESOURCE_TYPE', name: 'RESOURCE_NAME') do
  its('properties.availabilityState') { should eq 'Available' }
end
```

**Test the chronicity type of a resource.**

```ruby
describe azure_resource_health_availability_status(resource_group: 'AZURE_RESOURCE_GROUP', resource_type: 'AZURE_RESOURCE_TYPE', name: 'RESOURCE_NAME') do
  its('properties.reasonChronicity') { should include 'Persistent' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](/inspec/matchers/).

### exists

```ruby
# If a resource status is found it will exist

describe azure_resource_health_availability_status(resource_group: 'AZURE_RESOURCE_GROUP', resource_type: 'AZURE_RESOURCE_TYPE', name: 'RESOURCE_NAME') do
  it { should exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
