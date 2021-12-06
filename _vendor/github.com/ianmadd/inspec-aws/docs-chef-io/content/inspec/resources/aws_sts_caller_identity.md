+++
title = "aws_sts_caller_identity Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_sts_caller_identity"
identifier = "inspec/resources/aws/aws_sts_caller_identity Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_sts_caller_identity.md">https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_sts_caller_identity.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_sts_caller_identity.md">https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_sts_caller_identity.md</a></p>
</div>
</div>


Use the `aws_sts_caller_identity` InSpec audit resource to test properties of AWS IAM identity whose credentials are used in the current InSpec scan.

## Installation

{{% inspec_aws_install %}}

## Syntax

An `aws_sts_caller_identity` resource block may be used to perform tests on details of the AWS credentials being used in the current Inspec scan. You can also test if the credentials belong to a GovCloud account or not.

```ruby
describe aws_sts_caller_identity do
  it { should exist }
end
```


## Parameters

`name` _(required)_

: This resource does not expect any parameters.

## Properties

`arn`
: The AWS ARN associated with the calling entity.

`account`
: The AWS account ID number of the account that owns or contains the calling entity.

`user_id`
: The unique identifier of the calling entity.

For more info, see [the API reference documentation](https://docs.aws.amazon.com/STS/latest/APIReference/API_GetCallerIdentity.html)

## Examples

**Check that the credentials used to run the scan is correct.**

```ruby
describe aws_sts_caller_identity do
  its("arn") { should match "arn:aws:iam::.*:user/service-account-inspec" }
end
```

**Test if the account belongs to GovCloud.**

```ruby
describe aws_sts_caller_identity do
  it { should be_govcloud }
end
```

**Skip a test if we are using GovCloud.**

```ruby
if aws_sts_caller_identity.govcloud?
  describe 'Skipping Root User MFA check as we are on GovCloud' do
    skip
  end
else
  describe aws_iam_root_user do
    it { should have_mfa_enabled }  
  end
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [matchers page](https://www.inspec.io/docs/reference/matchers/).

### be_govcloud

The `be_govcloud` matcher tests if the account is a 'GovCloud' AWS Account.

```ruby
describe aws_sts_caller_identity do
    it { should_not be_govcloud }
end
```

## AWS Permissions

{{% aws_permissions_principal action="STS:Client:GetCallerIdentityResponse" %}}
