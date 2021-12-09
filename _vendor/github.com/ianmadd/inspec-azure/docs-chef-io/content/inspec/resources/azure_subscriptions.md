+++
title = "azure_subscriptions Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_subscriptions"
identifier = "inspec/resources/azure/azure_subscriptions Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_subscriptions.md">https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_subscriptions.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_subscriptions.md">https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_subscriptions.md</a></p>
</div>
</div>


Use the `azure_subscriptions` InSpec audit resource to test properties and configuration of all Azure subscriptions for a tenant.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_subscriptions` resource block returns all subscription for a tenant.
```ruby
describe azure_subscriptions do
  it { should exist }
end
```

## Parameters

This resource does not require any parameters.

## Properties

`ids`
: A list of the subscription ids.

: **Field**: `id`

`names`
: A list of display names of all the subscriptions.

: **Field**: `name`

`tags`
: A list of `tag:value` pairs defined on the subscriptions.

: **Field**: `tags`

`tenant_ids`
: A list of tenant ids of all the subscriptions.

: **Field**: `tenant_id`

{{% inspec_filter_table %}}

## Examples

**Check a Specific Subscription is Present.**

```ruby
describe azure_subscriptions do
  its('names')  { should include 'my-subscription' }
end
``` 

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

The control will pass if the filter returns at least one result. Use `should_not` if you expect zero matches.
```ruby
describe azure_subscriptions do
  it { should exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
