+++
title = "aws_network_manager_device Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_network_manager_device"
identifier = "inspec/resources/aws/aws_network_manager_device Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_network_manager_device.md">https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_network_manager_device.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_network_manager_device.md">https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_network_manager_device.md</a></p>
</div>
</div>


Use the `aws_network_manager_device` InSpec audit resource to test properties of a single specific AWS Network Manager device.

The `AWS::NetworkManager::Device` resource gets information about one or more of your devices in a global network.

For additional information, including details on parameters and properties, see the [AWS documentation on AWS Network Manager Device](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-networkmanager-device.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

Ensure that a device exists.

```ruby
describe aws_network_manager_device(device_id: 'DEVICE_ID', global_network_id: 'GLOBAL_NETWORK_ID') do
  it { should exist }
end
```

## Parameters

`device_id` _(required)_

: The ID of the device.

`global_network_id` _(required)_

: The ID of the global network.

## Properties

`device_id`
: The ID of the device.

`device_arn`
: The Amazon Resource Name (ARN) of the device.

`global_network_id`
: The ID of the global network.

`aws_location.zone`
: The Zone the device is located in. This can be the ID of an Availability Zone, Local Zone, Wavelength Zone, or an Outpost.

`aws_location.subnet_arn`
: The Amazon Resource Name (ARN) of the subnet the device is located in.

`description`
: The description of the device.

`type`
: The device type.

`vendor`
: The device vendor.

`model`
: The device model.

`serial_number`
: The device serial number.

`location.address`
: The physical address of the location.

`location.latitude`
: The latitude of the location.

`location.longitude`
: The longitude of the location.

`site_id`
: The site ID.

`created_at`
: The date and time that the site was created.

`state`
: The device state.

`tags`
: The tags for the device.

## Examples

**Ensure a device ID is available.**

```ruby
describe aws_network_manager_device(device_id: 'DEVICE_ID', global_network_id: 'GLOBAL_NETWORK_ID') do
  its('device_id') { should eq 'DEVICE_ID' }
end
```

**Ensure a global network ID is available.**

```ruby
describe aws_network_manager_device(device_id: 'DEVICE_ID', global_network_id: 'GLOBAL_NETWORK_ID') do
  its('global_network_id') { should eq 'GLOBAL_NETWORK_ID' }
end
```

**Ensure a zone is available.**

```ruby
describe aws_network_manager_device(device_id: 'DEVICE_ID', global_network_id: 'GLOBAL_NETWORK_ID') do
  its('aws_location.zone') { should eq 'ZONE_NAME' }
end
```

**Ensure that the state is `AVAILABLE`.**

```ruby
describe aws_network_manager_global_network(device_id: 'DEVICE_ID', global_network_id: 'GLOBAL_NETWORK_ID') do
    its('state') { should eq 'AVAILABLE' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

The controls will pass if the `get` method returns at least one result.

### exist

Use `should` to test that the entity exists.

```ruby
describe aws_network_manager_device(device_id: 'DEVICE_ID', global_network_id: 'GLOBAL_NETWORK_ID') do
  it { should exist }
end
```

Use `should_not` to test the entity does not exist.

```ruby
describe aws_network_manager_device(device_id: 'DEVICE_ID', global_network_id: 'GLOBAL_NETWORK_ID') do
  it { should_not exist }
end
```

### be_available

Use `should` to check if the entity is available.

```ruby
describe aws_network_manager_device(device_id: 'DEVICE_ID', global_network_id: 'GLOBAL_NETWORK_ID') do
  it { should be_available }
end
```

## AWS Permissions

{{% aws_permissions_principal action="NetworkManager:Client:GetDevicesResponse" %}}
