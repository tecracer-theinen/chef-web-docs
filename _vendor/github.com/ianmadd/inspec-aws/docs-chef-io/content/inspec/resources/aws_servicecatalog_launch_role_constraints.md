+++
title = "aws_servicecatalog_launch_role_constraints Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_servicecatalog_launch_role_constraints"
identifier = "inspec/resources/aws/aws_servicecatalog_launch_role_constraints Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_servicecatalog_launch_role_constraints.md">https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_servicecatalog_launch_role_constraints.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_servicecatalog_launch_role_constraints.md">https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_servicecatalog_launch_role_constraints.md</a></p>
</div>
</div>


Use the `aws_servicecatalog_launch_role_constraints` InSpec audit resource to test properties of multiple AWS Service Catalog launch constraint.

For additional information, including details on parameters and properties, see the [AWS documentation on AWS ServiceCatalog LaunchRoleConstraint](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-servicecatalog-launchroleconstraint.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

Ensure that a portfolio exists.

```ruby
describe aws_servicecatalog_launch_role_constraints(portfolio_id: 'PORTFOLIO_ID') do
  it { should exist }
end
```

## Parameters

`portfolio_id` _(required)_

: The identifier of the portfolio the product resides in.

## Properties

`constraint_ids`
: The identifier of the constraint.

`types`
: The type of constraint. Valid values are: `LAUNCH`, `NOTIFICATION`, `RESOURCE_UPDATE`, `STACKSET`, and `TEMPLATE`.

`descriptions`
: The description of the constraint.

`owners`
: The owner of the constraint.

`product_ids`
: The identifier of the product the constraint applies to. Note that a constraint applies to a specific instance of a product within a certain portfolio.

`portfolio_ids`
: The identifier of the portfolio the product resides in. The constraint applies only to the instance of the product that lives within this portfolio.

## Examples

**Ensure a constraint is available.**

```ruby
describe aws_servicecatalog_launch_role_constraints(portfolio_id: 'PORTFOLIO_ID') do
  its('constraint_ids') { should include 'ID' }
end
```

**Ensure that the type is 'LAUNCH'.**

```ruby
describe aws_servicecatalog_launch_role_constraints(portfolio_id: 'PORTFOLIO_ID') do
    its('types') { should include 'LAUNCH' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

The controls will pass if the `list` method returns at least one result.

### exist

Use `should` to test that the entity exists.

```ruby
describe aws_servicecatalog_launch_role_constraints(portfolio_id: 'PORTFOLIO_ID') do
  it { should exist }
end
```

Use `should_not` to test the entity does not exist.

```ruby
describe aws_servicecatalog_launch_role_constraints(portfolio_id: 'PORTFOLIO_ID') do
  it { should_not exist }
end
```

## AWS Permissions

{{% aws_permissions_principal action="ServiceCatalog:Client:ListConstraintsForPortfolioOutput" %}}
