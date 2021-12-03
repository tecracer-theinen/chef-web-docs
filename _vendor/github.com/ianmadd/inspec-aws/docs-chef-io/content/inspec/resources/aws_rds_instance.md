+++
title = "aws_rds_instance Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_rds_instance"
identifier = "inspec/resources/aws/aws_rds_instance Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_rds_instance.md">aws_rds_instance.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_rds_instance.md">aws_rds_instance.md</a></p>
</div>
</div>



Use the `aws_rds_instance` InSpec audit resource to test detailed properties of an individual RDS instance.

RDS gives you access to the capabilities of a MySQL, MariaDB, PostgreSQL, Microsoft SQL Server, Oracle, or Amazon Aurora database server.

For additional information, including details on parameters and properties, see the [AWS documentation on RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

An `aws_rds_instance` resource block uses resource parameters to search for an RDS instance, and then tests that RDS instance.  If no RDS instances match, no error is raised, but the `exists` matcher will return `false` and all properties will be `nil`.  If more than one RDS instance matches (due to vague search parameters), an error is raised.

```ruby
describe aws_rds_instance('test-instance-id') do
  it { should exist }
end
```

    # Can also use hash syntax
```ruby
describe aws_rds_instance(db_instance_identifier: 'test-instance-id') do
  it { should exist }
end
```

## Parameters

`db_instance_identifier` _(required)_

: This resource accepts a single parameter, the user-supplied instance identifier. This parameter isn't case-sensitive.
  This can be passed either as a string or as a `db_instance_identifier: 'value'` key-value entry in a hash.

## Properties

For a comprehensive list of properties available to test on an RDS Instance see the [AWS Response Object](https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/RDS/Types/DBInstance.html)

## Examples

**Test the engine used with an RDS instance.**

```ruby
describe aws_rds_instance(db_instance_identifier: 'awsrds123') do
  its ('engine')         { should eq 'mysql' }
  its ('engine_version') { should eq '5.6.37' }
end
```

**Test the storage allocated to an RDS instance.**

```ruby
describe aws_rds_instance(db_instance_identifier: 'awsrds123') do
  its ('storage_type')      { should eq 'gp2' }
  its ('allocated_storage') { should eq 10 }
end
```

**Test the instance type and master username.**

```ruby
describe aws_rds_instance(db_instance_identifier: 'awsrds123') do
  its ('master_username')   { should eq 'db-maintain' }
  its ('db_instance_class') { should eq 'db.t3.micro' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [matchers page](https://www.inspec.io/docs/reference/matchers/).

### exist

The control will pass if the describe returns at least one result.

Use `should_not` to test the entity should not exist.

```ruby
describe aws_rds_instance(db_instance_identifier: 'AnExistingRDS') do
  it { should exist }
end
```

```ruby
describe aws_rds_instance(db_instance_identifier: 'ANonExistentRDS') do
  it { should_not exist }
end
```

## AWS Permissions

{{% aws_permissions_principal action="RDS:Client:DBInstanceMessage" %}}

You can find detailed documentation at [Actions, Resources, and Condition Keys for Amazon RDS](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_amazonrds.html).
