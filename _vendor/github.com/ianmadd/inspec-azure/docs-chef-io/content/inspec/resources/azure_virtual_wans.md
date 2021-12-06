+++
title = "azure_virtual_wans Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_virtual_wans"
identifier = "inspec/resources/azure/azure_virtual_wans Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_virtual_wans.md">https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_virtual_wans.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_virtual_wans.md">https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_virtual_wans.md</a></p>
</div>
</div>


Use the `azure_virtual_wans` InSpec audit resource to test the properties related to all Azure Virtual WANs in a subscription.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

An `azure_virtual_wans` resource block returns all Azure Virtual WANs in a subscription.

```ruby
describe azure_virtual_wans do
  #...
end
```

## Properties

`ids`
: A list of the unique resource ids.

: **Field**: `id`

`names`
: A list of names for all the Resources.

: **Field**: `name`

`etags`
: A list of etag for all the Resources.

: **Field**: `etag`

`types`
: A list of types for all the resources.

: **Field**: `type`

`locations`
: A list of locations for all the resources.

: **Field**: `location`

`properties`
: A list of Properties all the resources.

: **Field**: `properties`

<superscript>*</superscript> For information on how to use filter criteria on plural resources refer to [FilterTable usage](https://github.com/inspec/inspec/blob/master/dev-docs/filtertable-usage.md).

## Examples

**Test that the Virtual WAN type is Standard.**

```ruby
describe azure_virtual_wans.where{ properties.select{|prop| prop.type == 'Standard' } } do
  it { should exist }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

```ruby
# Should not exist if no virtual WANs are present

describe azure_virtual_wans do
  it { should_not exist }
end

# Should exist if the filter returns at least one virtual WAN

describe azure_virtual_wans do
  it { should exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal_contributor %}}
