+++
title = "azure_virtual_network_gateway Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_virtual_network_gateway"
identifier = "inspec/resources/azure/azure_virtual_network_gateway Resource"
parent = "inspec/resources/azure"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-azure/blob/main/docs/resources/azure_virtual_network_gateway.md">azure_virtual_network_gateway.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-azure/blob/im/hugo/docs-chef-io/content/inspec/resources/azure_virtual_network_gateway.md">azure_virtual_network_gateway.md</a></p>
</div>
</div>



Use the `azure_virtual_network_gateway` InSpec audit resource to test the properties and configuration of an Azure virtual network gateway.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

`resource_group` and `name` are required parameters.

```ruby
describe azure_virtual_network_gateway(resource_group: 'RESOURCE_GROUP', name: 'VIRTUAL_NETWORK_NAME') do
  it { should exist }
end
```

## Parameters

`resource_group` _(REQUIRED)_

: The Azure resource group that the targeted resource resides in.

`name` _(REQUIRED)_

: The unique name of the targeted resource.

## Properties

`name`
: The resource name.

`id`
: The resource ID.

`etag`
: A unique read-only string that changes whenever the resource is updated.

`type`
: The resource type.

`location`
: The resource location.

`tags`
: The resource tags.

`properties.bgpSettings`
: The virtual network gateway's BGP speaker settings.

`properties.provisioningState`
: The provisioning state of the virtual network gateway resource.

`properties.vpnClientConfiguration`
: The reference to the VpnClientConfiguration resource which represents the P2S VpnClient configurations.

For properties applicable to all resources, such as `type`, `name`, `id`, `properties`, refer to [`azure_generic_resource`]({{< relref "azure_generic_resource.md#properties" >}}).

Also, refer to [Azure documentation](https://docs.microsoft.com/en-us/rest/api/network-gateway/virtual-network-gateways/get) for other available properties. Any attribute in the response is accessed with the key names separated by dots (`.`).

## Examples

**Test the VPN client protocol of a virtual network gateway.**

```ruby
describe azure_virtual_network_gateway(resource_group: 'RESOURCE_GROUP', name: 'VIRTUAL_NETWORK_NAME') do
  its('properties.vpnClientConfiguration.vpnClientProtocols') { should include 'OpenVPN' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://docs.chef.io/inspec/matchers/).

### exists

```ruby
# If we expect a virtual network gateway to always exist

describe azure_virtual_network_gateway(resource_group: 'RESOURCE_GROUP', name: 'VIRTUAL_NETWORK_NAME') do
  it { should exist }
end

# If we expect virtual network gateway to never exist

describe azure_virtual_network_gateway(resource_group: 'RESOURCE_GROUP', name: 'VIRTUAL_NETWORK_NAME') do
  it { should_not exist }
end
```

## Azure Permissions

Your [Service Principal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal) must be set up with a minimum of `reader` role on the subscription you wish to test.
