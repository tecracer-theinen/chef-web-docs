+++
title = "aws_elasticloadbalancingv2_listener_certificates Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_elasticloadbalancingv2_listener_certificates"
identifier = "inspec/resources/aws/aws_elasticloadbalancingv2_listener_certificates Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_elasticloadbalancingv2_listener_certificates.md">aws_elasticloadbalancingv2_listener_certificates.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_elasticloadbalancingv2_listener_certificates.md">aws_elasticloadbalancingv2_listener_certificates.md</a></p>
</div>
</div>



Use the `aws_elasticloadbalancingv2_listener_certificates` InSpec audit resource to test properties of multiple TLS or HTTPS listener certificates.

For additional information, including details on parameters and properties, see the [AWS documentation on ElasticLoadBalancingV2 Listener Certificate](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-elasticloadbalancingv2-listenercertificate.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

Ensure that a listener ARN exists.

```ruby
describe aws_elasticloadbalancingv2_listener_certificates(listener_arn: 'LISTENER_ARN') do
  it { should exist }
end
```

## Parameters

`listener_arn` _(required)_

: The Amazon Resource Name (ARN) of the listener certificate.

## Properties

`certificate_arns`
: The Amazon Resource Name (ARN) of the certificate.

`is_default`
: Indicates whether the certificate is the default certificate.

## Examples

**Ensure a listener ARN is available.**

```ruby
describe aws_elasticloadbalancingv2_listener_certificates(listener_arn: 'LISTENER_ARN') do
  it { should exist }
end
```

**Ensure that listener has a desired certificate ARN attached.**

```ruby
describe aws_elasticloadbalancingv2_listener_certificates(listener_arn: 'LISTENER_ARN') do
  its('certificate_arns') { should include "CERTIFICATE_ARN" }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

The controls will pass if the `describe` method returns at least one result.

### exist

Use `should` to test that the entity exists.

```ruby
describe aws_elasticloadbalancingv2_listener_certificates(listener_arn: 'LISTENER_ARN') do
  it { should exist }
end
```

Use `should_not` to test the entity does not exist.

```ruby
describe aws_elasticloadbalancingv2_listener_certificates(listener_arn: 'LISTENER_ARN') do
  it { should_not exist }
end
```

## AWS Permissions

{{% aws_permissions_principal action="ElasticLoadBalancingV2:Client:DescribeListenerCertificatesOutput" %}}
