+++
title = "aws_rds_snapshot Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_rds_snapshot"
identifier = "inspec/resources/aws/aws_rds_snapshot Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_rds_snapshot.md">https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_rds_snapshot.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_rds_snapshot.md">https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_rds_snapshot.md</a></p>
</div>
</div>


Use the `aws_rds_snapshot` InSpec audit resource to test the detailed properties of an individual RDS snapshot.

For additional information, including details on parameters and properties, see the [AWS documentation on RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

An `aws_rds_snapshot` resource block uses resource parameters to search for an RDS snapshot and test the respective RDS snapshot.  

No error is raised if no RDS snapshots match. However, the `exists` matcher will return `false`, and all properties will be `nil`.  

An error is raised if more than one RDS snapshot matches (due to vague search parameters).

```ruby
describe aws_rds_snapshot('TEST-SNAPSHOT-ID') do
  it { should exist }
end
```

    # Can also use hash syntax
```ruby
describe aws_rds_snapshot(db_snapshot_identifier: 'TEST-SNAPSHOT-ID') do
  it { should exist }
end
```

## Parameters

`db_snapshot_identifier`

: This resource accepts a single parameter either as a string or a `db_snapshot_identifier: 'value'` key-value entry in a hash. This parameter is user-supplied DB snapshot identifier. This parameter isn't case-sensitive and is a required parameter.

## Properties

For a comprehensive list of properties available to test on an RDS snapshot see the [AWS Response Object](https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/RDS/Types/DBSnapshot.html)

## Examples

**Tests the engine used is with an RDS snapshot.**

```ruby
describe aws_rds_snapshot(db_snapshot_identifier: 'AWSRDS123') do
  its ('engine')         { should eq 'MYSQL' }
  its ('engine_version') { should eq '5.6.37' }
end
```

**Tests the storage allocated to an RDS snapshot.**

```ruby
describe aws_rds_snapshot(db_snapshot_identifier: 'AWSRDS123') do
  its ('allocated_storage') { should eq 10 }
end
```

**Tests the snapshot type and master username.**

```ruby
describe aws_rds_snapshot(db_snapshot_identifier: 'AWSRDS123') do
  its ('master_username')   { should eq 'DB-MAINTAIN' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [matchers page](https://www.inspec.io/docs/reference/matchers/).

### exist

The control will pass if the describe returns at least one result.

Use `should_not` to test the entity should not exist.

```ruby
describe aws_rds_snapshot(db_snapshot_identifier: 'AnExistingRDS') do
  it { should exist }
end
```

```ruby
describe aws_rds_snapshot(db_snapshot_identifier: 'ANonExistentRDS') do
  it { should_not exist }
end
```

## AWS Permissions

{{% aws_permissions_principal action="RDS:Client:DBSnapshotMessage" %}}

You can find detailed documentation at [Actions, Resources, and Condition Keys for Amazon RDS](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_amazonrds.html).
