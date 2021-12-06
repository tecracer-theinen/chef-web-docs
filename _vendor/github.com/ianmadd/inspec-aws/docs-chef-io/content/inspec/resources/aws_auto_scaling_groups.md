+++
title = "aws_auto_scaling_groups Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_auto_scaling_groups"
identifier = "inspec/resources/aws/aws_auto_scaling_groups Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_auto_scaling_groups.md">https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_auto_scaling_groups.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_auto_scaling_groups.md">https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_auto_scaling_groups.md</a></p>
</div>
</div>


Use the `aws_auto_scaling_groups` InSpec audit resource to test the properties of a collection of AWS Auto Scaling Groups.

For additional information, including details on parameters and properties, see the [AWS documentation on Auto Scaling Group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

An `aws_auto_scaling_groups` resource block returns all Auto Scaling Groups and allows the testing of those ASGs.

```ruby
describe aws_auto_scaling_groups do
  its('names') { should include 'group-name' }
end
```

## Parameters

This resource does not expect any parameters.

## Properties

`min_sizes`
: An integer indicating the minimum number of instances in the auto scaling group.

`max_sizes`
: An integer indicating the maximum number of instances in the auto scaling group.

`desired_capacities`
: An integer indicating the desired  number of instances in the auto scaling group.

`launch_configuration_names`
: The name of the auto scaling launch configuration associated with the auto scaling group.

`vpc_zone_identifiers`
: An array of strings corresponding to the subnet IDs associated with the auto scaling group.

`health_check_types`
: The service to use for the health checks. The valid values are EC2 and ELB.

`tags`
: A hash of key-value pairs corresponding to the tags associated with the entity.

`entries`
: Provides access to the raw results of the query, which can be treated as an array of hashes.

## Examples

**Ensure there are no groups with incorrect vpc_zone_identifiers.**

```ruby
describe aws_auto_scaling_groups do
  it                          { should exist }
  its('vpc_zone_identifiers') { should_not include 'UNDESIRED-ZONE'}
end
```

## Matchers

For a full list of available matchers, please visit our [matchers page](https://www.inspec.io/docs/reference/matchers/).

### exist

The control will pass if the describe returns at least one result.

Use `should_not` to test the entity should not exist.

```ruby
describe aws_auto_scaling_groups.where( <property>: <value>) do
  it { should exist }
end
```

```ruby
describe aws_auto_scaling_groups.where( <property>: <value>) do
  it { should_not exist }
end
```

## AWS Permissions

{{% aws_permissions_principal action="AutoScaling:Client:AutoScalingGroupsType" %}}
You can find detailed documentation at [Actions, Resources, and Condition Keys for Amazon Auto Scaling Groups](https://docs.aws.amazon.com/autoscaling/ec2/userguide/control-access-using-iam.html).
