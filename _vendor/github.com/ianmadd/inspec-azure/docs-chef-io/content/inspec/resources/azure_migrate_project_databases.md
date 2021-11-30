+++
title = "azure_migrate_project_database Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_migrate_project_database"
identifier = "inspec/resources/azure/azure_migrate_project_database Resource"
parent = "inspec/resources/azure"
+++

Use the `azure_migrate_project_database` InSpec audit resource to test the properties related to all Azure Migrate Project Databases within a project.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_migrate_project_database` resource block returns all Azure Migrate Project Databases within a project.

```ruby
describe azure_migrate_project_database(resource_group: 'RESOURCE_GROUP', project_name: 'PROJECT_NAME') do
  #...
end
```

## Parameters

| Name           | Description                                                                      |
|----------------|----------------------------------------------------------------------------------|
| resource_group | Azure resource group that the targeted resource resides in.                      |
| project_name   | Azure Migrate Project.                                                           |

The parameter set should be provided for a valid query:

- `resource_group` and `project_name`.

## Properties

`ids`
: Path reference to the Project Databases.

: **Field**: `id`

`names`
: Unique names for all Project Databases.

: **Field**: `name`

`types`
: Type of the objects.

: **Field**: `type`

`properties`
: A list of Properties for all the Project Databases.

: **Field**: `properties`

`assessmentDatas`
: The assessment details of the database published by various sources.

: **Field**: `assessmentData`

`assessmentIds`
: The database assessment scopes/Ids.

: **Field**: `assessmentId`

`assessmentTargetTypes`
: The assessed target database types.

: **Field**: `assessmentTargetType`

`breakingChangesCounts`
: The number of breaking changes found.

: **Field**: `breakingChangesCount`

`compatibilityLevels`
: The compatibility levels of the database.

: **Field**: `compatibilityLevel`

`databaseNames`
: The database names.

: **Field**: `databaseName`

`databaseSizeInMBs`
: The sizes of the databases.

: **Field**: `databaseSizeInMB`

`enqueueTimes`
: The list of times the message is enqueued.

: **Field**: `enqueueTime`

`extendedInfos`
: The extended properties of all the database.

: **Field**: `extendedInfo`

`instanceIds`
: The database server instance Ids.

: **Field**: `instanceId`

`isReadyForMigrations`
: The values indicating whether the database is ready for migration.

: **Field**: `isReadyForMigration`

`lastAssessedTimes`
: The time when the databases were last assessed.

: **Field**: `lastAssessedTime`

`lastUpdatedTimes`
: The time of the last modifications of the database details.

: **Field**: `lastUpdatedTime`

`migrationBlockersCounts`
: The number of blocking changes found.

: **Field**: `migrationBlockersCount`

`solutionNames`
: The names of the solution that sent the data.

: **Field**: `solutionName`

<superscript>*</superscript> For information on how to use filter criteria on plural resources refer to [FilterTable usage](https://github.com/inspec/inspec/blob/master/dev-docs/filtertable-usage.md).

## Examples

**Loop through migrate project databases by their names.**

```ruby
azure_migrate_project_databases(resource_group: 'RESOURCE_GROUP', project_name: 'PROJECT_NAME').names.each do |name|
  describe azure_migrate_project_database(resource_group: 'RESOURCE_GROUP', project_name: 'PROJECT_NAME', name: 'NAME') do
    it { should exist }
  end
end
```

**Test there are migrate project databases are ready for migration.**

```ruby
describe azure_migrate_project_database(resource_group: 'RESOURCE_GROUP', project_name: 'PROJECT_NAME').where{ isReadyForMigration.include?(true) } do
  it { should exist }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

```ruby
# Should not exist if no Migrate Project Databases are present in the project and in the resource group

describe azure_migrate_project_database(resource_group: 'RESOURCE_GROUP', project_name: 'PROJECT_NAME') do
  it { should_not exist }
end

# Should exist if the filter returns at least one Migrate Project Databases in the project and in the resource group

describe azure_migrate_project_database(resource_group: 'RESOURCE_GROUP', project_name: 'PROJECT_NAME') do
  it { should exist }
end
```

## Azure Permissions

Your [Service Principal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal) must be set up with a `contributor` role on the subscription you wish to test.
