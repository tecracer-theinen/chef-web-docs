+++
title = "aws_ebs_volumes Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_ebs_volumes"
identifier = "inspec/resources/aws/aws_ebs_volumes Resource"
parent = "inspec/resources/aws"
+++

Use the `aws_ebs_volumes` InSpec audit resource to test properties of a collection of AWS EBS volumes.

EBS volumes are persistent block storage volumes for use with Amazon EC2 instances in the AWS Cloud.

For additional information, including details on parameters and properties, see the [AWS documentation on EBS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

 Ensure you have exactly 3 volumes

```ruby
describe aws_ebs_volumes do
  its('volume_ids.count') { should cmp 3 }
end
```

## Parameters

This resource does not expect any parameters.

## Properties

`volume_ids`
: The unique IDs of the EBS Volumes returned.

`entries`
: Provides access to the raw results of the query, which can be treated as an array of hashes.

## Examples

**Ensure a specific volume exists.**

```ruby
describe aws_ebs_volumes do
  its('volume_ids') { should include 'vol-12345678' }
end
```

**Use the InSpec resource to request the IDs of all EBS volumes, then test in-depth using `aws_ebs_volume` to ensure all volumes are encrypted and have a sensible size.**

```ruby
aws_ebs_volumes.volume_ids.each do |volume_id|
  describe aws_ebs_volume(volume_id) do
    it          { should be_encrypted }
    its('size') { should be > 10 }
    its('iops') { should cmp 100 }
  end
end
```


## Matchers

For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exist

The control will pass if the describe returns at least one result.

Use `should_not` to test the entity should not exist.

```ruby
describe aws_ebs_volumes do
  it { should exist }
end
```

```ruby
describe aws_ebs_volumes do
  it { should_not exist }
end
```

## AWS Permissions

{{% aws_permissions_principal action="EC2:Client:DescribeVolumesResult" %}}
You can find detailed documentation at [Actions, Resources, and Condition Keys for Amazon EC2](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_amazonec2.html), and [Actions, Resources, and Condition Keys for Identity And Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_identityandaccessmanagement.html).
