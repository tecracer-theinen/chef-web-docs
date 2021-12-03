+++
title = "aws_cognito_identity_pool Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_cognito_identity_pool"
identifier = "inspec/resources/aws/aws_cognito_identity_pool Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_cognito_identity_pool.md">aws_cognito_identity_pool.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_cognito_identity_pool.md">aws_cognito_identity_pool.md</a></p>
</div>
</div>



Use the `aws_cognito_identity_pool` InSpec audit resource to test properties of a single Cognito identity pool.

For additional information, including details on parameters and properties, see the [AWS documentation on Cognito identity pool](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-cognito-identitypool.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

Ensure that an identity pool exists.
```ruby
describe aws_cognito_identity_pool(identity_pool_id: 'IDENTITY_POOL_ID') do
  it { should exist }
end
```

## Parameters

`identity_pool_id` _(required)_

## Properties

`identity_pool_id`
: An identity pool ID in the format REGION:GUID.

`identity_pool_name`
: The name of your Amazon Cognito identity pool.

`allow_unauthenticated_identities`
: Specifies whether the identity pool supports unauthenticated logins.

`supported_login_providers`
: Key-value pairs that map provider names to provider app IDs.

`developer_provider_name`
: The "domain" Amazon Cognito uses when referencing your users. This name acts as a placeholder that allows your backend and the Amazon Cognito service to communicate about the developer provider. For the DeveloperProviderName, you can use letters and periods (.), underscores (_), and dashes (-).

`open_id_connect_provider_arns`
: The Amazon Resource Names (ARNs) of the OpenID connect providers.

`cognito_identity_providers (provider_name)`
: The Amazon Cognito user pools and their client IDs. The provider name of the cognito identity providers.

`cognito_identity_providers (client_id)`
: The Amazon Cognito user pools and their client IDs. The client ID of the cognito identity providers.

`cognito_identity_providers (server_side_token_check)`
: The Amazon Cognito user pools and their client IDs. The server side token check of the cognito identity providers.

`saml_provider_arns`
: The Amazon Resource Names (ARNs) of the Security Assertion Markup Language (SAML) providers.

`identity_pool_tags`
: The tags of your Amazon Cognito identity pool.

## Examples

**Ensure an identity pool ID is available.**

```ruby
describe aws_cognito_identity_pool(identity_pool_id: 'IDENTITY_POOL_ID') do
  its('identity_pool_id') { should eq 'IDENTITY_POOL_ID' }
end
```

**Ensure that the identity pool name is available.**

```ruby
describe aws_cognito_identity_pool(identity_pool_id: 'IDENTITY_POOL_ID') do
    its('identity_pool_name') { should eq 'IDENTITY_POOL_NAME' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

The controls will pass if the `describe` method returns at least one result.

### exist

Use `should` to test that the entity exists.

```ruby
describe aws_cognito_identity_pool(identity_pool_id: 'IDENTITY_POOL_ID') do
  it { should exist }
end
```

Use `should_not` to test the entity does not exist.

```ruby
describe aws_cognito_identity_pool(identity_pool_id: 'IDENTITY_POOL_ID') do
  it { should_not exist }
end
```

### be_available

Use `should` to check if the identity pool id is available.

```ruby
describe aws_cognito_identity_pool(identity_pool_id: 'IDENTITY_POOL_ID') do
  it { should be_available }
end
```

## AWS Permissions

{{% aws_permissions_principal action="CognitoIdentity:Client:IdentityPool" %}}
