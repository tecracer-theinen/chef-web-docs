+++
title = "aws_hosted_zones Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_hosted_zones"
identifier = "inspec/resources/aws/aws_hosted_zones Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_hosted_zones.md">aws_hosted_zones.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_hosted_zones.md">aws_hosted_zones.md</a></p>
</div>
</div>



Use the `aws_hosted_zones` resource to test the hosted zones configuration.

## Installation

{{% inspec_aws_install %}}

## Syntax

````
    describe aws_hosted_zones do
      its('names') { should include ("carry-on.films.com") }
    end
````    

## Parameters

This resource does not expect any parameters.


## Properties

`name`
: The name of the hosted zone.

`id`
: It's id.

## Examples


**Ensure a specific hosted zone exists.**

````
    describe aws_hosted_zones do
      its('names') { should include ("carry-on.films.com") }
    end
````

## Matchers

This InSpec audit resource uses the following special matcher. For a full list of available matchers, please visit our [matchers page](https://www.inspec.io/docs/reference/matchers/).

### should

The control will pass if the describe passes all tests.

Use `should` to validate if a specific hosted zone exists

````
    describe aws_hosted_zones do
      its('names') { should include ("carry-on.films.com") }
    end

````

## AWS Permissions

{{% aws_permissions_principal action="Route53:Client:ListHostedZonesResponse" %}}

You can find detailed documentation at [Amazon Route 53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/r53-api-permissions-ref.html)

