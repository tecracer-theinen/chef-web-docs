+++
title = "aws_sns_topics Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_sns_topics"
identifier = "inspec/resources/aws/aws_sns_topics Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_sns_topics.md">aws_sns_topics.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_sns_topics.md">aws_sns_topics.md</a></p>
</div>
</div>



Use the `aws_sns_topics` InSpec audit resource to test all or a group of the SNS Topic ARNs in an account.

User the 'aws_sns_topic' InSpec audit resource to test a single SNS Topic in an account.

For additional information, including details on parameters and properties, see the [AWS documentation on SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

    # Get all SNS Topic arns
```ruby
describe aws_sns_topics do
  its('topic_arns') { should include 'arn:aws:sns:us-east-1:333344445555:MyTopic' }
end
```

## Parameters

This resource does not expect any parameters.

## Properties

`topic_arns`
: The ARNs of the SNS Topics.

`entries`
: Provides access to the raw results of the query, which can be treated as an array of hashes.

## Examples

The following examples show how to use this InSpec audit resource.

**Ensure a Topic exists.**

```ruby
describe aws_sns_topics do
  its('topic_arns') { should include 'arn:aws:sns:us-east-1:333344445555:MyTopic' }
end
```

## Matchers

### exist

The control will pass if the describe returns at least one result.

Use `should_not` to test the entity should not exist.

```ruby
describe aws_sns_topics do
  it { should exist }
end
```

```ruby
describe aws_sns_topics do
  it { should_not exist }
end
```

## AWS Permissions

{{% aws_permissions_principal action="SNS:Client:ListTopicsResponse" %}}

You can find detailed documentation at [Actions, Resources, and Condition Keys for Amazon SNS](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_amazonsns.html).
