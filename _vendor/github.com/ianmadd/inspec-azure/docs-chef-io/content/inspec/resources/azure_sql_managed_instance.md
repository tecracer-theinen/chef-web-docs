+++
title = "azure_sql_managed_instance Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_sql_managed_instance"
identifier = "inspec/resources/azure/azure_sql_managed_instance Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_sql_managed_instance.md">azure_sql_managed_instance.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_sql_managed_instance.md">azure_sql_managed_instance.md</a></p>
</div>
</div>



Use the `azure_sql_managed_instance` InSpec audit resource to test the properties related to an Azure SQL managed instance.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

`name`, `resource_group` are required parameters.

```ruby
describe azure_sql_managed_instance(resource_group: 'RESOURCE_GROUP', name: 'INSTANCE_NAME') do
  it                                      { should exist }
  its('type')                             { should eq 'Microsoft.Sql/managedInstances' }
  its('location')                         { should eq 'eastus' }
end
```

```ruby
describe azure_sql_managed_instance(resource_group: 'RESOURCE_GROUP', name: 'INSTANCE_NAME') do
  it  { should exist }
end
```

## Parameters

`name`
: Name of the Azure SQL managed instances to test.

`resource_group`
: Azure resource group that the targeted resource resides in.

The parameter set should be provided for a valid query: `resource_group` and `name`

## Properties

`id`
: Resource ID.

`name`
: Resource name.

`type`
: Resource type.

`location`
: Resource location.

`properties`
: The properties of the SQL Managed Instance.

`properties.minimalTlsVersion`
: Minimal TLS version. Allowed values are 'None', '1.0', '1.1', '1.2'.

`properties.maintenanceConfigurationId`
: Specifies maintenance configuration id to apply to this managed instance.

`properties.provisioningState`
: Provisioning state of the SQL managed instance.

`sku.name`
: The name of the SKU, typically, a letter with a number code. For example, P3.

For properties applicable to all resources, such as `type`, `name`, `id`, `properties` refer to [`azure_generic_resource`]({{< relref "azure_generic_resource.md#properties" >}}). Also, refer to [Azure documentation](https://docs.microsoft.com/en-us/rest/api/sql/2021-02-01-preview/managed-instances/get) for other properties available.

## Examples

**Test that the SQL managed instances is provisioned successfully.**

```ruby
describe azure_sql_managed_instance(resource_group: 'RESOURCE_GROUP', name: 'INSTANCE_NAME') do
  its('properties.provisioningState') { should eq 'Succeeded' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](/inspec/matchers/).

### exists

```ruby
# If a SQL managed instance is found, it will exist
describe azure_sql_managed_instance(resource_group: 'RESOURCE_GROUP', name: 'INSTANCE_NAME') do
  it { should exist }
end
# if SQL managed instance is not found, it will not exist
describe azure_sql_managed_instance(resource_group: 'RESOURCE_GROUP', name: 'INSTANCE_NAME') do
  it { should_not exist }
end
```

## Azure Permissions

Your [Service Principal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal) must be set up with a `reader` role on the subscription you wish to test.
