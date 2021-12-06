+++
title = "azure_data_factory_linked_service Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_data_factory_linked_service"
identifier = "inspec/resources/azure/azure_data_factory_linked_service Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_data_factory_linked_service.md">https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_data_factory_linked_service.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_data_factory_linked_service.md">https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_data_factory_linked_service.md</a></p>
</div>
</div>


Use the `azure_data_factory_linked_service` InSpec audit resource to test the properties of an Azure Linked service.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

`resource_group`, `linked_service_name`, and `factory_name` are required parameters.

```ruby
describe azure_data_factory_linked_service(resource_group: `RESOURCE_GROUP`, factory_name: `FACTORY_NAME`, linked_service_name: `LINKED_SERVICE_NAME`) do
end
```

## Parameters

`resource_group`
: Azure resource group that the targeted resource resides in.

`factory_name`
: The factory name.

`linked_service_name`
: The name of the linked service.

All the parameter sets are required for a valid query:

- `resource_group` , `factory_name`, and `linked_service_name`.

## Properties

`name`
: Name of the Azure resource to test.

`type`
: The resource type.

`linked_service_type`
: The linked services type.

`type_properties`
: The properties of linked service type.

`properties`
: The properties of the resource.

## Examples

**Test that a Linked Service exists.**

```ruby
describe azure_data_factory_linked_service(resource_group: `RESOURCE_GROUP`, factory_name: `FACTORY_NAME`, linked_service_name: `LINKED_SERVICE_NAME`) do
  it { should exist }
end
```

**Test that a linked service does not exist.**

```ruby
describe azure_data_factory_linked_service(resource_group: `RESOURCE_GROUP`, factory_name: `FACTORY_NAME`, linked_service_name: 'should not exit') do
  it { should_not exist }
end
```

**Test properties of a linked service.**

```ruby
describe azure_data_factory_linked_service(resource_group: `RESOURCE_GROUP`, name: 'FACTORY_NAME') do
  its('name') { should eq linked_service_name1 }
  its('type') { should eq 'Microsoft.DataFactory/factories/linkedservices' }
  its('linked_service_type') { should eq 'MYSQL' }
end
```

## Azure Permissions

Your [Service Principal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal) must be set up with a `contributor` role on the subscription you wish to test.
