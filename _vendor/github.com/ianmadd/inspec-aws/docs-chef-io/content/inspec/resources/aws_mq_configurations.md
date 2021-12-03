+++
title = "aws_mq_configurations Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_mq_configurations"
identifier = "inspec/resources/aws/aws_mq_configurations Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_mq_configurations.md">aws_mq_configurations.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_mq_configurations.md">aws_mq_configurations.md</a></p>
</div>
</div>



Use the `aws_mq_configurations` InSpec audit resource to test the properties of multiple AWS MQ configuration.

## Installation

{{% inspec_aws_install %}}

## Syntax

Ensure that AWS MQ configuration exists.

```ruby
describe aws_mq_configurations do
  it { should exist }
end
```

For additional information, see the [AWS documentation on AWS MQ configuration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-amazonmq-configuration.html).

## Properties

`arns`
: The ARN of the configuration.

: **Field**: `arn`

`authentication_strategies`
: The authentication strategy associated with the configuration. The default is SIMPLE.

: **Field**: `authentication_strategy`

`Created`
: The date and time of the configuration revision.

: **Field**: `Created`

`description`
: The description of the configuration.

: **Field**: `description`

`engine_types`
: The type of broker engine. Currently, Amazon MQ supports ACTIVEMQ and RABBITMQ.

: **Field**: `engine_type`

`engine_versions`
: The broker engine's version. For a list of supported engine versions.

: **Field**: `engine_version`

`ids`
: The unique ID that Amazon MQ generates for the configuration.

: **Field**: `id`

`names`
: The name of the configuration.

: **Field**: `name`

`tags`
: The list of all tags associated with this configuration.

: **Field**: `tags`

## Examples

**Ensure a configuration id is available.**

```ruby
describe aws_mq_configurations do
  its('ids') { should include 'configuration_id' }
end
```

**Ensure a configuration name is available..**

```ruby
describe aws_mq_configurations do
    its('names') { should include 'configuration_name' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

The controls will pass if the `list` method returns at least one result.

### exist

Use `should` to test that the entity exists.

```ruby
describe aws_mq_configurations do
  it { should exist }
end
```

Use `should_not` to test the entity does not exist.

```ruby
describe aws_mq_configurations do
  it { should_not exist }
end
```

### be_available

Use `should` to check if the mq configuration is available.

```ruby
describe aws_mq_configurations do
  it { should be_available }
end
```

## AWS Permissions

Your [Principal](https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-structure.html#intro-structure-principal) will need the `MQ:Client:ListConfigurationsResponsegit ` action with `Effect` set to `Allow`.
