+++
title = "aws_cloudwatch_dashboards Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_cloudwatch_dashboards"
identifier = "inspec/resources/aws/aws_cloudwatch_dashboards Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_cloudwatch_dashboards.md">aws_cloudwatch_dashboards.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_cloudwatch_dashboards.md">aws_cloudwatch_dashboards.md</a></p>
</div>
</div>



Use the `aws_cloudwatch_dashboards` InSpec audit resource to test properties of the plural AWS CloudWatch dashboard.

For additional information, including details on parameters and properties, see the [AWS documentation on AWS CloudWatch dashboard.](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-cloudwatch-dashboard.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

Ensure that the dashboard exists.

```ruby
describe aws_cloudwatch_dashboards do
  it { should exist }
end
```

## Parameters

This resource does not require any parameters.

## Properties

`dashboard_names`
: The name of the dashboard.

: **Field**: `dashboard_name`

`dashboard_arns`
: The Amazon Resource Name (ARN) of the dashboard.

: **Field**: `dashboard_arn`

`last_modified`
: The time stamp of when the dashboard was last modified, either by an API call or through the console.

: **Field**: `last_modified`

`sizes`
: The size of the dashboard, in bytes.

: **Field**: `size`

## Examples

**Ensure a dashboard ARN is available.**

```ruby
describe aws_cloudwatch_dashboards do
  its('dashboard_arns') { should include 'ARN' }
end
```

**Ensure a dashboard name is available.**

```ruby
describe aws_cloudwatch_dashboards do
    its('dashboard_names') { should include 'DASHBOARD_NAME' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

The controls will pass if the `list` method returns at least one result.

### exist

Use `should` to test that the entity exists.

```ruby
describe aws_cloudwatch_dashboards do
  it { should exist }
end
```

Use `should_not` to test the entity does not exist.

```ruby
describe aws_cloudwatch_dashboards do
  it { should_not exist }
end
```

## AWS Permissions

Your [Principal](https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-structure.html#intro-structure-principal) will need the `CloudWatch:Client:ListDashboardsOutput action with `Effect` set to `Allow`.