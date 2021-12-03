+++
title = "aws_api_gateway_deployments Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_api_gateway_deployments"
identifier = "inspec/resources/aws/aws_api_gateway_deployments Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_api_gateway_deployments.md">aws_api_gateway_deployments.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_api_gateway_deployments.md">aws_api_gateway_deployments.md</a></p>
</div>
</div>



Use the `aws_api_gateway_deployments` InSpec audit resource to test properties of multiple AWS ApiGateway Deployments.

The AWS::ApiGateway::Deployment resource deploys an API Gateway RestAPI resource to a stage so that clients can call the API over the internet. The stage acts as an environment.

For additional information, including details on parameters and properties, see the [AWS ApiGateway Deployment documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigateway-deployment.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

Ensure that the deployment exists.

```ruby
describe aws_api_gateway_deployments(rest_api_id: 'REST_API_ID') do
  it { should exist }
end
```

## Parameters

`rest_api_id` _(required)_

## Properties

`ids`
: The identifier for the deployment resource.

`descriptions`
: The description for the deployment resource.

`created_dates`
: The date and time that the deployment resource was created.

`api_summaries`
: A summary of the RestApi at the date and time that the deployment resource was created.

## Examples

**Ensure that the deployment ID exists.**

```ruby
describe aws_api_gateway_deployments(rest_api_id: 'REST_API_ID') do
  its('ids') { should include 'DEPLOYMENT_ID' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

The controls will pass if the `get` method returns at least one result.

### exist

Use `should` to test that the entity exists.

```ruby
describe aws_api_gateway_deployments(rest_api_id: 'REST_API_ID') do
  it { should exist }
end
```

Use `should_not` to test the entity does not exist.

```ruby
describe aws_api_gateway_deployments(rest_api_id: 'REST_API_ID') do
  it { should_not exist }
end
```

### be_available

Use `should` to check if the deployment is available.

```ruby
describe aws_api_gateway_deployments(rest_api_id: 'REST_API_ID') do
  it { should be_available }
end
```

## AWS Permissions

{{% aws_permissions_principal action="APIGateway:Client::Deployments" %}}
