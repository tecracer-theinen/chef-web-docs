+++
title = "azure_data_factory_pipeline Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_data_factory_pipeline"
identifier = "inspec/resources/azure/azure_data_factory_pipeline Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_data_factory_pipeline.md">https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_data_factory_pipeline.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_data_factory_pipeline.md">https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_data_factory_pipeline.md</a></p>
</div>
</div>


Use the `azure_data_factory_pipeline` InSpec audit resource to test properties of an Azure pipeline.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

`resource_group` and `pipeline_name`, `factory_name` must be given as parameters.

```ruby
describe azure_data_factory_pipeline(resource_group: 'RESOURCE_GROUP', factory_name: 'FACTORY_NAME', pipeline_name: 'PIPELINE_NAME') do
  #...
end
```

## Parameters

`resource_group`
: Azure resource group that the targeted resource resides in. `MyResourceGroup`.

`factory_name`
: Name for the data factory that you want to create your pipeline in..

`pipeline_name`
: The pipeline name.

All the parameter sets needs be provided for a valid query:
- `resource_group` , `factory_name` and `pipeline_name`

## Properties

`name`
: Name of the Azure resource to test.

`id`
: The pipeline type.

`properties`
: The properties of the Resource.

## Examples

**Test That A Pipeline Exists.**

```ruby
describe azure_data_factory_pipeline(resource_group: 'RESOURCE_GROUP', factory_name: 'FACTORY_NAME', pipeline_name: 'PIPELINE_NAME') do
  it { should exist }
end
```

**Test That A Pipeline Does Not Exist.**

```ruby
describe azure_data_factory_pipeline(resource_group: 'RESOURCE_GROUP', factory_name: 'FACTORY_NAME', pipeline_name: 'PIPELINE_NAME') do
  it { should_not exist }
end
 ```

**Test Properties Of A Pipeline.**

```ruby
describe azure_data_factory_pipeline(resource_group: 'RESOURCE_GROUP', factory_name: 'FACTORY_NAME', pipeline_name: 'PIPELINE_NAME') do
  its('name') { should eq 'PIPELINE_NAME' }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
