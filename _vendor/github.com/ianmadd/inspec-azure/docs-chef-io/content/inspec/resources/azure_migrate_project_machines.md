+++
title = "azure_migrate_project_machines Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_migrate_project_machines"
identifier = "inspec/resources/azure/azure_migrate_project_machines Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_migrate_project_machines.md">azure_migrate_project_machines.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_migrate_project_machines.md">azure_migrate_project_machines.md</a></p>
</div>
</div>



Use the `azure_migrate_project_machines` InSpec audit resource to test the properties related to all Azure Migrate project machines within a project.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_migrate_project_machines` resource block returns all Azure Migrate project machines within a project.

```ruby
describe azure_migrate_project_machines(resource_group: 'RESOURCE_GROUP', project_name: 'PROJECT_NAME') do
  #...
end
```

## Parameters

`resource_group`
: Azure resource group that the targeted resource resides in.

`project_name`
: Azure Migrate project name.

The parameter set should be provided for a valid query:
- `resource_group` and `project_name`.

## Properties

`ids`
: Path reference to the project machines.

: **Field**: `id`

`names`
: Unique names for all project machines.

: **Field**: `name`

`types`
: Type of the objects.

: **Field**: `type`

`properties`
: A list of properties for all the project machines.

: **Field**: `properties`

`discoveryData`
: The discovery details of all the machine published by various sources.

: **Field**: `discoveryData`

`assessmentData`
: The assessment details of all the machine published by various sources.

: **Field**: `assessmentData`

`migrationData`
: The migration details of all the machine published by various sources.

: **Field**: `migrationData`

`lastUpdatedTimes`
: The times of the last modification of all the machines.

: **Field**: `lastUpdatedTime`

<superscript>*</superscript> For information on how to use filter criteria on plural resources refer to [FilterTable usage](https://github.com/inspec/inspec/blob/master/dev-docs/filtertable-usage.md). For more details on the available properties please refer to [Azure documentation](https://docs.microsoft.com/en-us/rest/api/migrate/projects/machines/enumerate-machines).

## Examples

**Loop through migrate project machines by their names.**

```ruby
azure_migrate_project_machines(resource_group: 'RESOURCE_GROUP', project_name: 'PROJECT_NAME').names.each do |name|
  describe azure_migrate_project_machine(resource_group: 'RESOURCE_GROUP', project_name: 'PROJECT_NAME', name: `NAME`) do
    it { should exist }
  end
end
```

**Test that there are migrate project machines with Windows OS.**

```ruby
describe azure_migrate_project_machines(resource_group: 'RESOURCE_GROUP', project_name: 'PROJECT_NAME').where{ discoveryData.detect{ |data| data[:osType] == 'WINDOWSGUEST' } } do
  it { should exist }
end
```

**Test that the migrate project machines is of BIOS boot type.**

```ruby
describe azure_migrate_project_machines(resource_group: 'RESOURCE_GROUP', project_name: 'PROJECT_NAME').where{ discoveryData.detect{ |data| data[:extendedInfo][:bootType] == 'BIOS' } } do
  it { should exist }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

```ruby
# Should not exist, if no migrate project machines are present in the project and in the resource group
describe azure_migrate_project_machines(resource_group: 'migrate_vms', project_name: 'zoneA_migrate_project') do
  it { should_not exist }
end
# Should exist, if the filter returns at least one migrate project machines in the project and in the resource group
describe azure_migrate_project_machines(resource_group: 'RESOURCE_GROUP', project_name: 'PROJECT_NAME') do
  it { should exist }
end
```

## Azure Permissions

Your [Service Principal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal) must be set up with a `contributor` role on the subscription you wish to test.
