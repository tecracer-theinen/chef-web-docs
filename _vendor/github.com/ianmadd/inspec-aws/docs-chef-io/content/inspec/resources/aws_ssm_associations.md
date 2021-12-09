+++
title = "aws_ssm_associations Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_ssm_associations"
identifier = "inspec/resources/aws/aws_ssm_associations Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_ssm_associations.md">https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_ssm_associations.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_ssm_associations.md">https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_ssm_associations.md</a></p>
</div>
</div>


Use the `aws_ssm_associations` InSpec audit resource to test properties of a collection of AWS SSM Associations.

## Installation

{{% inspec_aws_install %}}

## Syntax

 Ensure you have exactly 3 associations

```ruby
describe aws_ssm_associations do
  its('names.count') { should cmp 3 }
end
```

## Parameters

This resource does not require any parameters.

## Properties

`association_ids`
: Provides the ID of the association.

`association_names`
: Provides the name of the association.

`association_versions`
: Provides the version of the association.

`document_versions`
: Provides the document version used in the association.

`instance_ids`
: Provides the id of the instance.

`last_execution_dates`
: The date on which the association was last run.

`names`
: The name of the Systems Manager document.

`overviews`
: Provides information about the association.

`schedule_expressions`
: A cron expression that specifies a schedule when the association runs.

`targets`
: Provides the instances targeted by the request to create an association.

For a comprehensive list of properties available, see [the API reference documentation](https://docs.aws.amazon.com/systems-manager/latest/APIReference/API_Association.html)

## Examples

**Ensure an Association ID of a SSM Association exists.**

```ruby
describe aws_ssm_associations do
  its('association_ids') { should include 'association-id' }
end
```

## Matchers

For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exist

The control will pass if the describe returns at least one result.

Use `should_not` to test the entity should not exist.

```ruby
describe aws_ssm_associations.where( <property>: <value> ) do
  it { should exist }
end
```

```ruby
describe aws_ssm_associations.where( <property>: <value> ) do
  it { should_not exist }
end
```

## AWS Permissions

{{% aws_permissions_principal action="SSM:Client:ListAssociationsResult" %}}

You can find detailed documentation at [Actions, Resources, and Condition Keys for Amazon Systems Manager](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awssystemsmanager.html).