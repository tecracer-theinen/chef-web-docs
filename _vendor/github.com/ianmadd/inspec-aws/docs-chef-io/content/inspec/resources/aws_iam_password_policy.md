+++
title = "aws_iam_password_policy Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_iam_password_policy"
identifier = "inspec/resources/aws/aws_iam_password_policy Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_iam_password_policy.md">https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_iam_password_policy.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_iam_password_policy.md">https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_iam_password_policy.md</a></p>
</div>
</div>


Use the `aws_iam_password_policy` InSpec audit resource to test properties of an AWS IAM Password Policy.

For additional information, including details on parameters and properties, see the [AWS documentation on Auto Scaling Group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

An `aws_iam_password_policy` resource block declares the tests for an AWS IAM Password Policy.

```ruby
describe aws_iam_password_policy do
  it { should exist }
end
```

## Parameters

This resource does not expect any parameters.

## Properties

`minimum_password_length`
: The minimum character count of the password policy.

`max_password_age_in_days`
: Integer representing in days how long a password may last before expiring.

`number_of_passwords_to_remember`
: Number of previous passwords to remember.

## Examples

**Test that a Password Policy meets your company's requirements.**

```ruby
describe aws_iam_password_policy do
  it                             { should require_uppercase_characters }
  it                             { should require_lowercase_characters }
  it                             { should require_numbers }
  its('minimum_password_length') { should be > 8 }
end
```

**Test that users can change their own passwords .**

```ruby
describe aws_iam_password_policy do
  it { should allow_users_to_change_password }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [matchers page](https://www.inspec.io/docs/reference/matchers/).

### exist

```ruby
it { should exist }
```

#### prevent_password_reuse
```ruby
it { should prevent_password_reuse }
```

#### expire_passwords 
```ruby
it { should expire_passwords }
```

#### require_numbers   
```ruby
it { should require_numbers }
```

#### require_symbols
```ruby
it { should require_symbols }
```

#### require_lowercase_characters
```ruby
it { should require_lowercase_characters }
```

#### require_uppercase_characters
```ruby
it { should require_uppercase_characters}
```

#### allow_users_to_change_passwords
```ruby
it { should allow_users_to_change_password }
```

All matchers can use the inverse `should_not` predicate.

## AWS Permissions

Your [Principal](https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-structure.html#intro-structure-principal) will need the following permissions action set to allow: `IAM:Client:GetAccountPasswordPolicyResponse`
