+++
title = "aws_ec2_prefix_lists Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_ec2_prefix_lists"
identifier = "inspec/resources/aws/aws_ec2_prefix_lists Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_ec2_prefix_lists.md">aws_ec2_prefix_lists.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_ec2_prefix_lists.md">aws_ec2_prefix_lists.md</a></p>
</div>
</div>



Use the `aws_ec2_prefix_lists` InSpec audit resource to test properties of multiple AWS EC2 prefix lists.

The `AWS::EC2::PrefixList` resource specifies a managed prefix list.

For additional information, including details on parameters and properties, see the [AWS documentation on AWS EC2 prefix lists](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-prefixlist.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

Ensure that a prefix list exists.

```ruby
describe aws_ec2_prefix_lists do
  it { should exist }
end
```

## Parameters

This resource does not require any parameters.

## Properties

`prefix_list_ids`
: The ID of the prefix list.

: **Field**: `prefix_list_id`

`address_families`
: The IP address version.

: **Field**: `address_family`

`states`
: The state of the prefix list.

: **Field**: `state`

`state_messages`
: The state message.

: **Field**: `state_message`

`prefix_list_arns`
: The Amazon Resource Name (ARN) for the prefix list.

: **Field**: `prefix_list_arn`

`prefix_list_names`
: The name of the prefix list.

: **Field**: `prefix_list_name`

`max_entries`
: The maximum number of entries for the prefix list.

: **Field**: `max_entries`

`versions`
: The version of the prefix list.

: **Field**: `version`

`tags`
: The tags for the prefix list.

: **Field**: `tags`

`owner_ids`
: The ID of the owner of the prefix list.

: **Field**: `owner_id`

## Examples

**Ensure a prefix list ID is available.**

```ruby
describe aws_ec2_prefix_lists do
  its('prefix_list_ids') { should include 'PREFIX_LIST_ID' }
end
```

**Ensure an address family is available.**

```ruby
describe aws_ec2_prefix_lists do
  its('address_families') { should include 'ADDRESS_FAMILY' }
end
```

**Ensure that the state is `AVAILABLE`.**

```ruby
describe aws_ec2_prefix_lists do
    its('states') { should include 'AVAILABLE' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

The controls will pass if the `describe` method returns at least one result.

### exist

Use `should` to test that the entity exists.

```ruby
describe aws_ec2_prefix_lists do
  it { should exist }
end
```

Use `should_not` to test the entity does not exist.

```ruby
describe aws_ec2_prefix_lists do
  it { should_not exist }
end
```

## AWS Permissions

{{% aws_permissions_principal action="EC2:Client:DescribeManagedPrefixListsResult" %}}
