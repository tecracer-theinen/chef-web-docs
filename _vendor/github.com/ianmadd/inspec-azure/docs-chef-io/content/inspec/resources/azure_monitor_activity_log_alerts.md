+++
title = "azure_monitor_activity_log_alerts Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_monitor_activity_log_alerts"
identifier = "inspec/resources/azure/azure_monitor_activity_log_alerts Resource"
parent = "inspec/resources/azure"
+++

Use the `azure_monitor_activity_log_alerts` InSpec audit resource to test properties and configuration of multiple Activity Log Alerts.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_monitor_activity_log_alerts` resource block returns all Activity Log Alerts, either within a Resource Group (if provided), or within an entire Subscription.
```ruby
describe azure_monitor_activity_log_alerts do
  it { should exist }
end
```
or
```ruby
describe azure_monitor_activity_log_alerts(resource_group: 'my-rg') do
  it { should exist }
end
```

## Parameters

- `resource_group` (Optional)

## Properties

`ids`
: A list of the unique resource ids.

: **Field**: `id`

`location`
: A list of locations for all the resources being interrogated.

: **Field**: `location`

`names`
: A list of names of all the resources being interrogated.

: **Field**: `name`

`tags`
: A list of `tag:value` pairs defined on the resources being interrogated.

: **Field**: `tags`

`operations`
: A list of operations for all the resources being interrogated.

: **Field**: `operations`

`resource_group`
: Azure resource group that the targeted resource resides in.

: **Field**: `resource_group`

<superscript>*</superscript> For information on how to use filter criteria on plural resources refer to [FilterTable usage](https://github.com/inspec/inspec/blob/master/dev-docs/filtertable-usage.md).

## Examples

**Test that a Subscription Has the Named Activity Log Alert.**

```ruby
describe azure_monitor_activity_log_alerts do
  its('names') { should include('ExampleLogAlert') }
end
```
**Loop through All Resources with `resource_id`.**

```ruby
azure_monitor_activity_log_alerts.ids.each do |id|
  describe azure_monitor_activity_log_alert(resource_id: id) do
    it { should be_enabled }
  end
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

The control will pass if the filter returns at least one result. Use `should_not` if you expect zero matches.
```ruby
# If we expect 'ExampleGroup' Resource Group to have Activity Log Alerts
describe azure_monitor_activity_log_alerts(resource_group: 'ExampleGroup') do
  it { should exist }
end

# If we expect 'EmptyExampleGroup' Resource Group to not have Activity Log Alerts
describe azure_monitor_activity_log_alerts(resource_group: 'ExampleGroup') do
  it { should_not exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
