+++
title = "azure_streaming_analytics_functions Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_streaming_analytics_functions"
identifier = "inspec/resources/azure/azure_streaming_analytics_functions Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_streaming_analytics_functions.md">https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_streaming_analytics_functions.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_streaming_analytics_functions.md">https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_streaming_analytics_functions.md</a></p>
</div>
</div>


Use the `azure_streaming_analytics_functions` InSpec audit resource to test properties and configuration of multiple Azure streaming analytics functions.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_streaming_analytics_functions` resource block returns all functions  under a job.

```ruby
describe azure_streaming_analytics_functions(resource_group: "RESOURCE_GROUP", job_name: "AZURE_STREAMING_JOB_NAME") do
  #...
end
```

## Parameters

`resource_group` _(required)_

: Azure resource group that the targeted resource resides in.

`job_name` _(required)_

: Name of the job.

## Properties

`ids`
: A list of the unique resource ids.

: **Field**: `id`

`names`
: A list of names of all the resources being interrogated.

: **Field**: `name`

`tags`
: A list of `tag:value` pairs defined on the resources being interrogated.

: **Field**: `tags`

`properties`
: A list of properties for all the resources being interrogated.

: **Field**: `properties`

Also, refer to [Azure documentation](https://docs.microsoft.com/en-us/rest/api/streamanalytics/) for other properties available.
Any attribute in the response may be accessed with the key names separated by dots (`.`), eg. `properties.<attribute>`.

<superscript>*</superscript> For information on how to use filter criteria on plural resources refer to [FilterTable usage](https://github.com/inspec/inspec/blob/master/dev-docs/filtertable-usage.md).

## Examples

**Test that the names should be an array.**

```ruby
describe azure_streaming_analytics_functions(resource_group: "RESOURCE_GROUP", job_name: "AZURE_STREAMING_JOB_NAME") do
  its('names') { should be_an(Array) }
end

```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

The control will pass if the filter returns at least one result.
```ruby
describe azure_streaming_analytics_functions(resource_group: "RESOURCE_GROUP", job_name: "AZURE_STREAMING_JOB_NAME") do
  it { should exist }
end
```

Use `should_not` if you expect zero matches.

```ruby
describe azure_streaming_analytics_functions(resource_group: "RESOURCE_GROUP", job_name: "AZURE_STREAMING_JOB_NAME") do
  it { should_not exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
